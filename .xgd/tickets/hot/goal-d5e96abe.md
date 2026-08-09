---
uid: goal-d5e96abe
id: GOAL-48
type: goal
title: XGD packaging v1 - install tool
created_by: xgd
created_at: '2026-08-08T22:54:00.879209+00:00'
updated_at: '2026-08-09T00:02:18.276502+00:00'
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

Hard short-term deadline: the n=1 external user - the operator son, on summer break - cannot be onboarded without it. Target 2026-08-20, matching goal-1789a4b5. The window expires when the summer does.

## Status 2026-08-08 evening - nearly finished

Most of this landed today.

- REQ-755 ./bin/build release-packaging - ready_to_reconcile, 13:49 local
- REQ-756 ./bin/deploy release-publishing - ready_to_reconcile, 14:00 local
- REQ-759 install/install.sh bootstrap installer + documented install command - ready_to_reconcile, 16:45 local
- REQ-761 Serve install.sh at xgd.dev/install/install.sh via Cloudflare - free_coded, 16:49 local
- REQ-763 min_required_version forced-update gate - draft
- REQ-754 xgd update command - draft
- xgd/GOAL-2 Packaging with an update path - planned

The installer exists and is served. What remains is the update path: REQ-754 and REQ-763 together.

## History

This was a gap in the planning exercise. Until 2026-08-08 the work was scattered as three drafts under XGD Remove friction plus xgd/GOAL-2, with nothing recording that an install tool sat on the critical path for a dated commitment.

Moved from planned to in_progress on 2026-08-08 on the evidence above.