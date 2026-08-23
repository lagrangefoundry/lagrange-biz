---
uid: comment-018e46f0
id: COMMENT-24
type: comment
title: Comment on goal GOAL-50
created_by: xgd
created_at: '2026-08-23T18:37:03.825820+00:00'
updated_at: '2026-08-23T18:37:03.825820+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-959f56f3
  kind: note
---

**2026-08-23 - the roll-up disagreement flagged at closure has resolved itself.**

When this goal was marked `realized` on 08-19 I recorded four children still at `free_coded` - BUG-1142, BUG-1143, BUG-1159 and REQ-801 - stuck because the `move-to-free-coded` ancestor gate would have refused their SHAs while `free-REQ-796` was unmerged, and predicted that re-running the gate would clear them.

All four are now `ready_to_reconcile`. Declared and derived agree. No action needed, recorded so the prediction is closed rather than left hanging.

One piece of permissions work continues to surface, and it belongs to the ordinary bug flow rather than reopening this goal:

- **BUG-1245** (`draft`) - the `claude_permissions_resolved` audit record omits `session_role` for headless launches. Worth noting because the audit trail is the part of this goal that carries the accountability claim, and a record that cannot say which role it describes is weaker evidence than it looks.
- **BUG-1247** (`ready_to_reconcile`) - unquoted YAML `off`/`on` in the permissions template broke freshly-initialised projects. A classic YAML 1.1 boolean coercion, and the kind of thing that only shows up on a fresh init - i.e. exactly what a beta user does first.
- **BUG-1237** (`free_coded`) - cross-project WHERE grant omits other projects primary checkouts.

DOC-981 s8 remains stale on the network item, as flagged on 08-19. Still worth a correction pass whenever the ticketing work settles.