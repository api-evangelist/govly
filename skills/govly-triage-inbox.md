---
name: Triage the Govly AI-match inbox
description: List AI and saved-search matches, inspect them, and accept, decline, or dismiss each item.
api: openapi/govly-tools-v1-openapi-original.yml
operations: [list_inbox_items, show_inbox_item, accept_inbox_item, decline_inbox_item, dismiss_inbox_item, restore_inbox_item]
---

# Triage the Govly AI-match inbox

Authenticate with `Authorization: Bearer gk_...` or `X-API-KEY`.

1. **List** — `GET /api/tools/v1/inbox_items` (`list_inbox_items`): active
   Govly AI matches and saved-search matches, newest first.
2. **Inspect** — `GET /api/tools/v1/inbox_items/{id}` (`show_inbox_item`).
3. **Act** on each item:
   - `POST .../{id}/accept` (`accept_inbox_item`) — follows the underlying
     opportunity/award/signal and opens its workspace. **Accept is FINAL and
     cannot be restored.** The response `meta.workspaceId` is the result.
   - `POST .../{id}/decline` (`decline_inbox_item`) — mark a bad fit (optionally
     with a reason that feeds matching-exclusions memory). Reversible.
   - `POST .../{id}/dismiss` (`dismiss_inbox_item`) — dismiss. Reversible.
4. **Restore** — `POST .../{id}/restore` (`restore_inbox_item`) returns a
   dismissed or declined item to the active inbox; an accepted item cannot be
   restored.
