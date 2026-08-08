---
uid: goal-181f56fc
id: GOAL-40
type: goal
title: Development bugs
created_by: xgd
created_at: '2026-08-08T16:30:23.416446+00:00'
updated_at: '2026-08-08T16:30:23.416446+00:00'
completed_at: null
last_field_updated: created_at
status: in_progress
fields:
  provenance: bug
  children:
  - ticket://lagrangefoundry/xgd/BUG-934
  - ticket://lagrangefoundry/xgd/BUG-938
  - ticket://lagrangefoundry/xgd/BUG-940
  - ticket://lagrangefoundry/xgd/BUG-943
  - ticket://lagrangefoundry/xgd/BUG-946
---

Bugs in the develop workflow and its dispatcher - the loop that takes a ticket through TDD to free-coded - worked on 2026-08-06.

Dispatcher and worktree provisioning failed hard: BUG-938 (lagrange-framework fully blocked - main pnpm lockfile/manifest mismatch failed all worktree provisioning) and BUG-943 (a 1stcontact zombie dispatcher process, 2+ days stale, recreated a duplicate bundle and never loaded the BUG-936 fix).

The fix loop itself was masking failures: BUG-934 (test_fix_planner emits an invalid test_scope for lint/build-only batches, hiding real failures behind a phantom preflight check) and BUG-946 (quality_check leaf workflow crashes xgd develop through the BUG-907 materialization repair gap).

BUG-940 is test-harness containment: xgd init and dashboard start were hijacking the operator browser and machine registry during test runs.

BUG-943 is the one worth remembering - a stale process silently running old code is the failure mode that makes every other fix look like it did not work.