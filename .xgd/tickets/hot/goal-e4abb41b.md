---
uid: goal-e4abb41b
id: GOAL-58
type: goal
title: 'Regression lifecycle: event-driven, not timed'
created_by: xgd
created_at: '2026-08-12T00:15:04.654659+00:00'
updated_at: '2026-08-16T01:12:43.773110+00:00'
completed_at: null
last_field_updated: status
status: in_progress
fields:
  provenance: planned
  children:
  - ticket://lagrangefoundry/xgd/REQ-797
  workstream: false
---

Regression starts the way every other workflow starts, rather than on a timer.

Operator description on 2026-08-11: a small change to how regression begins, to make it like the other flows and not timed.

Small in implementation, useful out of proportion to its size. A timed trigger means regression health is a function of whether the clock fired rather than whether the work was ready, and it makes "did regression run" a question you have to go and answer. Regression bugs (goal-215dd333) is the one bug goal on this map that is still **empty** - no failure in five days of heavy bug filing was attributable to the regression workflow, and it has never been clear whether that means healthy or unexercised. A timed trigger is a plausible reason it would be under-exercised without anyone noticing.

This matters more than usual right now: there is substantial capability-matrix refactor work landing on the regression run, and xgd/GOAL-3 states that a green end-to-end regression run is a precondition for trusting any matrix audit.

No tickets yet.