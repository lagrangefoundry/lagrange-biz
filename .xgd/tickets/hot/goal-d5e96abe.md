---
uid: goal-d5e96abe
id: GOAL-48
type: goal
title: XGD packaging v1 - install tool
created_by: xgd
created_at: '2026-08-08T22:54:00.879209+00:00'
updated_at: '2026-08-08T22:54:00.879209+00:00'
completed_at: null
last_field_updated: created_at
status: planned
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

**This has a hard short-term deadline and it was a gap in the planning exercise.** The n=1 external user - the operator son, on summer break - cannot be onboarded without it. Target 2026-08-20, matching goal-1789a4b5. The window expires when the summer does; it is not recoverable.

Until now this work was scattered: three drafts filed under XGD Remove friction (REQ-754 xgd update, REQ-755 ./bin/build release-packaging, REQ-756 ./bin/deploy release-publishing) plus xgd/GOAL-2 (Packaging with an update path, planned) with no owner drawing them together. Nothing was tracking that an install tool was on the critical path for a dated commitment. That is exactly the failure this map exists to catch.

The three REQs have been moved here from Remove friction; that goal is for ongoing ergonomics, not for a dated deliverable.

Note the ordering this implies: the install walkthrough is the first thing an external user touches, so it gates the n=1 onboarding rather than running alongside it.