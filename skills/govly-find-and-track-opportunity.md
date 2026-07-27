---
name: Find and track a government opportunity
description: Search Govly opportunities, inspect one, follow it, and open a workspace to collaborate on a bid.
api: openapi/govly-tools-v1-openapi-original.yml
operations: [search_opportunities, show_opportunity, follow_entity, create_workspace]
---

# Find and track a government opportunity

Authenticate every request with a Govly API key: `Authorization: Bearer gk_...`
or the `X-API-KEY` header. HTTPS only. Responses are JSON with a cursor envelope.

1. **Search** — `POST /api/tools/v1/opportunities/search` (`search_opportunities`).
   Defaults to open opportunities; searchType defaults to your market focus
   (fed or sled). Page with the returned `meta.nextCursor`.
2. **Inspect** — `GET /api/tools/v1/opportunities/{id}` (`show_opportunity`) for
   full detail on a candidate.
3. **Follow** — `POST /api/tools/v1/follows` (`follow_entity`) to track changes.
   For opportunities this creates or reuses the default opportunity workspace.
4. **Workspace** — `POST /api/tools/v1/workspaces` (`create_workspace`) if you
   need a dedicated collaboration space.

Errors return a JSON:API envelope (`errors[].source.pointer` locates the bad
field). No idempotency key — do not blindly retry POSTs.
