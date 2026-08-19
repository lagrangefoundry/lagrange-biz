---
uid: decision-cc46439b
id: DECISION-12
type: decision
title: 'Done means no work left for the operator: ready_to_reconcile counts as realized'
created_by: xgd
created_at: '2026-08-19T23:07:07.580284+00:00'
updated_at: '2026-08-19T23:07:07.580284+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-08-19'
  rationale: The goal map was gating the accumulation register on reconcile completing,
    so a ticket the operator had finished did not count as done until machinery had
    run - often days later, and sometimes not at all while a reconcile backlog built
    up. That put the machine definition of done in charge of the register that exists
    to answer what the operator has achieved. The operator directed the opposite on
    2026-08-15 (goal-d5e96abe was realized on the basis that ready_to_reconcile means
    done) and confirmed it explicitly on 2026-08-19. The accepted cost is that a failed
    reconcile requires un-realizing a goal, which the state ladder already permits
    and treats as rare and worth remarking on.
---

## What was decided

The projection from ticket status to goal state now credits `ready_to_reconcile` and `reconciling` as `realized`, not `in_progress`. Recorded in full on xgd/BUG-1132.

## Why this is a decision and not a bug fix

BUG-1132 is the bug. This is the semantic ruling underneath it, and it is worth its own record for two reasons.

**It defines the boundary of the accumulation register.** DOC-19 and the operator guide build this whole interface on two registers held apart: accumulation, which is monotonic and answers "what do I have now that I did not have in May", and distance, which is volatile. Where accumulation starts counting is the single most consequential semantic in the map. It had never been stated - it had been inherited from wherever the projection happened to draw the line.

**`realized` will jump discontinuously.** It stands at 2 of 67 today. When BUG-1132 lands it will move sharply upward in one step, with no corresponding burst of work. Without this record that reads as data corruption or as the map being gamed. It is neither: it is a backlog being credited under a rule that was already in force by operator direction and simply had no implementation.

## The situation

By 2026-08-19 roughly thirty tickets across three projects sat at `ready_to_reconcile` or beyond - the permissions redesign and the workerd migration had both landed large batches - and every one of them rendered as active work. The operator: *"I am still seeing lots of tickets as in_progress when I know they are not."*

The map was reporting the least useful thing it could: that almost everything was underway and almost nothing was finished, on two of the most productive days on record.

## The alternatives

**Keep `realized` at `free_and_merged`.** Defensible on the machine reading of done - the work is not in main until reconcile says so. Rejected because it makes the operator register a function of machinery, and because a reconcile backlog then reads as an absence of progress rather than as a queue.

**Give `ready_to_reconcile` a distinct visual treatment short of realized** - operator-done, machine-pending. This was the fallback offered in BUG-1132 if the answer came back no. It preserves the distinction without making the claim. Rejected, but it is the right fallback if this is ever revisited.

**Credit it as realized.** Taken.

## What tipped it

The rule was already in force and had been for four days. `goal-d5e96abe` (XGD packaging v1) was moved to `realized` on 2026-08-15 with its own body recording that all five components were at `ready_to_reconcile` or beyond, *"which the operator has directed be treated as done"*. That goal is currently one of only two realized goals on the map. The decision was not new on 08-19; it was already the operating rule everywhere except in code.

That BUG-1132 then filed it as an open question on 08-16 is worth noting on its own - the map had lost the operator ruling the same way it loses everything else, which is the argument for this log existing at all.

## The accepted cost

A reconcile that fails will require un-realizing a goal. Accepted deliberately, and explicitly not to be designed around: no guard, no confirmation step, no intermediate state. The state ladder already permits un-realizing and treats it as rare and important. Making it visible when it happens is the correct behaviour, not a problem to prevent.

## What this does not do

It does not clean up the declared-value drift. Twenty-eight goals currently sit at `in_progress`, and some of those are genuinely stale rather than mis-rendered. Those two are indistinguishable today because the collapse also blinds the roll-up disagreement detector. Fixing the projection is the precondition for that sweep, not the sweep itself.