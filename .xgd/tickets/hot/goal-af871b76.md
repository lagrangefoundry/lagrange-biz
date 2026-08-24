---
uid: goal-af871b76
id: GOAL-12
type: goal
title: XGD closed beta
created_by: xgd
created_at: '2026-08-06T21:19:31.925487+00:00'
updated_at: '2026-08-24T22:24:42.985983+00:00'
completed_at: null
last_field_updated: children
status: in_progress
fields:
  provenance: planned
  children:
  - goal-1789a4b5
  - goal-49e8dec2
  - goal-3380b45b
  - goal-cda15c54
  - goal-51d77dcd
  - goal-a1b63a1a
  - ticket://lagrangefoundry/xgd/GOAL-11
  - ticket://lagrangefoundry/xgd/GOAL-3
---

Get other people using xgd, because that is what accelerates learning fastest.

Still the goal. But reframed: beta is a learning instrument, not a launch. Rushing to it would be a mistake, and so would deferring it until quality is done - using the product to build real products is itself valuable, and letting others use it multiplies that.

Starts at n=1 (in-house) and grows to a small cohort in September.

## Deliberately split from xgd/GOAL-11 ("Beta ready")

These are two different things and both are real, so they are kept apart rather than deduplicated:

- **xgd/GOAL-11 - Beta ready.** The **engineering release gate**: the point at which xgd can be handed to a user who is not the operator. Composed of a green end-to-end regression run (xgd/GOAL-1) and packaging with an update path (xgd/GOAL-2). Attached here as a child.
- **This goal - XGD closed beta.** The **business milestone**: people who did not build it are using it. Cohort recruited, entry bar defined, onboarding flow, support and bug-intake loop.

The distinction matters because they can fail independently. A green regression run and a working installer do not produce a beta if nobody has been recruited; a recruited cohort on an unstable release spends an expiring opportunity badly. Collapsing them would hide whichever one is behind.

## What is still only a concept here

The business half is mostly unstarted: beta cohort recruited (3-5 friendlies), beta entry bar defined, support and bug-intake loop, onboarding flow. All at `concept`. **The feature list for beta is answerable; beta as a dated event is not** - there is no target date anywhere on this branch.

The three features the operator named on 2026-08-19 as beta requirements were quality, install and documentation. Install is realized. Quality is a root of its own (goal-5c39075c). Documentation is goal-aa268eb1.