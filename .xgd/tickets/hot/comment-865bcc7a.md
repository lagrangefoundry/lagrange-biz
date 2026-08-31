---
uid: comment-865bcc7a
id: COMMENT-41
type: comment
title: Comment on goal GOAL-44
created_by: xgd
created_at: '2026-08-31T18:18:17.913246+00:00'
updated_at: '2026-08-31T18:18:17.913246+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-5c39075c
  kind: note
---

**2026-08-31 - named as the core XGD goal, and two critical incidents to go with it.**

Operator: *"On the XGD side the core goal is to stabilize the backend processes."* Recorded here rather than as a new goal - the structure already exists as children of this one (Reconcile bugs, Resync bugs, Development bugs, Regression bugs, Ticketing store bugs), and creating a sixth goal called "stabilize the backend processes" would sit on top of them saying nothing they do not.

What this note adds is the priority statement, which is not derivable from any of them.

## Two critical incidents from yesterday, both `free_coding`

### BUG-1303 - ticket store data loss, 26,017 tickets deleted from main

Severity critical. The canonical store went from ~30,164 ticket files to 4,147.

Root cause confirmed in git history: commit `393dab7309` ("xgd(resync): strip .xgd/tickets... from main snapshot (BUG-904)", authored by xgd-resync, 2026-08-27 22:15) deleted 26,017 files and **is a direct linear ancestor of main HEAD**. The mechanism: `ensure_resync_setup()` strips the ticket tree from a resync scratch worktree and *commits* it - intended as scaffolding local to that branch - then resync CAS-publishes that branch as xgd-working new tip, making the strip a permanent commit. Reconcile then computed its cherry-pick window across it and carried "delete every ticket" onto main.

The arithmetic checks out exactly: 26,017 stripped + 4,147 remaining = 30,164.

Two things worth saying about this beyond the fix:

1. **It is a fix causing the next bug, again.** BUG-904 own stated reasoning was to stop future resyncs replanting main ticket tree into xgd-working. The fix was correct locally and wrong globally, because it did not account for the scratch branch becoming permanent history. Same shape as BUG-1251 (a guard safe only while xgd-working had no overlay) and BUG-1266 (a command correct only while xgd-working wrote to canonical). **Three instances now of the same class: a change that is correct under an assumption REQ-816 quietly removed.** That is worth an audit pass rather than a third individual fix.
2. **The commit is a linear ancestor, so the content is recoverable** from history. Recovery is a separate concern from prevention and both need doing - the ticket does not appear to say which has happened.

### BUG-1299 - BUNDLE-129 livelocked 43 hours, 3,286 identical attempts

Severity and priority both critical. Zero net progress since minute 6 of the run: `remaining_count` went 289 to 288 and never moved again. All 3,286 `cherry_pick_next_v2` attempts failed on the same commit, conflicting on the same file - `xgd_source/dashboard/static/index.html`, **a generated build artifact**. Each cycle ran a full LLM-mediated resolution reporting `success`, then the next iteration hit the identical conflict from scratch. ~33 cumulative hours in resolution alone.

**And here is the part worth celebrating rather than only mourning:** the ticket confirms BUG-1284 and BUG-1285 fixes are working - `cherry_pick_next_v2` median **2.8s, was ~1.5h**; `reconcile_stage_resolution` median **33s, was up to 54min**. Last week performance work delivered.

It also *exposed* this. At 1.5 hours per attempt the livelock would have managed roughly 30 iterations in 43 hours and read as "slow". At 2.8 seconds it managed 3,286 and read as what it is. **Fixing the slowness is what made the loop visible** - the defect was always there, masked by the cost of running it.

That a generated build artifact is in the cherry-pick path at all is the other question this raises, and it is cheaper to answer than the livelock.

## Current state of the front

Four bugs `free_coding` in xgd: BUG-1303, BUG-1299, plus BUG-1245 and BUG-1248 - the latter two unchanged since 2026-08-23, eight days in the same state. Two `draft`. BUNDLE-129 still `reconciling`.