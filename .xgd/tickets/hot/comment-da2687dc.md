---
uid: comment-da2687dc
id: COMMENT-29
type: comment
title: Comment on goal GOAL-45
created_by: xgd
created_at: '2026-08-24T19:05:50.859225+00:00'
updated_at: '2026-08-24T19:05:50.859225+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-98f48e17
  kind: note
---

**2026-08-24 - goal placement corrected, and it has already produced five duplicate pairs.**

Operator: *"When you add goals you should add them to the project that they are associated with unless they are truly business level goals that live here."*

Accepted, and recorded as standing practice. I had been creating everything locally regardless of owner.

## Goals I created in the wrong store

| Local goal | Belongs in |
|---|---|
| goal-aa268eb1 - XGD documentation a beta user can learn from | xgd |
| goal-e4c8a6ed - 1stcontact: email capture, user portal and CRM Lite | 1stcontact |
| goal-5d987c56 - Capability matrix is trustworthy | xgd - **and duplicates xgd/GOAL-3, which already existed** |
| goal-24b1f233 - Draft backlog burned down to zero, in every project | genuinely cross-project; needs an operator call |

The capability-matrix one is the clearest illustration of the cost: I created it on 08-20 recording that the matrix had *"no goal anywhere on the map"*. That was true of the biz map and false of xgd, where GOAL-3 ("Capability matrix verified working as intended") had existed since 2026-08-06. The rule would have caught it.

## Five duplicate pairs now exist

The operator filed four new goals in xgd on 08-24, all well-evidenced with `implemented_by` and `context_refs` populated. They overlap goals already on this map:

| xgd goal | Local goal |
|---|---|
| GOAL-8 Knowledge management introduction | goal-74b33543 Knowledge management in XGD sessions |
| GOAL-9 Design tab creation | goal-85b52724 Design tab: consolidate Chat and Docs |
| GOAL-10 Chat update | goal-c54b83e0 New chat implementation |
| GOAL-3 Capability matrix verified working as intended | goal-5d987c56 Capability matrix is trustworthy |
| GOAL-11 Beta ready | goal-af871b76 XGD closed beta |

The xgd copies are better sourced - GOAL-10 already carries REQ-741 at `free_and_reconciled` and REQ-794/795 at `ready_to_reconcile`, which the local copy does not know.

**Proposed resolution, not yet applied:** for the first four, keep the xgd goal as the owner and reduce the local goal to a `ticket://` child reference, so the biz map composes from it rather than shadowing it. The fifth is different and should stay split - xgd/GOAL-11 "Beta ready" is the engineering release gate (regression green, packaging), while goal-af871b76 "XGD closed beta" is the business milestone (cohort recruited, onboarding, support loop). Those are genuinely two things; they just need to say so, with the xgd goal as a child of the business one.

Holding off on executing this - it is a restructure of five goals and the operator has a short day. Say the word and it is one pass.