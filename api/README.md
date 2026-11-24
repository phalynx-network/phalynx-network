<!--
Source: https://phalynx.network/docs/api
Extracted: 2026-11-24 (America/New_York) from the public PhalynX Network site.
The site JS bundle was last-modified 2026-08-30 (HTTP Last-Modified on https://phalynx.network/assets/index-DQnlPCMO.js).
This file is a faithful Markdown conversion of the published page. Mermaid diagrams
were restored from the site source bundle. No protocol content was invented.
-->

# API Reference

REST API documentation for integrating with the PhalynX Network protocol.

## Authentication

All API requests require JWT authentication. Obtain a token by registering your device or application:

```bash
# Register device
curl -X POST https://api.phalynx.network/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "deviceId": "ring_camera_001",
    "deviceType": "CAMERA",
    "publicKey": "0x1a2b3c..."
  }'

# Response
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expiresAt": "2025-10-23T14:30:00Z"
}
```

Include the token in the Authorization header:

```bash
curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

## Rate Limits

API endpoints are rate-limited to prevent abuse:

* **Evidence submission:** 100 chunks/minute per device
* **Case creation:** 10 cases/hour per victim
* **Query endpoints:** 1000 requests/hour per token

> Rate limit headers are included in all responses. Exceeding limits results in HTTP 429 with retry-after header.

## Idempotency Keys

Use idempotency keys to safely retry requests without duplicate effects:

```bash
curl -X POST https://api.phalynx.network/v1/cases \
  -H "Authorization: Bearer ..." \
  -H "Idempotency-Key: 550e8400-e29b-41d4-a716-446655440000" \
  -H "Content-Type: application/json" \
  -d '{ "claimValue": 5000, "category": "PROPERTY_DAMAGE" }'
```

## Endpoints

### POST /api/cases

Create a new case and initiate the evidence collection phase.

```bash
POST /api/cases
Content-Type: application/json
Authorization: Bearer <token>

{
  "victimId": "0xVictimAddress",
  "claimValue": 5000,
  "category": "PROPERTY_DAMAGE",
  "location": {
    "lat": 15.9932,
    "lon": -61.9450
  },
  "metadata": {
    "description": "Broken window from rock throwing"
  }
}

# Response 201 Created
{
  "caseId": "550e8400-e29b-41d4-a716-446655440000",
  "victimBond": 250,
  "defendantBond": 6000,
  "status": "FILED",
  "createdAt": "2025-10-22T14:30:00Z"
}
```

### POST /api/cases/:id/evidence

Submit evidence chunks for a specific case.

```bash
POST /api/cases/550e8400-e29b-41d4-a716-446655440000/evidence
Content-Type: application/json
Authorization: Bearer <token>

{
  "chunkIndex": 0,
  "totalChunks": 10,
  "dataHash": "sha256:a3f5d8...",
  "encryptedBlob": "base64_encrypted_data",
  "deviceSignature": "0x9f8e7d..."
}

# Response 201 Created
{
  "chunkId": "chunk_001",
  "merkleProof": ["hash1", "hash2", "hash3"],
  "status": "ATTESTED"
}
```

### POST /api/jury/:id/commit

Submit a hashed vote during the commit phase.

```bash
POST /api/jury/550e8400-e29b-41d4-a716-446655440000/commit
Content-Type: application/json
Authorization: Bearer <token>

{
  "jurorId": "0xJuror1",
  "commitHash": "sha256:commit_hash_of_verdict_plus_salt"
}

# Response 201 Created
{
  "commitId": "commit_001",
  "timestamp": "2025-10-22T15:45:00Z",
  "revealDeadline": "2025-10-22T16:00:00Z"
}
```

### POST /api/jury/:id/reveal

Reveal the plaintext vote during the reveal phase.

```bash
POST /api/jury/550e8400-e29b-41d4-a716-446655440000/reveal
Content-Type: application/json
Authorization: Bearer <token>

{
  "jurorId": "0xJuror1",
  "verdict": "GUILTY",
  "salt": "random_salt_string"
}

# Response 200 OK
{
  "verified": true,
  "timestamp": "2025-10-22T15:55:00Z"
}
```

### POST /api/verdicts/:id/burn

Execute token burn after settlement completion.

```bash
POST /api/verdicts/550e8400-e29b-41d4-a716-446655440000/burn
Content-Type: application/json
Authorization: Bearer <token>

{
  "verdictTokenId": "vt_12345",
  "burnProof": "0xMerkleProof..."
}

# Response 200 OK
{
  "burnTxHash": "0xBTC_tx_hash",
  "burnedAmount": 450,
  "timestamp": "2025-10-22T16:30:00Z"
}
```

## Error Codes

| Code | Message | Description |
| --- | --- | --- |
| 400 | Bad Request | Invalid request format or missing required fields |
| 401 | Unauthorized | Missing or invalid JWT token |
| 403 | Forbidden | Insufficient permissions for operation |
| 404 | Not Found | Case, jury, or verdict not found |
| 409 | Conflict | Duplicate operation (check idempotency key) |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Unexpected server error |

## Webhooks

Register webhook endpoints to receive real-time case updates:

```bash
POST /api/webhooks
Content-Type: application/json
Authorization: Bearer <token>

{
  "url": "https://your-app.com/webhooks/phalynx",
  "events": ["CASE_FILED", "VERDICT_REACHED", "SETTLEMENT_COMPLETE"]
}

# Webhook payload example
{
  "event": "VERDICT_REACHED",
  "caseId": "550e8400-e29b-41d4-a716-446655440000",
  "verdict": "GUILTY",
  "timestamp": "2025-10-22T16:00:00Z"
}
```

> **OpenAPI Specification**
>
> Download the complete OpenAPI 3.0 specification at `/api/openapi.yaml` for automated client generation.


> **Note on `/api/openapi.yaml`:** The published API page tells readers to download an OpenAPI 3.0 specification at `/api/openapi.yaml`. As of this extraction, that URL is not a static YAML file — the site serves the SPA HTML shell instead. A draft OpenAPI document derived from this page (and, where clearly marked, from `/ai`) is in [`openapi.yaml`](openapi.yaml). Published conflicts between `/docs/api` and `/ai` are listed in [`NOTES.md`](NOTES.md).
