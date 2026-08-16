---
uid: decision-b805e879
id: DECISION-9
type: decision
title: Move 1stcontact natively onto Cloudflare workerd, sixteen days from the class
  deadline
created_by: xgd
created_at: '2026-08-16T01:23:18.050668+00:00'
updated_at: '2026-08-16T06:28:54.973265+00:00'
completed_at: null
last_field_updated: rationale
status: null
fields:
  decided_at: '2026-08-15'
  rationale: 'Two arguments, both from the operator. First, shareability: the tool
    cannot be shared from a laptop, and the class cohort has to use it - so Cloudflare
    is a hard prerequisite for the goal, not an infrastructure preference. Second,
    and the reason for going early rather than late: many things differ in the cloud,
    and building the CX on a laptop means developing against a comfortable illusion.
    Forcing the move now means the customer experience being designed is the real
    one.'
  caused:
  - goal-198516d1
---

## What happened

Eight requests filed in four minutes on 2026-08-15, 13:30-13:34 local (1stcontact REQ-141 to REQ-148), preceded by an update to 1stcontact/DOC-1, Gendev Website Caretaker Architecture, the same day.

Together they move 1stcontact from running *beside* Cloudflare to running *inside* it: an async SiteStore port with D1 and R2 behind it, routes and L1 render in workerd, the proxy deleted, the AI host and publish moved in, the builder made private behind Cloudflare Access, and behaviour modules precompiled for workerd.

## Why - in the operator words

> "The app needs to be on Cloudflare for the goal - if it is on my laptop I can not share it. We are going web with it early so I can use it in that environment and not kid myself it works because I am using it on my laptop. Many things are different in the cloud; if I force us there early I can develop the real CX and not fool myself. Either way that is a priority decision - the tool cannot be shared without it, so it is a hard dependency on our goal."

Two distinct arguments, and the second is the less obvious one.

**Shareability** makes this a prerequisite rather than a preference. A builder on a laptop cannot be handed to a class. That alone makes GOAL-65 a hard dependency of GOAL-47 (Site builder, 2026-08-31), now recorded as such.

**Not fooling yourself** is why it happens *now* rather than at the end. A CX developed against localhost is developed against conditions that will not hold - latency, cold starts, bindings, auth, failure modes. Building it there produces an experience that feels good to its author and may not survive contact with the platform. Moving first means every subsequent design decision is made against the real thing.

That is the same discipline as the capability matrix, and as REQ-141 below: build the conditions that tell you the truth before doing the work that depends on them. It recurs often enough across this project to be a working principle rather than a habit.

## The sequencing choice worth noticing

REQ-141 - a workers-runtime test project running UATs inside workerd against real D1 and R2 bindings - is `ready_to_reconcile` while most of the migration is still `draft`. The harness that can tell you whether the migration worked was built **first**.

Same instinct as DECISION-7, where ai_ticketing was made the first consumer of the Toolbox to prove the design.

## Cost

Attention, sixteen days out from the class cohort date, on a goal whose long pole is product discovery rather than available time. The risk is not that the migration is slow - it is that it competes with the discovery the builder still needs.

Against that: the migration is not optional for the goal, so the only real question was when, and doing it before a cohort arrives is cheaper than doing it with one on the system.

## Resolved

An earlier draft left open whether the Cloudflare work and the Site builder were the same work or a dependency pair. **Settled: hard dependency.** GOAL-47 now depends_on GOAL-65.

Consequence to watch: under the readiness rule, Site builder is not-ready until the migration is realized. That is now literally true - the builder cannot be shared without it.