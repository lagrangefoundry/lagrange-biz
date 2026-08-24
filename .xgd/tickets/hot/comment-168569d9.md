---
uid: comment-168569d9
id: COMMENT-26
type: comment
title: Comment on goal GOAL-42
created_by: xgd
created_at: '2026-08-24T01:39:44.518164+00:00'
updated_at: '2026-08-24T01:39:44.518164+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-0662ec2b
  kind: note
---

**2026-08-24 - the cluster is nearly cleared. One ticket is the whole remaining blocker, and it is still `draft`.**

Operator: *"I fixed a bunch of bugs in xgd - the workflows test has not completed yet but we are getting there - reconcile seems to not want to dispatch on real projects but we will get there."*

## Cleared since yesterday

Twelve REQ-816 fallout bugs reached `ready_to_reconcile`:

| | | |
|---|---|---|
| BUG-1251 | LATEST short-circuit disabled by overlay mode (47s/185s chat loads) | ready_to_reconcile |
| BUG-1252 | "Unable to find ticket banner" after REQ-816 | ready_to_reconcile |
| BUG-1256 | remove --feature-branches and cross-worktree aggregation | ready_to_reconcile |
| BUG-1257 | Resync SHA remap only checks canonical, misses xgd-working overlay | ready_to_reconcile |
| BUG-1258 | _inline_demotion_sweep bypasses is_branch_worktree() index guard | ready_to_reconcile |
| BUG-1259 | Dashboard IndexPoller conflates primary checkout with canonical | ready_to_reconcile |
| BUG-1261 | 1stcontact dashboard pegs CPU on repeated 30-40s index reloads | ready_to_reconcile |
| BUG-1247, BUG-1249, BUG-1250 | permissions template, panel refresh, feature-branch loss | ready_to_reconcile |
| BUG-1254, BUG-1260, BUG-1262 | test-workflows harness, blueprint spec, disclaimer | ready_to_reconcile |

BUG-1255 (a 9-minute intent-ticket lookup, traced to a lock storm from BUG-1251 pre-fix dashboard process) closed `wont_fix` - it was a symptom of a process still running old code, not a defect.

That is the performance complaint from yesterday substantially answered. The 47-second chat load, the 30-40 second index reloads and the pegged CPU all have fixes sitting at `ready_to_reconcile`.

## BUG-1266 is the reconcile dispatch problem, and its root cause is already confirmed

**`draft`. Severity high. Root cause CONFIRMED and written up. Not started.**

The operator report - reconcile not dispatching on real projects - is fully diagnosed. `xgd revert reconcile <ticket>` runs from xgd-working, which since REQ-816 is in overlay mode, so its status write lands in xgd-working local overlay and never reaches canonical. `xgd revert reconcile` is a one-shot administrative command with no merge-back step.

Verified by reading the two physical files: xgd-working copy of BUNDLE-128 says `ready_to_reconcile` (the operator revert); canonical copy says **`reconciling`**, untouched since before the crash.

The consequence is not local to that bundle. The dispatcher runs against canonical and applies a **cycle-wide gate** (REQ-710): while ANY intent ticket is `reconciling`, no new reconcile is planned or dispatched. Canonical still shows BUNDLE-128 at `reconciling`, so **every reconcile in every project is blocked**, not just that one.

That gate exists for a good reason - it was added to stop the dispatcher orphaning a ticket stuck at `reconciling` with no worktree. It is working exactly as designed, on a stale fact.

**This is the same failure shape as BUG-1251, for the third time:** a mechanism that was correct while xgd-working wrote straight to canonical, now silently wrong because it writes to an overlay. Worth auditing the remaining one-shot administrative commands for the same pattern rather than waiting for each to surface.

I cannot promote it - `ready_to_implement` is the operator transition - so flagging its priority here.

## Still open

- **BUG-1266** - `draft`, above. The blocker.
- **BUG-1248** - `free_coding`. lagrange-framework xgd-working overlay stuck stale.
- **BUG-1245** - `free_coding`. Permissions audit record omits session_role for headless launches.
- **BUG-1263** (`draft`) - Status tab shows dispatcher as dead during slow StatusCache refresh. Note this is cosmetic-looking but is exactly the kind of thing that makes a real dispatcher stall hard to distinguish from a display lag.
- **BUG-1264** (`draft`) - branch-seeding ticket-seed failures warn and continue where they should hard-error. Same class as the silent-partial-snapshot problem REQ-816 exists to fix.
- **BUG-1267** (`draft`, Untitled).

## The index still disagrees with the tickets

Re-verified today: `xgd ticket list --filter status=draft --project xgd` reports BUG-1247, BUG-1249 and BUG-1250 as `draft` and titled "Untitled"; `xgd ticket get` on the same ids returns all three at `ready_to_reconcile` with real titles.

BUG-1252 is fixed, so this is a separate residue - stale index entries rather than a lookup-path defect. It still means **any count taken from `list` is wrong**, which continues to block the burn-down measurement on goal-24b1f233. Not yet ticketed as far as I can see.