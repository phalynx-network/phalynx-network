# Source and extraction notes

Assembled 2026-11-24 (America/New_York) from the public website [phalynx.network](https://phalynx.network).

## What this tree is

A faithful conversion of the protocol documentation already published on the site: the whitepaper, the `/docs/*` pages, the `/ai` complete documentation (v2.0, July 2026), JSON examples, derived JSON Schemas, and a **draft** OpenAPI file. Nothing here is a claim that the API is live or that `/api/openapi.yaml` already exists on the site (it did not, as of this extraction).

The site JS bundle (`https://phalynx.network/assets/index-DQnlPCMO.js`, HTTP Last-Modified 2026-08-30) is a compiled React SPA. Pages were rendered from the live site and converted to Markdown. Mermaid diagrams were restored from the bundle so they remain editable. No protocol rules, fields, or endpoints were invented to fill gaps.

## Site routes that were linked but not published

These URLs are linked from the public site but were not registered in the site router at extraction time (they return 404). There was no published text to copy:

- `/docs/legal/tos` and `/docs/legal/privacy` (footer links)
- `/docs/integrations/devices`, `/docs/integrations/responders`, `/docs/integrations/drones`, `/docs/integrations/collectors`
- `/docs/api/overview`
- `/api/openapi.yaml` (advertised on the API page; the site serves the SPA HTML shell instead)

Integration material that *is* published — the integrations index and the Integration Guides section of `/ai` — is included in `docs/integrations.md` and `docs/complete.md`.

## Published inconsistencies (not silently merged)

- **API auth, paths, rate limits, and payload shapes** differ between `/docs/api` and `/ai`. See [`api/NOTES.md`](api/NOTES.md).
- **`/api/openapi.yaml` is advertised but not actually served.** The draft in `api/openapi.yaml` is derived, not downloaded.
- **Bond formula presentation** on `/docs/economics` and the `/ai` economics section is `VB = α × ClaimValue × (RI_high / max(RI, RI_floor))` (with clamp and defaults on the economics page). Treat that as the published page text.
- Endpoint headings say `/api/...` while curl examples and the `/ai` base URL use `https://api.phalynx.network/v1/...`.

Derived JSON Schemas (`schemas/*.schema.json`) and the draft OpenAPI file follow only fields and examples shown on the public pages. Each schema’s `$comment` records that derivation. `/ai` message sketches that differ from `/docs/protocol` were not merged into those schemas.

## Assets not copied

The explainer poster and the site favicon/logo are in [`assets/`](assets/README.md). The live site also serves a Grok-named hero image, a Grok-named hero video, and a ~20 MB explainer video that were left out pending a license and attribution decision. See `assets/README.md`.

## License

Copyright (c) 2026 PhalynX Network. All rights reserved. These materials are published for reference only; no license to copy, modify, or distribute is granted without written permission. Contact: [contact@phalynx.network](mailto:contact@phalynx.network). See [`LICENSE`](LICENSE).
