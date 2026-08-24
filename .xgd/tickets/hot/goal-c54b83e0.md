---
uid: goal-c54b83e0
id: GOAL-57
type: goal
title: New chat implementation
created_by: xgd
created_at: '2026-08-12T00:14:58.277933+00:00'
updated_at: '2026-08-24T22:24:19.557219+00:00'
completed_at: null
last_field_updated: children
status: concept
fields:
  provenance: planned
  children:
  - ticket://lagrangefoundry/xgd/GOAL-10
  workstream: false
---

**Owned by xgd/GOAL-10 (Chat update).** That ticket is the authoritative record and is considerably better sourced than this one ever was - it carries REQ-741 (`free_and_reconciled`), REQ-794 and REQ-795 (`ready_to_reconcile`), REQ-762 and REQ-782, with DOC-984 as context. This goal composes from it and should not be edited in parallel.

Scope: the dashboard chat moves onto the webui-chat component and the gendevlabs.ai backend, with real session semantics - turn lifecycle, resume, persisted per-turn timestamps - and the Goals-tab chat role gains full cross-project ticket read/write.

## Why this sits under quality rather than features

Chat is the surface this interface runs on. A transcript that loses or duplicates turns is the failure of the one thing the product promises, and it destroys the audit trail the accountability whitepapers rest on - see goal-39ddc03c (Chat infrastructure is dependable), which is the reliability half of the same concern.

The two are worth holding apart: goal-39ddc03c is about transcripts surviving; this is about the chat implementation itself being a component rather than hand-rolled. lagrange-framework/BUG-32 (dashboard restart re-drains orphaned session logs from offset 0, appending stale turns with their original timestamps) belongs to the former.