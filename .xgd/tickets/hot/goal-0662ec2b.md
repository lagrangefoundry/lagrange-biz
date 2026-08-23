---
uid: goal-0662ec2b
id: GOAL-42
type: goal
title: Ticketing store bugs
created_by: xgd
created_at: '2026-08-08T16:30:48.190077+00:00'
updated_at: '2026-08-23T18:36:26.328225+00:00'
completed_at: null
last_field_updated: workstream
status: in_progress
fields:
  provenance: bug
  children:
  - ticket://lagrangefoundry/xgd/REQ-816
  - ticket://lagrangefoundry/xgd/DOC-986
  - ticket://lagrangefoundry/xgd/BUG-1246
  - ticket://lagrangefoundry/xgd/BUG-1247
  - ticket://lagrangefoundry/xgd/BUG-1248
  - ticket://lagrangefoundry/xgd/BUG-1249
  - ticket://lagrangefoundry/xgd/BUG-1250
  - ticket://lagrangefoundry/xgd/BUG-1251
  - ticket://lagrangefoundry/xgd/BUG-1252
  - ticket://lagrangefoundry/xgd/BUG-1253
  - ticket://lagrangefoundry/xgd/BUG-1213
  - ticket://lagrangefoundry/xgd/BUG-1185
  - ticket://lagrangefoundry/xgd/BUG-944
  - ticket://lagrangefoundry/xgd/BUG-959
  - ticket://lagrangefoundry/xgd/BUG-970
  - ticket://lagrangefoundry/xgd/BUG-982
  - ticket://lagrangefoundry/xgd/BUG-993
  workstream: true
---

Bugs in the ticket store itself - routing, overlays, index bookkeeping, promotion.

Originally a fifth cluster split out of the four workflow buckets on 2026-08-07, because the root cause was the store rather than any one workflow: these bugs crashed whichever workflow happened to touch a promotion first, which makes them look like reconcile bugs and misattributes the fix. That reasoning has held.

## Marked a workstream 2026-08-23

Operator: *"Our latest set of changes to the ticket system are still working through - we have all kinds of mostly performance issues. I think I need to keep pushing on this until the system is stable again."*

This is the current primary thread. It was not on the ready frontier before today because the goal body still described 2026-08-07.

## REQ-816 - the change that is working through

**Ticketing: overlay-everywhere ticket store routing and branch-cut matrix/intent seeding (REQ-630 successor).** `free_coded`, 10 commits, version 0.15.354. Design in DOC-986.

What it did, in one line: **removed the special case that made `xgd-working` route straight to canonical, giving it an ordinary local overlay like every other worktree.** Also retired `feature_branches=True` cross-worktree aggregation entirely, removed the `xgd-ticket-recent` git merge driver, and fixed capability-matrix tickets not being pinned to the code version their branch was cut from.

It folded in four bugs, all closed `wont_fix` as the same mechanism - a branch local ticket store being a partial, unpinned snapshot: BUG-1092, BUG-1240 (a ~26h regression run and six wasted fix-loop iterations), BUG-1089 (a stale-vs-current mixed read that destructively overwrote a reconciled story body on `main`), and BUG-1230 (a live stuck-reconcile incident).

Deliberately one ticket rather than several - the pieces are mutually load-bearing and partial delivery has no value.

## The fallout, and why it is the shape it is

Every performance problem in this cluster traces to the same thing: **the special case that was removed was load-bearing for a fast path.**

The clearest instance is BUG-1251 (`ready_to_reconcile`, severity high). Loading a ticket chat transcript in the dashboard took **47 seconds, and in one case 185 seconds**. Root cause: REQ-609 added a LATEST-query short-circuit that answers `_latest: True` in O(1) from the hot-tier index; BUG-931 later guarded it with `and not _overlay_sources`, because the short-circuit did not consult branch-local overlays. That guard was safe precisely *because* `xgd-working` had no overlay. Post-REQ-816 it has one - so `_overlay_sources` is non-empty on every ordinary dashboard read, and the fast path is permanently disabled for everything.

A guard written for the exotic case became the common case. That is the pattern to expect from the rest of this cluster, and it is a good reason to keep pushing rather than to patch symptom by symptom.

| Ticket | | Status |
|---|---|---|
| BUG-1251 | LATEST short-circuit disabled by overlay mode; chat loads pay a full main-index rebuild | ready_to_reconcile |
| BUG-1249 | Dashboard IndexPoller never broadcasts panel refresh for xgd-working own local writes | ready_to_reconcile |
| BUG-1247 | Permissions template: unquoted YAML off/on breaks freshly-init projects | ready_to_reconcile |
| BUG-1246 | Dispatcher tests: stale single-checkout fixture no longer satisfies resolve_main_xgd_dir | free_coded |
| BUG-1250 | get_ticket_feature_branches loses tickets on xgd-working index-load failure | free_coded |
| BUG-1253 | test-workflows --feature-branches lookup stuck on stale xgd-working index | free_coded |
| BUG-1248 | lagrange-framework xgd-working local overlay stuck stale | **free_coding** |
| BUG-1252 | "Unable to find ticket banner" after REQ-816 | **draft** |
| BUG-1213 | `xgd ticket history --follow` pathologically slow on large repos | ready_to_reconcile |
| BUG-1185 | `xgd ticket list --project` crashed with AttributeError: list_refs | ready_to_reconcile |

## Reproduced from outside, 2026-08-23

Two observations from this goal map session, offered as evidence rather than as new tickets:

1. **BUG-1252 is real and reproducible from a sibling project.** `xgd ticket get --project xgd --id BUG-1240` returns not-found, while `xgd ticket get --project xgd bug-0617965f` - the same ticket by uid - returns it. The human-id path is resolving against something the uid path is not.
2. **`list` and `get` currently disagree about status.** `xgd ticket list --filter status=draft --project xgd` reports BUG-1246 through BUG-1250 as `draft`; `xgd ticket get` on the same ids reports `ready_to_reconcile`, `free_coded` and `free_coding`. Several also render as "Untitled" in `list` while having real titles via `get`. The index and the ticket disagree, and `get` is the one matching the work actually done.

That second one has a consequence beyond this goal: any count taken from `list` right now is wrong, which lands directly on goal-24b1f233 (draft backlog burn-down) and on REQ-811, the tracker built to produce those counts.

## Historical - the 2026-08-06/07 cluster

BUG-944 (`git add --sparse` cannot stage an old-path deletion for cold-to-hot promotion on EXCLUDE branches), BUG-959 (a rejected `update()` orphans the promotion and crashes generic auto_commit), BUG-970 (stray `hot/index.json` and `search/` cache left in xgd-working). All three trace to the REQ-722 move that made main the canonical ticket store and left xgd-working sparse-excluded - which is the same architectural seam REQ-816 has now removed outright.