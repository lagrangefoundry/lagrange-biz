---
uid: goal-ed2e16eb
id: GOAL-64
type: goal
title: Forced update path
created_by: xgd
created_at: '2026-08-16T01:12:10.431216+00:00'
updated_at: '2026-08-16T01:12:10.431216+00:00'
completed_at: null
last_field_updated: created_at
status: concept
fields:
  provenance: planned
  children:
  - ticket://lagrangefoundry/xgd/REQ-763
  - ticket://lagrangefoundry/xgd/GOAL-2
  workstream: false
---

Installations can be required to move to a minimum version.

Split out of XGD packaging v1 on 2026-08-15 when v1 was declared complete. The packaging tool ships and updates; **enforcing** an update is a separate capability and was explicitly excluded from v1.

- xgd/REQ-763 - min_required_version forced-update gate at CLI invocation and dispatcher dispatch checkpoints. Still draft, untouched since 2026-08-08.
- xgd/GOAL-2 - Packaging with an update path.

## Why it will matter later rather than now

With one external user, an out-of-date install is a conversation. With a beta cohort it is a support burden and a source of misleading bug reports - xgd/BUG-943 and BUG-933 are both cases where stale code made a working fix look broken, and that was the author own machine.

Not urgent for the 2026-08-24 dinner or the n=1 onboarding. Likely to become urgent the moment more than a handful of people are running XGD independently.