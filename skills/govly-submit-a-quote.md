---
name: Submit a quote to a procurement portal
description: Check submission requirements, upload the quote file, submit it, and poll status to completion.
api: openapi/govly-tools-v1-openapi-original.yml
operations: [get_quote_submission_requirements, upload_workspace_attachments, create_quote_submission, show_quote_submission]
---

# Submit a quote to a procurement portal

Authenticate with `Authorization: Bearer gk_...` or `X-API-KEY`. HTTPS + JSON.

1. **Requirements** — `GET /api/tools/v1/quote/submissions/requirements`
   (`get_quote_submission_requirements`): returns portal-specific fields and any
   blocking reasons for the actor + workspace.
2. **Upload** — `POST /api/tools/v1/workspaces/{workspaceId}/attachments`
   (`upload_workspace_attachments`): upload the quote file first; keep the
   returned `workspaceAttachmentId`.
3. **Submit** — `POST /api/tools/v1/quote/submissions` (`create_quote_submission`)
   passing the `workspaceAttachmentId`. Returns a submission id.
4. **Poll** — `GET /api/tools/v1/quote/submissions/{id}` (`show_quote_submission`)
   until `meta.terminal` is true. Completed submissions carry confirmation
   details; failures include `failureReason`.

Do not resubmit on a transient error before polling — there is no idempotency
contract, and a duplicate submit may double-file.
