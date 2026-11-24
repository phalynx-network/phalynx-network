<!--
Source: https://phalynx.network/docs/integrations
Extracted: 2026-11-24 (America/New_York) from the public PhalynX Network site.
The site JS bundle was last-modified 2026-08-30 (HTTP Last-Modified on https://phalynx.network/assets/index-DQnlPCMO.js).
This file is a faithful Markdown conversion of the published page. Mermaid diagrams
were restored from the site source bundle. No protocol content was invented.
-->

# Integrations

Integration guides for devices, responders, drones, and debt collectors.

The site documentation index links to four dedicated guides. Those routes were not published as standalone pages at extraction time (they 404). Titles and one-line descriptions below are taken from the public integrations index.

- [Device Integration](https://phalynx.network/docs/integrations/devices) — Connect Ring cameras, mobile apps, and IoT sensors to the gateway *(page not published; 404)*
- [Responder Integration](https://phalynx.network/docs/integrations/responders) — Private security and emergency dispatch protocols *(page not published; 404)*
- [Drone Integration](https://phalynx.network/docs/integrations/drones) — Drone-in-a-box bounty system for aerial evidence collection *(page not published; 404)*
- [Collector Integration](https://phalynx.network/docs/integrations/collectors) — Export court bundles to traditional legal and debt collection systems *(page not published; 404)*


## Quick Start

All integrations follow a similar pattern:

1. **Register:** Obtain API credentials and device/service ID
2. **Authenticate:** Use JWT tokens for all API requests
3. **Implement:** Follow the specific integration guide
4. **Test:** Use sandbox environment before production

## Device Integration Example

Here's a basic example of submitting evidence from a Ring camera:

```bash
# 1. Create a case
curl -X POST https://api.phalynx.network/v1/cases \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "victimId": "0xVictimAddress",
    "claimValue": 5000,
    "category": "PROPERTY_DAMAGE",
    "deviceId": "ring_camera_001"
  }'

# 2. Stream evidence chunks
curl -X POST https://api.phalynx.network/v1/cases/{caseId}/evidence \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "chunkIndex": 0,
    "totalChunks": 10,
    "dataHash": "sha256:a3f5d8...",
    "encryptedBlob": "base64_video_frame",
    "deviceSignature": "0x9f8e7d..."
  }'
```

For complete integration guides, select a specific integration type above.


---

## Integration Guides (from the `/ai` complete documentation)

The four dedicated integration routes linked above (`/docs/integrations/devices`, `/responders`, `/drones`, `/collectors`) were not published as standalone pages on the site at extraction time (they 404). The following section is copied from the public complete documentation at [https://phalynx.network/ai](https://phalynx.network/ai), which does include integration guides. Event names and payload shapes here are not always identical to the `/docs/api` page; see [`../api/NOTES.md`](../api/NOTES.md).

# 13. Integration Guides

Integration guides for developers building on PhalynX Network.

### Quick Start

```bash
# 1. Create a case
POST /api/cases
→ Returns caseId, victimBond, defendantBond

# 2. Upload evidence
POST /api/cases/{caseId}/evidence
→ Returns merkleProof

# 3. Poll case status
GET /api/cases/{caseId}
→ Returns state, verdict, settlement
```

### Smart Ring SDK

Integrate SOS functionality into wearable devices:

```bash
npm install @phalynx/ring-sdk

import { RingClient } from '@phalynx/ring-sdk';

const ring = new RingClient({
  apiKey:   'your_api_key',
  deviceId: 'ring_001'
});

ring.on('sos', async (event) => {
  await ring.startEvidenceSession(event);
});
```

### Mobile App Integration

```typescript
// iOS (Swift)
import PhalynxSDK

let client = PhalynxClient(apiKey: "...")
client.startEvidenceCapture(caseId: "...") { result in
  // Handle evidence upload
}

// Android (Kotlin)
val client = PhalynxClient(apiKey = "...")
client.startEvidenceCapture(caseId = "...") { result ->
  // Handle evidence upload
}
```

### Knowledge Node Operation

```bash
docker run -d \
  -v /data/phalynx:/data \
  -p 9944:9944 \
  -e PHLX_STAKE=10000 \
  phalynx/knowledge-node:latest

# Requirements:
# - Minimum PHLX stake: 10,000 PHLX
# - Uptime SLA: 99%+ (penalized below threshold)
# - Storage: 1 TB minimum
# - RI: starts at 0.5; builds with successful attestations
```

### Webhook Integration

```bash
# Register webhook
POST /api/webhooks
{
  "url":    "https://your-app.com/webhooks/phalynx",
  "events": ["verdict.finalized", "settlement.complete"]
}

# Webhook payload example
POST https://your-app.com/webhooks/phalynx
{
  "event":     "verdict.finalized",
  "caseId":    "...",
  "verdict":   "guilty",
  "confidence": 0.91,
  "timestamp": "2025-10-22T16:00:00Z"
}
```
