---
uid: goal-0662ec2b
id: GOAL-42
type: goal
title: Ticketing store bugs
created_by: xgd
created_at: '2026-08-08T16:30:48.190077+00:00'
updated_at: '2026-08-09T18:58:20.831168+00:00'
completed_at: null
last_field_updated: children
status: in_progress
fields:
  provenance: bug
  children:
  - ticket://lagrangefoundry/xgd/BUG-944
  - ticket://lagrangefoundry/xgd/BUG-959
  - ticket://lagrangefoundry/xgd/BUG-970
  - ticket://lagrangefoundry/xgd/BUG-982
  - ticket://lagrangefoundry/xgd/BUG-993
---

Bugs in the ticket store itself - sparse checkout, cold/hot promotion, index bookkeeping - worked on 2026-08-06 and 2026-08-07.

A fifth cluster, not among the four workflow buckets originally asked for. Split out rather than folded into reconcile or resync because the root cause is the store, not the workflow: these bugs crashed whichever workflow happened to touch a promotion first, which makes them look like reconcile bugs and misattributes the fix.

- BUG-944 - git add --sparse cannot stage an old-path deletion for cold-to-hot promotion or archive on TicketPolicy.EXCLUDE branches.
- BUG-959 - a rejected update() orphans the cold-to-hot promotion and crashes generic auto_commit on EXCLUDE worktrees.
- BUG-970 - stray hot/index.json and search/ cache left in xgd-working.

All three trace to the REQ-722 move that made main the canonical ticket store and left xgd-working sparse-excluded.

Just outside the window and not listed as children: BUG-931 (branch-worktree list() bypasses the canonical index, forcing a full-store scan per query) and BUG-932 (move-to-free-coded superset gate keeps dangling SHAs forever), both opened late on 2026-08-05. Say the word and I will pull them in.