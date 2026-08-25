---
uid: comment-9552acc2
id: COMMENT-32
type: comment
title: Comment on goal GOAL-62
created_by: xgd
created_at: '2026-08-25T05:39:17.782343+00:00'
updated_at: '2026-08-25T05:39:17.782343+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-74b33543
  kind: note
---

**2026-08-24 evening - the operator named the next four priorities, and three of them are this.**

> (1) Get the KMS system **with ticket backing** running on 1c
> (2) Get upload working on 1c to add to the project KB
> (3) Get the KMS running in xgd
> (4) Create some new docs on how xgd is used today

Recorded here because it is a cross-project ordering statement and lives nowhere else. Every one of the four already has a goal - which is new. A week ago two of them had none.

| Priority | Owner | State |
|---|---|---|
| 1 - KMS on 1c | 1stcontact/GOAL-33 over GOAL-34 (KM core system) | `concept` |
| 2 - upload into project KB | 1stcontact/GOAL-37 over GOAL-38, GOAL-39 | `concept` |
| 3 - KMS in xgd | xgd/GOAL-8, cutover is xgd/REQ-775 | REQ-775 `draft` |
| 4 - docs on how xgd is used today | xgd/GOAL-12 | `aspiration` |

## Note the ordering, because it is not the obvious one

1c gets the knowledge system **before** xgd does. That inverts what this goal has assumed since 08-13, where KM was framed as the completion of the xgd backend refactor and 1c was not in the picture.

It is defensible and probably right: 1c/GOAL-34 is adoption-and-wiring of components that already exist, while xgd/REQ-775 is a **replacement** that deletes the static priming assembler with no cheap rollback. Doing the additive integration first buys evidence that the components work in a real app before betting the priming path of the system that runs everything on them.

But it is a reversal, and the reason should be stated by the operator rather than inferred by me.

## "With ticket backing" is new, and may conflict with what is written down

Priority 1 says the KMS on 1c should have **ticket backing**. That phrase appears nowhere in the 1c goals filed earlier today. 1c/GOAL-34 states a different architecture: *"Architectural home per DOC-5: D1 for structured records, R2 for larger payloads and archived content."*

Those may be compatible - ticket-backed could mean KB entries are ticket records (as xgd docs already are), stored in D1 underneath. Or it may be a genuine change of direction toward the ticketing store as the KB substrate. **The two readings imply different data models**, and 1c/GOAL-43 (what the backend data model really looks like) is already the open question blocking GOAL-34.

Flagged rather than resolved - I have added a note to 1c/GOAL-34 so whoever picks it up sees the ambiguity before choosing.

## What has not changed

The framework components are done and waiting: lagrange-framework REQ-99, REQ-100, REQ-101 all `ready_to_reconcile`. Three consumers, one build, none of them reimplementing. The bottleneck is adoption, not construction.