---
uid: comment-12b9206a
id: COMMENT-23
type: comment
title: Comment on goal GOAL-68
created_by: xgd
created_at: '2026-08-23T18:36:48.981143+00:00'
updated_at: '2026-08-23T18:36:48.981143+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-24b1f233
  kind: note
---

**2026-08-23 - the tooling landed, and it immediately showed why the numbers cannot be trusted yet.**

Both blockers cleared since this goal was created on 08-19:

- **xgd/BUG-1185** (`xgd ticket list --project` crashed with `AttributeError: list_refs`) - now `ready_to_reconcile` and **working**. Verified live from lagrange-biz.
- **xgd/REQ-811** (the backlog tracker) - `ready_to_reconcile`.

So for the first time there are real cross-project counts rather than probe-derived floors.

## First measurement, 2026-08-23

| Project | Draft bugs | Draft requests | Total |
|---|---|---|---|
| xgd | 10 | 12 | **22** |
| 1stcontact | 0 | 4 | **4** |
| lagrange-framework | 0 | 0 | **0** |
| lagrange-biz | 0 | 0 | **0** |

Two of four projects are at the floor. lagrange-framework was at zero without anyone aiming at it.

## The number is wrong, and knowing why matters more than the number

`list` and `get` currently disagree. `list --filter status=draft --project xgd` returns BUG-1246, 1247, 1248, 1249 and 1250 as `draft`; `xgd ticket get` on those same ids returns `ready_to_reconcile`, `ready_to_reconcile`, `free_coding`, `ready_to_reconcile` and `free_coded`. Five of the ten "draft" bugs are not drafts. Several also render as "Untitled" in `list` while having real titles via `get`.

This is REQ-816 fallout - the index and the ticket disagree while overlay routing settles (see goal-0662ec2b, and BUG-1252). **The real xgd draft count is meaningfully lower than 22.**

## What this changes about the goal

Nothing about the intent, one thing about sequencing: **do not start burning down from a `list`-derived worklist until the ticketing cluster stabilises.** Working from a stale index means re-triaging tickets that are already done, which is the same wasted motion BUG-1240 recorded (a 26-hour regression run and six fix-loop iterations spent on a partial snapshot).

It also validates the hazard written into REQ-811: that ticket reports and ranks, and must never bulk-close. A bulk-close pass run against today index would have closed five tickets that are actually in flight.

## Oldest drafts, which is the more useful signal

The age tail in xgd is long and predates all of this: REQ-468, REQ-539, REQ-540 (all 2026-05-19/20, the Surfaces block), REQ-583 (05-26), REQ-661 and REQ-663 (06-26), REQ-675 (07-09), BUG-873 (07-27). Eight items older than four weeks.

Worth a separate call from the recent fallout: those are not work in flight, they are decisions never made. Burning them down probably means deciding to abandon most of them, not implementing them - and `abandoned` with a reason is a perfectly good outcome that this goal should count as progress.