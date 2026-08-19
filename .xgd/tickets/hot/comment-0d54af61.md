---
uid: comment-0d54af61
id: COMMENT-14
type: comment
title: Comment on goal GOAL-62
created_by: xgd
created_at: '2026-08-19T18:10:24.536489+00:00'
updated_at: '2026-08-19T18:10:24.536489+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-74b33543
  kind: note
---

2026-08-19 - operator named this **the big XGD goal**: *"I think the big xgd goal is the knowledge management - getting that up and running could unlock so much."*

Recorded here because the model has no priority or ordering field, so a statement like that has nowhere else to live. It is not derivable from the ticket trail either - by ticket count this goal is one draft (xgd/REQ-775) against three ready_to_reconcile framework tickets, which reads as nearly-done rather than as the highest-leverage thing on the map. The trail cannot tell you what a goal unlocks. Only the operator can.

The dependency is clearing: access control (goal-959f56f3) is expected in the rear-view today, and REQ-806 - the redesign that was blocking it - is free_coded with 519 tests green.

Standing caution, unchanged and worth repeating now that this is next: REQ-775 is a **replacement**. It deletes the static priming assembler rather than running beside it. Unlike the dashboard refactor (goal-77251769), which the operator has explicitly noted can be run alongside the old code, this one has no cheap rollback. Two refactors queued behind the same dependency, two different risk profiles - do not sequence them as if they were the same kind of change.