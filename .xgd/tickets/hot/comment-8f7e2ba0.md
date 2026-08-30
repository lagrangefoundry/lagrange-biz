---
uid: comment-8f7e2ba0
id: COMMENT-36
type: comment
title: Comment on goal GOAL-62
created_by: xgd
created_at: '2026-08-30T03:00:35.390207+00:00'
updated_at: '2026-08-30T03:00:35.390207+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-74b33543
  kind: note
---

**2026-08-29 - priority 1 is scoped and filed, and it turned up something that changes the estimate.**

**1stcontact/REQ-158** - *The system KB in the Worker: bundle-resident index, AI binding, knowledge surface on the builder toolbox* - filed 2026-08-28. `draft`, priority high, 8 story points. This is the operator first named priority (KMS running on 1c) turned into a scoped request.

It is well-shaped and honest about being small: *"This is a wiring ticket, not a design one. The seam already exists and is deliberately shaped for exactly this."* `createL1ToolboxCore` already accepts a `knowledgeSurface`; the node-side `createL1Toolbox` already builds one; `openKnowledgeRuntime()` already opens a runtime from disk. Only `apps/control-app/src/ai.ts` passes no knowledge at all, so the surface defaults to `null`. **The CLI path works and the Worker path was never connected.**

## The finding worth surfacing

> *"The corpus has never actually been built. `kb/system/` contains 33 exported markdown documents and nothing else - no `index/`, no `chunks/`, no awareness-map document. Only `1c kb export` has ever run, so the embedder, describer and awareness passes are unexercised against the current corpus."*

That is a bigger statement than the ticket it sits in. The framework components (lagrange-framework REQ-99, REQ-100, REQ-101 - query side, ai_knowledge bridge, awareness build) have been `ready_to_reconcile` since 2026-08-19, and the note on this goal from 08-24 said the bottleneck was adoption rather than construction. It is more specific than that: **the build passes have never been run end to end on a real corpus.** Export has; embed, describe and awareness have not.

So the first genuine test of the knowledge components is not the Worker wiring - it is `1c kb build` completing against 33 real documents. REQ-158 names that as a prerequisite rather than part of the ticket, which is correct scoping, but it means the 8 points measure the wiring and not the risk.

This matters for **priority 3 (KMS in xgd)** too. xgd/REQ-775 replaces the static priming assembler with KB-based priming and has no cheap rollback. Whatever `1c kb build` reveals about the build passes is evidence xgd gets for free by going second - which is the argument for the ordering reversal noted on 08-24, now with a concrete payoff rather than a general one.

## Still open from 08-24

The **ticket backing** ambiguity is unresolved. The operator phrasing was *"get the KMS system with ticket backing running on 1c"*; 1c/GOAL-34 commits to D1 for structured records and R2 for payloads per DOC-5. REQ-158 describes a **bundle-resident index** shipped as a release artefact - which is a third shape again, and arguably the most concrete of the three. Worth reconciling those three descriptions before GOAL-34 is implemented, since 1c/GOAL-43 (the backend data model question) is the recorded blocker and this is most of its content.