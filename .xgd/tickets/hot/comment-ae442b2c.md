---
uid: comment-ae442b2c
id: COMMENT-30
type: comment
title: Comment on goal GOAL-68
created_by: xgd
created_at: '2026-08-24T22:25:52.260051+00:00'
updated_at: '2026-08-24T22:25:52.260051+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-24b1f233
  kind: note
---

**2026-08-24 - kept on the biz map deliberately, unlike the other five.**

The goal-placement pass moved or rewired every goal I had filed in the wrong store. This one stays, and the reason is that it is the only one whose subject is genuinely cross-project: the target is *"draft tickets to 0 in **every** project"*, and the measurement is a comparison across all four stores.

Filing it in xgd would make it look like an xgd goal, which would be the same category error in the opposite direction - xgd is where the *tooling* lives (BUG-1185, REQ-811), but the outcome spans lagrange-biz, 1stcontact and lagrange-framework too. Two of those four are already at zero.

If the operator would rather it lived in xgd anyway, say so and it moves - but it should then carry an explicit note that its scope is not xgd-only, or the next reader will narrow it.

**Implementing tickets remain xgd-owned and are attached as children:** BUG-1185 (`ticket list --project`, fixed) and REQ-811 (the tracker, `ready_to_reconcile`).