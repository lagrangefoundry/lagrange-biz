---
uid: comment-a468d5f5
id: COMMENT-12
type: comment
title: Comment on goal GOAL-50
created_by: xgd
created_at: '2026-08-19T18:09:13.132945+00:00'
updated_at: '2026-08-19T18:09:13.132945+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-959f56f3
  kind: note
---

**Sequencing hazard for today, from REQ-806 own record - read before turning off the overrides on main.**

REQ-806 flags two deliberate gaps, one of which is order-dependent and bites today:

> Main live `.xgd/permissions.yaml` still carries the OLD schema - I cannot write it myself (self-protection blocks this session unconditionally, by design, confirmed live). Content is prepared; applying it must happen AFTER this code is installed into `.venv-working` - **old code cannot parse the new schema, confirmed this would break session resolution if sequenced the other way around.**

So the order is: merge REQ-806 to `xgd-working` -> install into `.venv-working` -> *then* apply the prepared `permissions.yaml`. Applying the file first breaks every session launch. The self-protection working correctly is what forces the two-step, which is a good sign and an inconvenience at the same time.

Second gap, lower stakes: the dashboard WHERE/WHAT split tile and hover text were reviewed for syntax only - no running dashboard or browser was available in that session. That is part of the "UI details" still outstanding, alongside REQ-803 (tile renamed to "AI access permissions", ready_to_reconcile).

Also resolved and worth not re-litigating: none of REQ-806 four commits carry the `[FREE-CODED]` tag. The operator chose ticket-level commit attachment over a history rewrite, so `fields.commits` on REQ-806 (`c64efec72b5`, `7e39d447ebc`, `d5926e9911a`, `065268cb2a0`) is the authoritative link regardless of message text. Reconcile should read the ticket, not grep the messages.