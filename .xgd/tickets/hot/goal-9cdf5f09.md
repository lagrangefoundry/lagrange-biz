---
uid: goal-9cdf5f09
id: GOAL-49
type: goal
title: Reusable AI tooling object
created_by: xgd
created_at: '2026-08-08T23:48:08.445713+00:00'
updated_at: '2026-08-08T23:48:08.445713+00:00'
completed_at: null
last_field_updated: created_at
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

**Composition:** DOC-13 (Toolbox API: host tool-registration contract, Python + JS) and DOC-20 (the tooling object design: declared API, config, call types, policy, security frame) are the design; REQ-73 completes DOC-20; REQ-74 builds the object; REQ-75 refactors ai_ticketing onto it as the first consumer, which is what proves the design; REQ-76 refactors ai_knowledge; REQ-77 refactors the built-in filesystem toolset, sequenced last with a decision still pending.

**Framework work, but not for framework sake.** Framework supplies XGD and 1stcontact; it is not a destination. This is here because every AI surface the operator runs - the goal map, ai_ticketing, ai_knowledge, the filesystem toolset - currently re-implements gating by hand.

**A live instance of the cost of not having it.** On 2026-08-08 the goal-map assistant could not file a REQ because its type allowlist is fixed at [decision, goal] for the session: creating type request is not enabled for this session. The plumbing for cross-project filing already existed - xgd/REQ-750 (xgd ticket create --project) and lagrange-framework/REQ-67 (xgd-cli access kind: create() for cross-project filing), both free_coded on 2026-08-07. Only the policy gate was closed, and there was no principled place to open it. That gate is exactly what REQ-73 and REQ-74 are designing. Ensure request and bug are expressible in the policy frame rather than patched in afterwards.

See decision-af75b21f for why this was built as a component rather than solved point-wise.