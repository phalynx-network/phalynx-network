# Published API inconsistencies

The dedicated API page ([https://phalynx.network/docs/api](https://phalynx.network/docs/api)) and the complete documentation ([https://phalynx.network/ai](https://phalynx.network/ai)) do not always describe the same API. This repository does **not** reconcile them. [`openapi.yaml`](openapi.yaml) follows `/docs/api` when they conflict, and marks `/ai`-only paths as such.

| Topic | `/docs/api` | `/ai` (v2.0, July 2026) |
| --- | --- | --- |
| Authentication | JWT Bearer. Register at `POST https://api.phalynx.network/v1/auth/register` with `deviceId`, `deviceType`, `publicKey`; response `token`, `expiresAt`. | Ed25519: `Authorization: Signature <base64_signature>`, `X-Public-Key`, `X-Timestamp` (within 5 minutes). No JWT or register endpoint. |
| Base URL | Curl host `https://api.phalynx.network/v1/...` | Explicitly `https://api.phalynx.network/v1` |
| Path headings | `POST /api/cases`, `POST /api/cases/:id/evidence`, and similar | `POST /api/cases`, `GET /api/cases/:id`, and similar |
| Create-case body | `victimId`, `claimValue`, `category`, `location`, `metadata.description` | `victimId`, `claimValue`, `category`, `description`, `location` (no `metadata` wrapper). Example category `ASSAULT` vs `PROPERTY_DAMAGE`. |
| Create-case response | `caseId`, `victimBond`, `defendantBond`, `status`, `createdAt` (201) | `caseId`, `victimBond`, `defendantBond`, `expiresAt` (72 hours to post DB). No `status`. |
| Evidence upload | JSON including `totalChunks` | `multipart/form-data`; `totalChunks` not shown |
| Jury commit body | `jurorId`, `commitHash` | `commitHash` only |
| Jury reveal | Request `jurorId`, `verdict`, `salt`; response `verified`, `timestamp` | Request `vote`, `salt`; response `verdict`, `confidence` |
| Burn | Request `verdictTokenId`, `burnProof`; response `burnTxHash`, `burnedAmount`, `timestamp` | Titled “Initiate Token Burn (Not Guilty)”; response `burnProof`, `burnTxHash` |
| Webhooks | Events `CASE_FILED`, `VERDICT_REACHED`, `SETTLEMENT_COMPLETE` (payload `event: VERDICT_REACHED`) | Register events `verdict.finalized`, `settlement.complete`; payload uses lowercase `guilty` and a `confidence` field |
| Extra endpoints | Not listed | `GET /api/cases/:id`, `GET /api/reputation/:userId`, WebSocket `wss://ws.phalynx.network/v1/cases/:id/stream` |
| Rate limits | Evidence 100 chunks/min/device; case creation 10/hour/victim; queries 1000/hour/token | General 100/min/IP; case creation 10/hour/account; evidence 100 chunks/min/case; monthly cap 3 cases/month/account |

There is also mixed path notation on both pages (headings say `/api/...` while curl examples and the `/ai` base URL use `https://api.phalynx.network/v1/...`). Bond math on `/docs/economics` and the `/ai` economics section is presented as `VB = α × ClaimValue × (RI_high / max(RI, RI_floor))` (with clamp and defaults on the economics page). Treat that as the published page text; do not replace it with unpublished alternate formulas from private sketches.
