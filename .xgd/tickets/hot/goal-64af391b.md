---
uid: goal-64af391b
id: GOAL-54
type: goal
title: Ticket state transitions are safe and legible
created_by: xgd
created_at: '2026-08-12T00:14:36.026817+00:00'
updated_at: '2026-08-12T00:14:36.026817+00:00'
completed_at: null
last_field_updated: created_at
status: concept
fields:
  provenance: user_feedback
  children: []
  workstream: false
---

Ticket state transitions are constrained, so neither a user nor an AI can put a ticket into a state that breaks the workflow.

Operator assessment on 2026-08-11: "it is a bit of a wild west right now and Claude is getting confused putting tickets into dangerous states".

**Two distinct problems, and the second is the reason this is urgent.**

The correctness problem is that transitions are under-constrained and an AI can select an invalid one. The operator can absorb this - it is recognisable and repairable if you know the state machine.

The readiness problem is that a newcomer cannot. They will neither notice the ticket is in a dangerous state nor know how to get it out, and their first encounter with the workflow will be it silently misbehaving. That converts a tolerable internal quirk into a first-session failure.

This is the same shape as REQ-779 (replace status-advance buttons with Develop / Ready to reconcile): the state machine is legible to the person who wrote it and opaque to everyone else. REQ-779 fixed the naming; this fixes what the transitions actually permit.

No tickets yet.