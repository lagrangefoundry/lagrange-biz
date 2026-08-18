---
uid: goal-aa268eb1
id: GOAL-66
type: goal
title: XGD documentation a beta user can learn from
created_by: xgd
created_at: '2026-08-18T20:02:54.654413+00:00'
updated_at: '2026-08-18T20:02:54.654413+00:00'
completed_at: null
last_field_updated: created_at
status: aspiration
fields:
  provenance: planned
  workstream: false
---

Named by the operator on 2026-08-18 as one of three features required for beta launch, alongside quality and install.

**Created because it did not exist.** Quality has goal-5c39075c and xgd/GOAL-1. Install has goal-d5e96abe (realized 08-15) and xgd/GOAL-2. Documentation had no goal, no tickets, and no presence on this map at all - so a beta requirement the operator is actively counting on was invisible to every view. That is the gap this goal closes; the content is still to be scoped.

Filed at `aspiration`: wanted and named, no date set and no work started. It needs a target date to count toward distance, and that is an operator call - the natural candidate is whatever date the closed beta cohort is aimed at, since documentation is the one of the three that gates a stranger rather than a session.

## What it is not

Not the whitepapers (goal-b7d9d110, goal-3f32f3db) - those are positioning for people deciding whether XGD is interesting. This is for someone who has already installed it and needs to do something.

Not the system docs bundled in `xgd_source/system_docs/` - TDD-PROCESS, TEST-STRATEGY, PHILOSOPHY, FREE-CODING. Those are loaded into sessions and written for the AI. A beta user reading them learns how XGD makes an agent behave, not how to run XGD.

## Open scoping questions

None of these are answered anywhere on the map yet:

- **What does a beta user actually need?** Install-to-first-ticket is one document. The workflow model - develop, reconcile, resync, regression, the branch topology - is another, and it is the part that has no shortcut: someone who does not understand reconcile cannot use XGD.
- **Does the knowledge-management work (goal-74b33543) change the answer?** If the shipped KB becomes a first-class artifact (lagrange-framework/REQ-71), then user-facing documentation and session-priming knowledge might be one corpus with two readers rather than two bodies of writing. Worth deciding before writing twice.
- **Who writes it?** This is the only one of the three beta features that XGD building itself does not obviously produce as a by-product.

## Relationship to the other two

The operator sequencing on 2026-08-18 was quality, install, documentation. Install is done. Quality is the long pole and is a root of its own. Documentation is the cheapest of the three to defer and the most expensive to discover missing during an onboarding - the same trade that goal-a1b63a1a records about legibility: packaging without legibility produces a successful install and a confused user.