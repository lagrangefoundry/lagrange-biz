---
uid: doc-3ca0a1f8
id: DOC-7
type: doc
title: XGD Business & Marketing Plan — Initial Context
created_by: xgd
created_at: '2026-06-28T22:19:53.328638+00:00'
updated_at: '2026-06-28T23:15:26.368563+00:00'
completed_at: null
last_field_updated: audience
status: draft
fields:
  doc_kind: project_context
  audience: internal
---

# XGD Business & Marketing Plan — Initial Context

_Working planning document. Captures the current state, positioning, phases, and marketing
workstreams for taking XGD to market. Companion to the foundation docs: [[DOC-4]] (the scaling
wall / behavioral identity argument), [[DOC-5]] (the XGD self-build experiment), and [[DOC-6]]
(distribution, identity & licensing architecture)._

## Scope of this project

This is a **planning and marketing-content** effort, not a development effort. No new XGD
functionality is planned here. The live design surface is **positioning** — how XGD is framed
and sold.

- **Execution team:** Martin + Claude (just the two of us). This constrains how much can run
  in parallel and should anchor every timeline.
- **Forcing function:** None. There is **no external deadline** (no conference, funding round,
  or demo pulling on the beta date). Beta timing is **purely quality-gated** — it happens when
  the system is stable.

## Current state

- XGD is **~95% feature-complete for beta**.
- **Not beta-ready yet** — blocked on quality, not features.
- Concretely: a **reconciliation backlog estimated at 1–2 weeks**, plus an expected tail of
  bug fixes still to come.
- Outstanding **licensing / packaging** work exists (DOC-6 territory) but is parked for now.
- The core value offering is understood today; even so, articulating it is a useful exercise.

## Product positioning (core thesis)

XGD is **automation that closes the gap on vibe coding so that output is predictably robust and
regressions are automatically spotted and fixed.**

Three benefit tiers, escalating in ambition:

1. **Force multiplication** — a single developer becomes a team that can move at vibe-coding speed.
2. **Behavioral guarantees** — we know with confidence what functionality is being built
   (behavioral identity, automatic regression detection).
3. **Autonomy** — fully autonomous development is possible; the ultimate aim is
   **self-maintaining XGD projects**.

This ladders directly off DOC-4 and DOC-5.

## Business phases (go-to-market)

1. **Closed Beta** — once the system is sufficiently stable, invite external users to start
   using the product.
2. **Launch** — free for use with **public git repos**; modest per-seat subscription for
   **private repos at $25–$100 / seat / month**. Initial customers: founders and greenfield
   projects.

## Customer phases (segment progression)

1. **Founders & greenfield projects** — the launch target.
2. **Consultancies** — leverage the boutique India + Romania consulting orgs.
3. **Enterprise** — once legacy CM gaps are filled and demand is demonstrated.

## Marketing workstreams

The 11 anticipated activities, grouped into 6 clusters:

### A. Content foundation
- Finish the draft docs.
- Blog posts on the site, plus Medium, LinkedIn, Reddit, and a newsletter — expecting to
  cross-post the same content across channels.
- **State of GenDev survey** — start by polling LinkedIn colleagues; potentially a ~6-month
  survey out to the mailing list that generates a summary post. Key risk: securing sufficient
  participation.

### B. Web platform
- Website: initially **blog → whitepaper lead capture → beta signup**. Later a **customer portal**
  for managing subscriptions.

### C. Showcase project
- Open-source **modular markdown editor** as a live proof point: open-source repo + video
  content + blog content.

### D. Education
- **XGD classes** — self-learning tutorials contributed to education sites; in-person tutorials
  at conferences.
- **Train the trainers** — get other people set up to deliver the classes.

### E. Field presence
- **Conference & meetup appearances** — significant Bay Area opportunity to speak at events;
  expected to compound once there's a little momentum.

### F. Paid & channel
- **SEM plan** — a tailored paid-marketing plan, once the paid product is launched.
- **Consulting arm** — use the XGD name to bring in business via the partner consultancies and
  take a cut. Arguably more important: **learn what the tool is missing**, particularly for
  enterprise deployment.
- **Enterprise-ready XGD** — fill gaps in legacy CM coverage, demonstrate demand, and recruit
  an enterprise CEO to sell it.

## Cross-cutting notes

- **Critical path is quality, not marketing.** Beta gates everything downstream, and beta gates
  on stability (clearing the reconciliation backlog + bug tail). However, much of clusters A and
  B can proceed **in parallel** with quality work — they don't require a beta-stable product.
- **Cross-posting caveat:** cross-posting identical content is mostly fine, but Reddit penalizes
  copy-paste promotional content (needs community-specific framing) and there should be a
  canonical home (the blog) that other channels point back to. To be detailed under cluster A.

## How the layers align

| | Founders / Greenfield | Consultancies | Enterprise |
|---|---|---|---|
| **Business phase** | Launch | Post-launch | Later |
| **Lead workstreams** | A, B, C, E | D, F (consulting) | F (enterprise) |

## Open / next

- Layer **timelines** onto these workstreams (next conversation), anchored to a two-person team
  and a quality-gated (undated) beta.