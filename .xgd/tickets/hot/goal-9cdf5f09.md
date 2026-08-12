---
uid: goal-9cdf5f09
id: GOAL-49
type: goal
title: Reusable AI tooling object
created_by: xgd
created_at: '2026-08-08T23:48:08.445713+00:00'
updated_at: '2026-08-12T00:04:42.154600+00:00'
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

The Toolbox carries projection, validation, capability groups, scope gating, provenance and audit. Toolsets declare an API and a config; the object enforces what a caller may address and how.

**Composition:** DOC-13 (Toolbox API: host tool-registration contract, Python + JS) and DOC-20 (the design: declared API, config, call types, policy, security frame). REQ-73 completed DOC-20 (legacy_done). REQ-74 built the Toolbox (free_coded). REQ-75 bridges to the framework ticket implementation, REQ-76 refactors ai_knowledge, REQ-77 refactors the built-in filesystem toolset onto FilesystemToolbox - resequenced first.

## Who depends on this

**XGD access control (goal-959f56f3), via adoption.** xgd/REQ-781 imports this backend into XGD so Claude invocation runs through a single choke point with a declared permissions schema, rather than permission control being retrofitted onto XGD legacy code. This is the route by which the Toolbox reaches XGD - not REQ-75, which bridges to the framework ticket implementation that XGD does not use.

**The site builder (goal-1a5a8d2b, target 2026-08-31).** The glue that lets an AI drive site construction. The chat interfaces exist and much of the site framework exists; this was the missing piece. Work here is site builder progress even when no 1stcontact ticket moves.

**The goal map (goal-98f48e17).** On 2026-08-08 this assistant could not file a REQ - "creating type request is not enabled for this session". The plumbing existed (xgd/REQ-750, lagrange-framework/REQ-67, both free_coded the day before); only the policy gate was closed, with nowhere principled to open it. xgd/REQ-762 opened it the same day.

**Validation defects that uniform projection should make impossible** - lagrange-framework/BUG-20, and its host-side instances xgd/BUG-982 and xgd/BUG-996, where unrecognised argument keys are silently ignored and success is returned. These reach a fix through XGD adopting the Toolbox (REQ-781).

**Framework work, but not for framework sake.** Framework supplies XGD and 1stcontact; it is not a destination.

See decision-46593d49 for why this was built as a component rather than solved point-wise.