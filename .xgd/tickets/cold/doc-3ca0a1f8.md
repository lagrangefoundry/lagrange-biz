---
uid: doc-3ca0a1f8
id: DOC-7
type: doc
title: XGD Business & Marketing Plan — Initial Context
created_by: xgd
created_at: '2026-06-28T22:19:53.328638+00:00'
updated_at: '2026-06-28T23:48:14.543897+00:00'
completed_at: null
last_field_updated: body
status: draft
fields:
  doc_kind: project_context
  audience: internal
---

# XGD Business & Marketing Plan — Initial Context

_Working planning document. Captures the current state, positioning, phases, and marketing
workstreams for taking XGD to market._

**Related docs:**
- **Positioning keystone:** [[DOC-9]] — the source of truth for messaging; this plan executes it.
- **Public whitepapers:** [[DOC-4]] (frame the problem), [[DOC-5]] (XGD as the solution),
  [[DOC-8]] (accountability & safety).

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
- Outstanding **licensing / packaging** work exists but is parked for now. (Note: this is a
  hidden dependency for *Launch* — you cannot charge for private repos without it — even though
  it is not needed for *Beta*.)
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

## Dependencies, Sequencing & Launch Gates

### Three insights that drive the whole sequence

1. **There is exactly one hard gate: Quality → Beta.** Everything customer-facing waits on it;
   a large amount of asset-building does not. Strategy: front-load every non-gated thing now, so
   the instant quality clears, beta opens into a warm audience with assets ready.
2. **The binding constraint is Martin-hours, not the calendar.** Claude can draft content/code/
   structure in parallel; only Martin can do quality work, talks, on-camera, architecture, and
   relationships. Ordering must avoid stacking Martin-heavy activities concurrently.
3. **Beta is a reference factory, not just product validation.** Pragmatist customers buy on
   references from people like them; references only come from beta. Beta's *output*
   (testimonials, case studies, the showcase) is a dependency for everything downstream.

### Launch-gate buckets (the operative view)

**(1) Required FOR beta launch** — doors can't open without these:
- **[GATE] Quality**: reconciliation backlog cleared + bug tail acceptable. (The one hard prereq.)
- **Beta cohort secured**: enough committed participants. Consulting contacts are the seed;
  "sufficient participation" is the risk → needs a waitlist + invite mechanism.
- **Minimal beta landing/signup page** (Martin-driven; subset of the full website).
- **Minimal onboarding / getting-started docs (D1-min)**: enough to install, run, and understand
  the loop. Activation is load-bearing → genuinely required.
- **Minimal bug intake + triage process**: must exist; need not be automated yet.
- **Beta ToS / agreement**: lightweight usage terms. (NOT the paid licensing — see bucket 3.)

**(2) Required shortly AFTER beta launch** — can lag the opening (light bucket):
- **Ticket automation**: triage, bug dedup, optimistically auto build/test/deploy of fixes with a
  quick review. Build during beta; it makes the beta sustainable for two people.
- Onboarding iteration from first-user friction.
- Reference/case-study capture once users have wins.

**(3) Required FOR paid launch:**
- **[GATE] Beta validated** (works + references).
- **Licensing / packaging** (the real one): public-free vs private-paid, enforced. (Martin-heavy.)
- **Billing + customer portal (website v2).**
- **Full public website** (Martin-driven): blog, published whitepapers, lead capture, pricing.
- **Whitepaper trilogy published.**
- **Matured support capability** (bucket-2 automation grown up).

**(4) Required shortly AFTER paid launch:**
- SEM live (post-launch). Sustained content push. Field presence / talks land (if CFPs submitted
  in Wave 0). Full education program (D2) + first tutorials. Formal State of GenDev survey.

**(5) Anything else / later:**
- Train-the-trainers. Consulting arm formalized (people are already the beta cohort; the
  commercial channel is later). Enterprise-ready XGD (legacy CM gaps, demand proof, enterprise CEO).

### Scope sizing (relative; bottleneck = Martin-hours)

| Workstream | Bucket | Size | Martin-intensity | Notes |
|---|---|---|---|---|
| Whitepapers (×3) | 0→3 | M | Med | DOC-8 is a stub → most work |
| Website — beta signup page | 1 | S | **Med–High** | Martin drives design |
| Website — full public + portal | 3 | L | **Med–High** | Martin drives design; needs billing + licensing |
| Showcase project | 1→2 | XL | High | Build + video + blog; longest pole |
| Mailing list / survey seed | 1 | S | Low | Slow-burn asset |
| Conference CFPs | 1 | S | Med | Cheap, long lead — don't delay |
| Onboarding docs (D1) | 1 | M | Med | Gates beta activation |
| Bug intake + triage | 1 | S | Med | Manual is fine at first |
| Ticket automation | 2 | L | Med | Makes beta sustainable |
| Licensing / packaging | 3 | M–L | High | Hidden Launch gate |
| SEM | 4 | M | Low | Post-launch |
| Field presence | 4→5 | L | **Very high** | Martin only — serialize |
| Full education (D2) | 4 | L | Med | Inherits from D1 |
| Consulting arm | 5 | M | Very high | Relationship-bound |
| Enterprise-ready XGD | 5 | XL | Very high | Furthest out |

Pattern: **buckets 1–2 are parallelizable and Claude-heavy; buckets 3–5 are Martin-bound and
serialize.** Cram as much as possible into the pre-beta window while quality is the focus.

## Open threads — dedicated conversations to schedule

- **Beta operations & product maintenance** — duration, number of customers, the triage/dedup/
  auto-fix automation, sustaining the product during beta with two people.
- **Beta demand flywheel** — Cursor-style "everyone wants in" scarcity/FOMO to generate interest
  and leads.
- **The link between them:** closed beta resolves the tension — the *waitlist* is the marketing
  asset (big → leads + FOMO) while the *admitted cohort* stays small (→ supportable). Same
  mechanism, tuned from opposite ends.
- **Founder-facing tagline** — dedicated generation pass (see [[DOC-9]] §Open).

## Open / next

- With the dependency frame and launch-gate buckets recorded, **aspirational dates** can be hung
  on this scaffold — dated backward from the only real anchor (quality-done → beta), since
  everything keys off that. Defer until the beta-operations conversation pins beta scope/duration.
