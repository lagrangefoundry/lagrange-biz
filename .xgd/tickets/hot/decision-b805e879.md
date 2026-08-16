---
uid: decision-b805e879
id: DECISION-9
type: decision
title: Move 1stcontact natively onto Cloudflare workerd, sixteen days from the class
  deadline
created_by: xgd
created_at: '2026-08-16T01:23:18.050668+00:00'
updated_at: '2026-08-16T01:23:18.050668+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-08-15'
  rationale: 'DRAFTED FROM EVIDENCE - the rationale below is inferred from the tickets
    and needs the operator correction. The apparent reasoning: DOC-5 always specified
    a Cloudflare-first architecture, the current shape runs beside that platform rather
    than inside it via a proxy, and a production 503 traced to a [vars] inheritance
    bug exposed the deployment path as fragile. Doing the migration before the class
    cohort arrives is cheaper than doing it under load with real users on it.'
  caused:
  - goal-198516d1
---

## What happened

Eight requests filed in four minutes on 2026-08-15, 13:30-13:34 local (1stcontact REQ-141 to REQ-148), preceded by an update to 1stcontact/DOC-1, Gendev Website Caretaker Architecture, the same day.

Together they move 1stcontact from running *beside* Cloudflare to running *inside* it: an async SiteStore port with D1 and R2 behind it, routes and L1 render in workerd, the proxy deleted, the AI host and publish moved in, the builder made private behind Cloudflare Access, and behaviour modules precompiled for workerd.

## Why this is a decision and not a batch of tickets

Three of the structural signatures at once. A subtree appeared fully formed with no prior aspiration on the map. The shape of the system changed rather than its contents - "proxy deleted" and "control-app becomes the builder" are statements about what the thing *is*. And it started sixteen days before a hard external date, the class cohort on 2026-08-31.

## The sequencing choice worth noticing

REQ-141 - a workers-runtime test project running UATs inside workerd against real D1 and R2 bindings - is `ready_to_reconcile` while most of the migration is still `draft`. The harness that can tell you whether the migration worked was built **first**.

That is the same instinct as decision-46593d49, where ai_ticketing was made the first consumer of the Toolbox to prove the design. It is a consistent and unusual discipline: build the thing that reports truth before doing the work it will report on.

## What it costs and what it buys

The cost is attention, sixteen days out from a deadline whose long pole is product discovery rather than available time - so the risk is not that the migration is slow, but that it competes with the discovery the builder still needs.

What it buys, if the inferred rationale is right: a deployment path that does not produce unexplained 503s, an architecture that matches what DOC-5 has specified since June, and a builder that is private by construction rather than by proxy configuration. Doing it before a cohort arrives rather than during is the cheaper ordering.

## Open question carried into the goal

REQ-145 says the control-app *becomes* the builder. So this work and the Site builder goal (target 2026-08-31) are either the same work seen from two angles, or a prerequisite and its dependant. That distinction decides whether the site builder date is exposed to this migration, and it has not been settled.

## Note on this record

Drafted by the goal-map assistant from ticket evidence on 2026-08-15, the day it happened, so the reasoning is still recoverable. **The rationale field is inference, not the operator words.** Correct it.