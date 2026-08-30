---
uid: comment-d0fc8f20
id: COMMENT-37
type: comment
title: Comment on goal GOAL-68
created_by: xgd
created_at: '2026-08-30T03:00:54.572350+00:00'
updated_at: '2026-08-30T03:00:54.572350+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-24b1f233
  kind: note
---

**2026-08-29 - real movement, and the counts are trustworthy again.**

| Project | Draft bugs | Draft requests | Total | vs 08-23 |
|---|---|---|---|---|
| xgd | **1** | 11 | **12** | was 22 |
| 1stcontact | **0** | 4 | **4** | was 4 |
| lagrange-framework | **0** | 1 | **1** | was 0 |
| lagrange-biz | 0 | 0 | **0** | unchanged |

**17 total, down from 26.** And the `list`/`get` disagreement that made the 08-23 numbers unreliable has gone - spot-checked against direct `get` calls and they now agree, which is the REQ-816 index work settling.

## What moved

- xgd draft bugs **3 to 1**. BUG-1263 and BUG-1264 both cleared; only BUG-1281 remains, still `Untitled`.
- xgd draft requests **13 to 11** - REQ-675 (resync regression tests for CherryPickEngine) and REQ-763 (min_required_version forced-update gate) cleared.
- 1stcontact draft bugs held at **zero**.
- lagrange-framework gained its first draft in a while: REQ-108 (attachment soft-delete and blob garbage collection). One new draft in a week is a healthy rate, not a regression.

## The age tail is the remaining work, and it has not moved

Six of the eleven xgd draft requests predate August: REQ-468, REQ-539, REQ-540 (the Surfaces block, 2026-05-19/20), REQ-583 (05-26), REQ-661 and REQ-663 (06-26). Between three and four months old.

These are the ones I flagged on 08-23 as *decisions never made rather than work in flight*. Nothing has touched them since. They will not clear through ordinary bug-fixing because nobody is going to pick up a May request opportunistically - they need a deliberate pass whose likely output is `abandoned` with a reason for most of them.

That is a twenty-minute job and it would take the xgd draft count from 12 to about 6. Worth doing while the recent fallout is fresh enough that the contrast is obvious: the recent drafts are real work, the May ones are shelf-life.

## Tooling status

xgd/BUG-1185 (`ticket list --project`) and xgd/REQ-811 (the tracker) are both attached as children and both past `ready_to_reconcile`. The measurement problem this goal opened with is solved - these counts came straight out of the fixed command.