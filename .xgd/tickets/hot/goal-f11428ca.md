---
uid: goal-f11428ca
id: GOAL-38
type: goal
title: Reconcile bugs
created_by: xgd
created_at: '2026-08-08T16:30:10.737223+00:00'
updated_at: '2026-08-09T18:58:15.832796+00:00'
completed_at: null
last_field_updated: children
status: in_progress
fields:
  provenance: bug
  children:
  - ticket://lagrangefoundry/xgd/BUG-936
  - ticket://lagrangefoundry/xgd/BUG-941
  - ticket://lagrangefoundry/xgd/BUG-949
  - ticket://lagrangefoundry/xgd/BUG-951
  - ticket://lagrangefoundry/xgd/BUG-952
  - ticket://lagrangefoundry/xgd/BUG-957
  - ticket://lagrangefoundry/xgd/BUG-958
  - ticket://lagrangefoundry/xgd/BUG-961
  - ticket://lagrangefoundry/xgd/BUG-963
  - ticket://lagrangefoundry/xgd/BUG-966
  - ticket://lagrangefoundry/xgd/BUG-986
  - ticket://lagrangefoundry/xgd/BUG-989
  - ticket://lagrangefoundry/xgd/BUG-990
---

Bugs in the reconcile workflow - promoting working bundles into main - worked on 2026-08-06 and 2026-08-07.

The dominant cluster is the cherry-pick engine and its finalize step, which failed in four distinct ways in under 36 hours: BUG-952 (scheduler swallows commit failures, ignores skip_auto_commit), BUG-957 (finalize mis-marks already-continued commits as skipped, abandoned), BUG-958 (finalize hard-fails on an already-cleared cherry-pick, stalling BUNDLE-108), BUG-963 (finalize hard-fails BUG-708 out-of-band --continue after BUG-952 added a returncode check - a fix inducing the next bug).

Concurrency with resync is the second theme: BUG-936 (bundle scope from own commits + planner claim race), BUG-941 (scope SHAs absent during a concurrent resync publish race).

Stale-SHA reporting is the third: BUG-951 and BUG-966 both surface dead fields.commits SHAs as purple has_stale_commits tickets on the dashboard.

BUG-949 is the BUNDLE-103 crash root-cause investigation.

Two of these (BUG-957, BUG-961) closed as abandoned/duplicate - real triage, not lost work.