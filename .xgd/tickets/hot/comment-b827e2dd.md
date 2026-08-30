---
uid: comment-b827e2dd
id: COMMENT-34
type: comment
title: Comment on goal GOAL-42
created_by: xgd
created_at: '2026-08-30T02:59:52.228599+00:00'
updated_at: '2026-08-30T02:59:52.228599+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-0662ec2b
  kind: note
---

**2026-08-29 - BUNDLE-128 is through, and the week found where reconcile time actually goes.**

Five days since the last pass. Operator: *"I have been busy on other things this week, mostly work has been bug fixes."* Version 0.15.390 to 0.15.404.

## The blockage cleared

**BUNDLE-128 is `free_and_reconciled`** - 27 tickets. That is the bundle whose stale `reconciling` row on canonical was blocking every reconcile in every project (BUG-1266). It did not just get unstuck; it completed.

**BUNDLE-129 is `reconciling` now** - 19 tickets, in flight. The pipeline is moving rather than jammed, which is the first time that has been true since REQ-816 landed.

## What the week actually found: reconcile had an unmeasured ~1.5 hour floor

Four bugs, all `ready_to_reconcile`, and together they are a single story about cherry-pick cost that nobody had instrumented:

- **BUG-1285** (severity high) - *~63 minutes of completely silent time inside every `cherry_pick_next_v2` iteration.* Zero log lines between the last instrumented step and the conflict report. All four attempts observed on BUNDLE-128 took **87-91 minutes end to end regardless of conflict size** - one was a single-file version-bump collision in `__init__.py` whose actual resolution took 69.5 seconds. A fixed 1.5-hour floor holding steady across wildly different conflict complexity means the cost is not in conflict resolution at all.
- **BUG-1276** - the cherry-pick loop recomputes the window and the rogue-commit safety gate **on every commit** instead of once per bundle. The most likely occupant of that silent window.
- **BUG-1291** - `is_applied()` never recognises a skipped merge-commit pick, causing an infinite re-pick livelock.
- **BUG-1287** - invoker now retries on `Connection lost mid-response` rather than failing the run.

The pattern worth keeping: **the fixed floor was the diagnostic.** A cost that does not vary with the work being done is not the work - it is overhead, and it was invisible because nothing logged inside the window. That is the same class of finding as BUG-1251 (47-second chat loads from a permanently-disabled fast path): a system slow in a suspiciously constant way.

Worth naming what this cost before it was found. BUNDLE-128 carried 27 tickets through a loop with a 1.5-hour floor per cherry-pick attempt. The reconcile backlog that built up over the last fortnight was not idleness.

## Draft burn-down inside this cluster

xgd draft bugs went **3 to 1** - only BUG-1281 (still `Untitled`) remains. BUG-1263 and BUG-1264 both cleared. BUG-1264 is the one I flagged on 08-24 as not-to-leave: branch seeding treating ticket-seed failures as best-effort, which reintroduced the silent-partial-snapshot mode REQ-816 exists to remove. Good to see it gone.

Still `free_coding` and unchanged since 08-23: **BUG-1245** (permissions audit record omits `session_role` for headless launches) and **BUG-1248** (lagrange-framework xgd-working overlay stuck stale). BUG-1248 is the only leaf this goal currently offers On Deck - six days in the same state is worth a look, either to finish it or to say it is parked.