# Schemas

JSON Schema documents and examples for PhalynX Network protocol messages and a few API request/response bodies.

## Provenance

These files were **derived** from examples and TypeScript-shaped interfaces published on [https://phalynx.network/docs/protocol](https://phalynx.network/docs/protocol) and [https://phalynx.network/docs/api](https://phalynx.network/docs/api) as of 2026-11-24. They are not an official closed specification: each schema's `$comment` says so, `additionalProperties` is `true`, and only fields shown on the site are listed.

The `/ai` complete documentation also publishes message sketches that are not identical to the `/docs/protocol` examples (for example an attestation sketch that includes Bitcoin transaction fields, and a `SETTLEMENT` message type). Those sketches were **not** merged into the schemas here. Compare [`../docs/complete.md`](../docs/complete.md) before treating a field as required.

## Message schemas

| Schema | Example | Source |
| --- | --- | --- |
| [base-message.schema.json](base-message.schema.json) | — | `interface BaseMessage` on `/docs/protocol` |
| [sos.schema.json](sos.schema.json) | [examples/sos.json](examples/sos.json) | SOS Event example |
| [evidence-chunk.schema.json](evidence-chunk.schema.json) | [examples/evidence-chunk.json](examples/evidence-chunk.json) | Evidence Chunk example |
| [attestation.schema.json](attestation.schema.json) | [examples/attestation.json](examples/attestation.json) | Attestation example |
| [verdict.schema.json](verdict.schema.json) | [examples/verdict.json](examples/verdict.json) | Verdict example |

`examples/api-*.json` are request or response objects copied from the `/docs/api` page.

## TypeScript interfaces published in the docs

The following interfaces appear as code samples on the public docs pages (not all are given JSON examples). See the linked page rather than a separately invented schema:

- `BaseMessage`, `MessageValidator`, `ProtocolError` — [protocol.md](../docs/protocol.md)
- `SOSEvent`, `HapticEvent` — [architecture.md](../docs/architecture.md)
- `VoteCommit`, `Vote` — [jury-protocol.md](../docs/jury-protocol.md)
- `TAPActivation`, `TapGesture` — [evidence-pipeline.md](../docs/evidence-pipeline.md) (and related TAP Ring flow)
- `CoCEntry`, `EvidenceObject`, `KeyShard` — evidence and security pages
- `BondParams` and payout helper types — [economics.md](../docs/economics.md)
- `PCSParams`, `LCTEntry`, `GovernanceProposal`, and related types — [governance.md](../docs/governance.md)
- Token and settlement types (`VerdictToken`, `DebtNetting`, `InvestorPayout`, and others) — [tokens.md](../docs/tokens.md) and [settlement.md](../docs/settlement.md)
