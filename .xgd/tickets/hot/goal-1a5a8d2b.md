---
uid: goal-1a5a8d2b
id: GOAL-47
type: goal
title: Site builder
created_by: xgd
created_at: '2026-08-08T22:53:54.056155+00:00'
updated_at: '2026-08-12T00:05:00.105778+00:00'
completed_at: null
last_field_updated: workstream
status: in_progress
fields:
  provenance: planned
  target_date: '2026-08-31'
  children:
  - ticket://lagrangefoundry/1stcontact/GOAL-16
  - ticket://lagrangefoundry/1stcontact/GOAL-17
  depends_on:
  - goal-9cdf5f09
  workstream: true
---

The chat-driven website builder in 1stcontact: good enough that a class cohort can build real sites on it.

The deadline is external and hard. The class will use another tool if 1stcontact is not ready by the end of August (decision-9d416da1). Target 2026-08-31.

**Composition:** 1stcontact/GOAL-16 (Web editor, in_progress) and 1stcontact/GOAL-17 (Editor chat, concept).

Split out of Class cohort as its own goal so the builder work carries the date visibly rather than inheriting it implicitly from a parent that also contains course material and onboarding.

## Depends on the tooling object

The pieces largely exist: the basic chat interfaces, and a lot of the site framework. What was missing is the glue that lets an AI actually drive site construction - declared tools, projection, validation, policy gating, dispatch. That is the Reusable AI tooling object (goal-9cdf5f09), designed and begun on 2026-08-08.

Recorded as depends_on rather than children deliberately: the tooling object is not part of the site builder, it is a prerequisite that also serves ai_ticketing, ai_knowledge and the goal-map tools. Lateral ordering, not composition.

**This is the first depends_on edge on the map.** Consequence worth noting: under the current readiness rule the site builder is now not-ready until the tooling object is realized. That is arguably the truth - the glue has to exist before the builder can be finished - but discovery work on the builder can and does proceed in parallel, so if it reads wrong on the On deck list, say so and it can come out.

## The long pole

Product discovery, not available time. How long it takes to work out what the builder should be is genuinely unbounded, in the same way that working out what the goal map should be is unbounded. Distinct from a date under time pressure, and it should not be read as a slip risk of the same kind.