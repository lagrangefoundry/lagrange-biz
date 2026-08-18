---
uid: comment-c2cad4b5
id: COMMENT-9
type: comment
title: Comment on goal GOAL-46
created_by: xgd
created_at: '2026-08-18T20:03:42.522318+00:00'
updated_at: '2026-08-18T20:03:42.522318+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-39ddc03c
  kind: note
---

Sweep 2026-08-18. lagrange-framework/BUG-32 - dashboard restart re-drains orphaned chat_sessions/*.jsonl from offset 0, appending stale turns at the transcript tail - is now **ready_to_reconcile** (was planned/in flight).

That is the ticket behind the symptom the operator described today: *"the broken transcript chunk that keeps coming back still has the old date on it."* The stale date is the tell - the re-drained turns carry their original timestamps, so a chunk reappearing with yesterday date is the offset-0 re-read, not a new write. Consistent with BUG-32 diagnosis, and with the operator read that it is nearly fixed.

Worth noting what this goal body already argues: a transcript that loses or duplicates turns is the failure of the one thing this interface promises. It is also the only bug on the map whose symptom the operator can observe directly while using the tool, which is why it keeps surfacing in conversation rather than in a ticket queue.