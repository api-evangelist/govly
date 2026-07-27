---
name: Research government contract awards
description: Search awarded contracts and drill into a single award's transactions, sub-awards, and related records.
api: openapi/govly-tools-v1-openapi-original.yml
operations: [search_awards, show_award]
---

# Research government contract awards

Authenticate with `Authorization: Bearer gk_...` or `X-API-KEY`. HTTPS + JSON.

1. **Search** — `POST /api/tools/v1/awards/search` (`search_awards`): searches
   all time unless a `dateRange` is given. `searchType` defaults to the
   authenticated user's market focus (fed or sled); sled and international
   require the matching organization subscription (else a 403 envelope).
2. **Show** — `GET /api/tools/v1/awards/{id}` (`show_award`): a single award with
   transactions, sub-awards, related opportunities, program links, line items,
   places, classification codes, and contacts. The path id accepts either an
   all-digit Govly award database id or the award's external identifier.

Page results with `meta.nextCursor`.
