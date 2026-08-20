---
uid: comment-375a99ec
id: COMMENT-19
type: comment
title: Comment on goal GOAL-43
created_by: xgd
created_at: '2026-08-20T01:08:57.203869+00:00'
updated_at: '2026-08-20T01:08:57.203869+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-61027b65
  kind: note
---

**2026-08-19 evening - BUG-1132 landed. `ready_to_reconcile`.**

Answered by the operator at 16:04, implemented the same evening. The projection now credits `ready_to_reconcile` and `reconciling` as `realized` per decision-cc46439b.

What this changes, in order of how much it matters:

1. **Roughly thirty leaves stop lying about themselves.** Done-but-for-machinery work will read as done.
2. **The roll-up disagreement detector unblinds.** This is the one to act on next. Until today, derived always agreed with declared because every non-terminal child collapsed to a single value, so genuinely stale declared states never surfaced. Once this reconciles, the disagreement list becomes meaningful for the first time - and the sweep of the 28 `in_progress` goals, which I have been unable to do because a mis-rendered goal and a stale one were indistinguishable, becomes a single pass. **Worth running the digest and asking me to sweep declared states once BUG-1132 is through reconcile.**
3. `realized` will jump discontinuously from 2 of 67. That is the backlog being credited, not corruption - decision-cc46439b exists so it reads correctly later.

Also landed today on this goal territory: BUG-1212 (permissions tile blocking on redundant cross-project git sweeps), BUG-1210 (orphan tile shows truncated command with no cwd/project), BUG-1203 (Allow Any Command switch replacing the permission-mode dropdown), BUG-1215 (dashboard sessions have no persisted permission-audit trail - `configure_global_logger()` never called at dashboard startup, so records are generated and dropped).

lagrange-framework/BUG-33 - the Calendar target-vs-event fix this map needed - is still `ready_to_reconcile` upstream and needs a `bin/vendor-webui-components` re-vendor to arrive here. Operator action, not automatic.