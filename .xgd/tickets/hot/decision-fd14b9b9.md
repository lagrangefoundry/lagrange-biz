---
uid: decision-fd14b9b9
id: DECISION-8
type: decision
title: Spend a day making XGD legible to a newcomer, prompted by lunch with the n=1
  user
created_by: xgd
created_at: '2026-08-11T23:45:01.260187+00:00'
updated_at: '2026-08-11T23:45:01.260187+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-08-11'
  rationale: 'Lunch with the son who is the n=1 external user made concrete what handing
    over XGD actually involves. Two gaps became obvious and neither was on any list:
    there is no way for a user to see what the AI is permitted to do, and the dashboard
    controls are named for internal state transitions rather than for what the user
    is trying to accomplish. Both are cheap now and expensive after someone has already
    had a confusing first session.'
  caused:
  - goal-a1b63a1a
  - goal-959f56f3
  - goal-adac9e3a
---

## Situation

Lunch with the n=1 external user - the operator son, on summer break - on 2026-08-10. He is the first person who will use XGD without having built it, targeted for 2026-08-20.

Eight requests followed on 2026-08-11, in two clusters.

**Access control transparency**, both filed within a minute at 13:31: REQ-780 (Status tab tile listing Claude session roles and their permissions) and REQ-781 (Claude invocation: single choke point with a permissions schema for lagrangefoundry-ai).

**Interface legibility**, six requests through the day: REQ-777 and REQ-783 (Free Code / Investigate action buttons, single and batch), REQ-779 (replace status-advance buttons with Develop / Ready to reconcile), REQ-778 (batch Free Code with depends_on-aware queueing), REQ-782 (free-coding reminder wording), REQ-784 (button styling consistency).

## What tipped it

Not a plan. A conversation with the actual user, ten days before he is handed the tool.

Two things only become visible when you picture someone else at the keyboard. First, handing someone an agent that can write to your repositories raises a question - what is it allowed to do - that the product could not answer. Second, controls named for internal state transitions are legible to the person who wrote the state machine and opaque to everyone else. REQ-779 is the clearest case: replacing advance the status with Develop names what the user is trying to do rather than what the system does internally.

## The connection worth not losing

The access-control half is not only a usability fix. DOC-4 and DOC-8 both argue that trust in AI-written software must be structural rather than promised. An AI development tool whose own permissions are invisible, and decided in several places, is hard to defend in a document making that argument. REQ-781 chooses a single choke point over scattered call sites for exactly that reason - a choke point can be audited.

There is direct evidence the gap was real: on 2026-08-08 the goal-map assistant was refused a ticket create with "creating type request is not enabled for this session". Correct behaviour, but the operator could neither see what the session was permitted to do nor change it without reading code.

## Cost and shape

Most of 2026-08-11. Not a trade against the dated work: the packaging deliverable was already essentially complete, and this goal sits under XGD closed beta as a precondition for the same 2026-08-20 onboarding. The install tool gets a newcomer to a running system; this decides whether what they find is usable once they arrive.

Six of the eight requests were free_coded or ready_to_reconcile the same day. The two access-control tickets remain draft and are the substantive open work.

## Pattern worth naming

This is the first time a decision on this map was caused by **talking to a user** rather than by hitting a wall in the system. Every prior decision was reactive - a bug pattern, a blocked tool, an expiring window. The n=1 user is nine days from onboarding and is already generating better direction than the backlog was. Whether that becomes a deliberate, repeated loop or stays incidental is an open question.