---
uid: goal-1a5a8d2b
id: GOAL-47
type: goal
title: Site builder
created_by: xgd
created_at: '2026-08-08T22:53:54.056155+00:00'
updated_at: '2026-08-16T06:28:20.410872+00:00'
completed_at: null
last_field_updated: depends_on
status: in_progress
fields:
  provenance: planned
  target_date: '2026-08-31'
  children:
  - ticket://lagrangefoundry/1stcontact/GOAL-16
  - ticket://lagrangefoundry/1stcontact/GOAL-17
  - ticket://lagrangefoundry/1stcontact/REQ-135
  - ticket://lagrangefoundry/1stcontact/REQ-136
  - ticket://lagrangefoundry/1stcontact/REQ-137
  - ticket://lagrangefoundry/1stcontact/REQ-138
  - ticket://lagrangefoundry/1stcontact/REQ-139
  - ticket://lagrangefoundry/1stcontact/REQ-140
  depends_on:
  - goal-198516d1
  - goal-9cdf5f09
  workstream: true
---

The chat-driven website builder in 1stcontact: good enough that a class cohort can build real sites on it.

The deadline is external and hard. The class will use another tool if 1stcontact is not ready by the end of August (decision-9d416da1). Target 2026-08-31.

## State as of 2026-08-13

Operator report: the **manual editor is taking shape**, as is the **website creation playbook**. The intent is to build several more websites with it over the coming weekend - which is the real test, since the playbook only proves itself by producing sites.

"We are very close to having an alpha version of the website ready."

**Composition:** 1stcontact/GOAL-16 (Web editor) and 1stcontact/GOAL-17 (Editor chat).

## What follows the alpha

User portal and CRM - 1stcontact/GOAL-10 and GOAL-4, both currently under 1stcontact commercial launch (goal-3d5965fb). The operator sequencing is explicit: alpha website first, then those two. Worth noting they are the first revenue-bearing modules, so the alpha is the gate on commercial work as well as on the class cohort.

## Depends on the Toolbox

The chat interfaces and much of the site framework already existed; what was missing was the glue letting an AI drive site construction. That is goal-9cdf5f09, designed and built 2026-08-08 onward.

Recorded as depends_on rather than children: the Toolbox is a prerequisite that also serves ai_ticketing, ai_knowledge and the goal-map tools. Lateral ordering, not composition.

## The long pole

Product discovery, not available time. How long it takes to work out what the builder should be is genuinely unbounded - the same way that working out what this goal map should be is unbounded. Distinct from a date under time pressure, and it should not be read as a slip risk of the same kind.