---
uid: decision-26290aa2
id: DECISION-3
type: decision
title: Build flagship sites ahead of the builder, as R&D vehicles
created_by: xgd
created_at: '2026-08-06T21:24:01.856556+00:00'
updated_at: '2026-08-06T21:24:01.856556+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-07-02'
  rationale: A builder designed before any real site has been built encodes guesses.
    Building demanding sites first generates the design intelligence that tells you
    what the builder must actually support.
  caused: []
  deferred: []
---

Order the work as framework, then flagship sites, then the builder (DOC-16 §4) — the sites are the R&D vehicle that *generates* design intelligence rather than a consumer of a finished tool.

**Consequence worth preserving:** the relationship between a flagship site and the builder is deliberately soft and is deliberately **not** filed as a `depends_on` edge, because a hard dependency would falsely park the site off the ready frontier.

This is why the XGD website exists as two goals rather than one: 1stcontact GOAL-7 is the design-R&D vehicle, and lagrange-biz GOAL-17 is the published marketing asset.