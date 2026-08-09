---
uid: goal-d5e96abe
id: GOAL-48
type: goal
title: XGD packaging v1 - install tool
created_by: xgd
created_at: '2026-08-08T22:54:00.879209+00:00'
updated_at: '2026-08-09T00:03:08.176778+00:00'
completed_at: null
last_field_updated: status
status: in_progress
fields:
  provenance: planned
  target_date: '2026-08-20'
  children:
  - ticket://lagrangefoundry/xgd/GOAL-2
  - ticket://lagrangefoundry/xgd/REQ-754
  - ticket://lagrangefoundry/xgd/REQ-755
  - ticket://lagrangefoundry/xgd/REQ-756
---

An install path that a first-time user can walk through, end to end, without the author sitting next to them.

**Hard short-term deadline.** The n=1 external user - the operator son, on summer break - cannot be onboarded without it. Target 2026-08-20, matching goal-1789a4b5. The window expires when the summer does.

## State as of 2026-08-08 evening: nearly finished

- xgd/REQ-759 - install/install.sh bootstrap installer plus documented install command - ready_to_reconcile, 16:45.
- xgd/REQ-761 - serve install.sh at xgd.dev/install/install.sh via Cloudflare - free_coded, 16:49.
- xgd/REQ-755 - ./bin/build release-packaging script - ready_to_reconcile, 13:49.
- xgd/REQ-756 - ./bin/deploy release-publishing script - ready_to_reconcile, 14:00.
- xgd/REQ-763 - min_required_version forced-update gate at CLI invocation and dispatcher dispatch checkpoints - draft.
- xgd/REQ-754 - xgd update command - draft.
- xgd/GOAL-2 - Packaging with an update path - planned.

The installer exists and is served. What remains is the update path: the xgd update command and the forced-update gate.

## History

This work was scattered until 2026-08-08 - three drafts filed under XGD Remove friction with no owner drawing them together, and nothing recording that an install tool sat on the critical path for a dated commitment. Consolidated here on that basis.

State moved from planned to in_progress on 2026-08-08 to match reality: four of seven children are free_coded or ready_to_reconcile.