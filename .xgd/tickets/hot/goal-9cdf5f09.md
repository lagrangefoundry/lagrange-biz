---
uid: goal-9cdf5f09
id: GOAL-49
type: goal
title: Reusable AI tooling object
created_by: xgd
created_at: '2026-08-08T23:48:08.445713+00:00'
updated_at: '2026-08-09T00:19:10.980208+00:00'
completed_at: null
last_field_updated: body
status: in_progress
fields:
  provenance: product_decision
  children:
  - ticket://lagrangefoundry/lagrange-framework/REQ-73
  - ticket://lagrangefoundry/lagrange-framework/REQ-74
  - ticket://lagrangefoundry/lagrange-framework/REQ-75
  - ticket://lagrangefoundry/lagrange-framework/REQ-76
  - ticket://lagrangefoundry/lagrange-framework/REQ-77
  - ticket://lagrangefoundry/lagrange-framework/DOC-13
---

One configurable, declarative component that every AI toolset is built on - rather than a hand-rolled integration per surface.

The object carries projection, validation, policy gating, structural dispatch, provenance and audit. Toolsets declare an API and a config; the object enforces what a caller may address and how.

**Composition:** DOC-13 (Toolbox API: host tool-registration contract, Python + JS) and DOC-20 (the tooling object design: declared API, config, call types, policy, security frame) are the design; REQ-73 completes DOC-20; REQ-74 builds the object; REQ-75 refactors ai_ticketing onto it as the first consumer, which is what proves the design; REQ-76 refactors ai_knowledge; REQ-77 refactors the built-in filesystem toolset, sequenced last with a decision still pending. REQ-74 through REQ-77 are expected to be built in a single pass on 2026-08-09.

## Who depends on this

**The site builder (goal-1a5a8d2b, target 2026-08-31).** This is the glue the builder needs. The basic chat interfaces exist and much of the site framework exists; what was missing is the tooling that lets an AI actually drive site construction. Work on this object *is* site builder progress, even though no 1stcontact ticket moved on 2026-08-08.

**The goal map (goal-98f48e17).** On 2026-08-08 this assistant could not file a REQ because its type allowlist was fixed at [decision, goal]: creating type request is not enabled for this session. The plumbing already existed - xgd/REQ-750 and lagrange-framework/REQ-67, both free_coded the day before. Only the policy gate was closed and there was nowhere principled to open it. xgd/REQ-762 opened it the same day; the tooling object is what makes that kind of change configuration rather than code. Ensure request and bug are expressible in the policy frame rather than patched in afterwards.

**ai_ticketing, ai_knowledge and the filesystem toolset**, each of which currently re-implements gating by hand. xgd/BUG-982 (unrecognised routing key silently ignored, ticket lands in the wrong project) is precisely the class of defect uniform projection and validation should make impossible.

**Framework work, but not for framework sake.** Framework supplies XGD and 1stcontact; it is not a destination.

See decision-46593d49 for why this was built as a component rather than solved point-wise.