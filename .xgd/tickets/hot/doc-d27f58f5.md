---
uid: doc-d27f58f5
id: DOC-9
type: doc
title: XGD Positioning
created_by: xgd
created_at: '2026-06-28T23:20:25.351081+00:00'
updated_at: '2026-07-30T21:17:49.797674+00:00'
completed_at: null
last_field_updated: body
status: draft
fields:
  doc_kind: project_context
  audience: internal
---

# XGD Positioning

_Internal working document. The keystone of our messaging: the source of truth that both the
public whitepapers ([[DOC-4]], [[DOC-5]], [[DOC-8]]) and the Business & Marketing Plan ([[DOC-7]])
draw from. If this drifts, every downstream doc drifts. Get this right first._

> **Revision note — 2026-07-30.** This document had drifted from the product and from its own
> downstream papers. It described XGD's original conception: a fully automated pipeline that takes
> a specification in at the top and produces validated code at the bottom. That is now the
> *secondary* mode. The primary mode — **free coding**, with reconciliation running behind it — is
> how XGD is actually used, including by us.
>
> The whitepapers had already moved: [[DOC-4]] §Wave 3 states that automation "returns generative
> development to the speed of vibe coding but with the discipline of agentic engineering integrated
> into it," and [[DOC-5]] §4 documents free coding, reconciliation, and the five-to-ten-minute loop.
> The keystone was the stale one. §1, §2, §5, §6, §7, §8 and §10 are revised accordingly; §2.1 is
> new.

## 1. Core message

**XGD makes generative development safe without making it slow.**

Two clauses, both load-bearing, and they answer two different competitors:

- **_Safe_** separates XGD from vibe coding, which got the human out of the loop and lost the
  guarantees.
- **_Without making it slow_** separates XGD from every attempt to fix vibe coding by putting
  process in front of the developer — specs first, review every diff, wait for the cycle. This is
  the newer and less contested claim, and it is the one competitors are not making.

The mechanism behind both: **governance runs behind the developer, not in front of them.**

## 2. The three-act spine

The narrative that relates to two anchors people already know — vibe coding (recognizable) and
agentic engineering (credible) — without being either. Drawn from the four-waves argument in
[[DOC-4]].

- **Vibe coding** got the human *out of the loop* and lost control. But note *why* people keep
  going back to it: the loop is short. You see the consequence of a change in minutes, and short
  loops are how you learn — about the architecture and about what the product should be.
- **Agentic engineering** restored control by putting the human *back in the loop*, reviewing every
  diff. A fully automated spec-driven pipeline goes further and removes the human again — but pays
  for it in cycle time, because planning, design, and testing all sit on the critical path. Either
  way, **the governance is in front of you**, and the loop stretches from minutes to hours.
- **XGD** keeps the short loop and moves the governance *behind* it. You work at conversational
  cadence; reconciliation builds the specification and test infrastructure in the background;
  regressions are caught and repaired automatically.

**The line that carries the whole thing:**

> Vibe coding put nothing in your way and gave you no guarantees. Agentic engineering gave you the
> guarantees by putting itself in your way. **XGD runs the governance behind you.**

_(Internal explanatory line. The older formulation — "XGD gives you the guarantees without the
reviewer" — remains true and is still useful for the out-of-the-code-loop half, but it says nothing
about cadence, which is now half the position.)_

### 2.1 The two modes — and why cadence is positioning, not implementation

XGD has two working modes ([[DOC-5]] §4). Which one leads is a positioning decision, and it has
changed.

| Mode | Loop time | What it is |
|---|---|---|
| **Free coding** (primary) | 5–10 minutes | Interactive work with the AI under lightweight process enforcement — intent ticket, tests, traceable commits. Feels like structured vibe coding. Reconciliation folds the result into the Capability Matrix afterwards, in the background. |
| **Autonomous coding** (secondary) | Several hours | Full unattended cycle: technical design, planning, TDD, code review, intent review. The overnight mode. |

**Why this reordering happened, and why it is a marketing fact rather than an engineering detail:**
XGD was built autonomous-first. In practice its own creator kept falling back to vibe coding for
day-to-day work, because immediate feedback was worth more than immediate rigour. Two problems
drove it — specifications are hard to get right for anything non-trivial, and a full cycle takes
hours even for a small bug. Free coding exists because the autonomous mode, on its own, lost to the
thing it was meant to replace.

Cycle time from intent to observable behaviour is a first-order metric in lean and agile practice,
and it is first-order here too. **A governance system people route around provides no governance.**
That is the argument, and we have run the experiment on ourselves.

The corollary for messaging: the *experience* of XGD is vibe-coding-like, and we should say so. The
*difference* is the Capability Matrix and the machinery around it. Lead with cadence; differentiate
on the matrix.

## 3. The category

XGD is not a tool *or* a practice — they are indivisible (the practice cannot be run without the
system; the system cannot run any other practice). That fusion is a **moat**: competitors can copy
a feature, not an architecture-plus-methodology.

XGD is a **governor for generative development** — a closed-loop control system.

- **Open-loop** coding agents run to completion and *hope* the output is right.
- **Closed-loop** XGD takes intent in, drives a controlled outcome out, and corrects regressions
  inside the loop.

The cleanest analogy (almost literal): **Kubernetes reconciles infrastructure to declared state;
XGD reconciles software to declared behavior.** (Our branch topology literally calls this
"reconcile.")

The analogy has become *more* apt under §2.1, not less: a Kubernetes controller reconciles
**asynchronously and continuously in the background**, while you carry on working. That is exactly
the shape of free coding plus reconciliation — and it is a precise, technical way to say "the
governance runs behind you" to an audience that already knows what a control loop is.

## 4. The compiler analogy

Our strongest rhetorical device — and, with the right framing, a defensible one.

- **What it establishes:** you don't review the assembly your compiler emits — you trust the
  compiler and test behavior. XGD aims to make AI-generated code like compiler output: an
  abstraction layer you trust, so reading the code is as unnecessary as reading assembly. The
  review didn't vanish; it **moved up a level of abstraction** — from implementation to behavior.
  The human reviews what the software *does*, not how it is written.

- **The honesty it forces (anti-magic-wand):** the compiler removed the need to write assembly; it
  did **not** remove the need for an engineer. XGD raises the level of abstraction; it does not
  remove the need for real engineering — architecture, technology choices, API decisions, and
  ownership of final quality still require a human with judgment.

- **The seam — and why it is our justification, not our weakness:** a compiler is *deterministic*;
  natural-language-to-code is *ambiguous and lossy* ("describe a UI in English and you don't always
  get what you expect"). That imperfection is precisely *why* you need a closed-loop governor and
  not just a smarter code generator — something to reconcile, prove behavioral conformance, and
  catch the gap between what you *said* and what you *meant*, plus an Artificer to validate
  outcomes. The non-determinism is the proof you need XGD.

  > Compiler-like trust in the output; governor-like control because the input is fuzzy.

## 5. Who it is for — and who it is NOT for

**For: technical builders with engineering judgment.** Technical founders, ex-engineers, the
"product manager with a CS degree." People who can make architecture / tech-stack / API decisions
and judge the quality of a delivered product.

**Not for: the no-code / citizen-developer market.** XGD will turn a PM-with-a-CS-degree into a
programmer; it will **not** turn an arts graduate into one. We are emphatically *not* competing
with Lovable / v0 / Bubble on "anyone can build an app."

**Marketing consequence — qualify in *and* qualify out:**
- *Qualify in* the technical: speak to people who make architecture/API/stack decisions. The
  language attracts the right user and signals seriousness.
- *Qualify out* the magic-wand seekers: non-technical users who expect to build a SaaS without
  understanding anything will fail, churn, and write our worst reviews. Honest positioning is
  cheaper than refunds and bad press. Read "founders" as **technical founders.**

**New tension introduced by §2.1, and how to hold it.** Leaning on vibe-coding cadence pulls
directly on the audience this section exists to repel — "feels like vibe coding" is what Lovable
and v0 promise. The resolution is to **lead on cadence, not on the phrase**: promise the short loop
("you never wait for the process"), and use vibe coding as the named *contrast* inside the argument
rather than as the promise in the headline. Capability Matrix language, architecture ownership, and
the regression benchmark in §8 all do qualify-out work in the same breath — keep at least one of
them adjacent to any cadence claim.

## 6. What the human still owns

The human is **out of the code-review loop** and, in free coding, very much **in the development
loop** — steering interactively, at conversational cadence. Those are different loops, and
conflating them is the most common way to misstate the position. "Out of the loop" alone is now
imprecise; say which loop.

Even with no line of code reviewed, the Artificer owns:
- **Intent** — saying what to build.
- **Architecture** — system structure and its consequences.
- **Technology & API choices** — and living with their trade-offs.
- **Final quality** — confirming the delivered product is what was asked for, in the form expected.

What XGD takes is not the direction — it is the bookkeeping that scales badly with human attention:
maintaining the behavioral record, generating and running the tests that pin it, detecting
regressions, and repairing them.

## 7. Two registers (same truth, different altitude)

| | Category narrative | Founder value message |
|---|---|---|
| Audience | Visionaries, press, the whitepapers, "why this is different" | The buyer, the landing page, the ad |
| Register | Sophisticated, defensible | Emotional, simple |
| Example | "A governor that reconciles software to declared behavior — asynchronously, while you keep working; it takes the human out of the code loop the way the compiler did with assembly." | "Work at the speed you already like. XGD catches what breaks behind you — and fixes it." |

Use vibe coding as the **experience benchmark and contrast**, never as the category: *"feels like
vibe coding, behaves like engineering."* Hook with the feeling, pivot to the guarantee.

## 8. Proof

We have three distinct proof assets. They do different jobs and should not be conflated.

**8.1 — Built with XGD.** XGD was built with XGD (and vibe coding). Its creator has not read a
single line of its Python source — yet deeply understands what is going on and continually reminds
the AI of the design decisions made along the way. Over nine months: 130,000 lines of production
code, 300,000 lines of test code, one Artificer, 30–50 tickets in a typical week.

This one fact proves *both halves* of the position at once:
- Human out of the code loop ✅ (zero lines reviewed)
- Engineering judgment still required ✅ (the human holds the architecture and design decisions)

> "I built a platform I've never read the source of — but I never stopped being its engineer."

**8.2 — The regression benchmark.** On a complex codebase, free coding produces roughly **one
regression for every two tickets implemented**. XGD catches and repairs them automatically.

Framing matters, and it is easy to get backwards. **This is the error rate you should expect from
structured vibe coding — vibe coding with design docs — as a practice.** It is not a defect
introduced by XGD; it is the ambient cost of generative development on a real codebase, which
almost nobody measures because almost nobody has an instrument that can. Our claim is the
instrument and the repair, not the rate.

Honesty constraint: this is a single system observed over nine months. State the sample. A
technical audience trusts a hedged number far more than a confident one, and overclaiming here
would undercut §8.1.

**8.3 — The abandonment story.** We built the fully autonomous pipeline first, and then noticed we
were not using it — the loop was too long, and vibe coding kept winning. Free coding exists because
of that finding.

This is the same rhetorical shape as 8.1, and nearly as strong: a founder reporting an inconvenient
result about their own product. It disarms the "governance is overhead" objection before it is
raised, because we hit that objection first and redesigned around it. Currently unused in any
public material — it should not stay that way.

## 9. The Software Artificer

The role is *defined* by the position: the Artificer is the human who has stepped **out of the code
loop** — declaring intent and validating outcomes, not reading diffs. "No line of code requires
human review" is not just an aesthetic; it is the boundary that separates an Artificer from a
reviewer. (We coined "generative development" and "the Software Artificer" precisely to escape the
low-status "vibe coder" label while still relating to it.)

## 10. Dos & don'ts (quick reference)

**Do**
- Lead with both halves: **safe** *and* **not slow**. Either alone is a claim someone else makes.
- Say what using it *feels like* — interactive, minutes not hours. The experience is a
  differentiator and we spent a long time not mentioning it.
- Use the compiler analogy — but always pair the bold claim with the proof mechanism.
- Use "agentic engineering" (defined; in our own paper), not the fuzzy "agentic coding."
- Target technical builders; speak their language.
- Use the build-with-itself proof early and often — and the abandonment story (§8.3) alongside it.
- Be precise about *which loop* the human is out of (§6).

**Don't**
- Anchor the *category* to vibe coding — it is the experience benchmark and the contrast, not what
  we are. Lead on cadence rather than on the phrase itself (§5).
- Describe XGD as a specification-in, code-out pipeline. That is the secondary mode and it was
  losing to vibe coding until free coding existed.
- Promise "no process." There is process; it runs behind you. Claiming otherwise attracts exactly
  the audience §5 exists to repel, and it is not true.
- Put **autonomy / self-maintaining** in the front-line message — it is the visionary north star,
  not the day-one claim, and it spooks pragmatists.
- Claim to "automate agentic engineering" wholesale — we automate the parts that don't need a human
  (plan supervision, diff review, eval loops); intent-setting stays human. Say so.
- Quote the regression rate without its framing (§8.2). Unframed it reads as an indictment.
- Drift into no-code / citizen-developer language.

## Open / next

- **Tagline — resolved, but only half of it.** REQ-95 settled on **"AI writes it. XGD keeps it
  working."** after a full divergent pass (rejected: "the guarantees without the reviewer" —
  vague; "proves it works" — formal-methods baggage; "ensures" — compliance-deck filler; anything
  foregrounding an absence — reads as negligent). It carries *safe*. It is silent on *not slow*,
  which §1 now makes half the message — so the sub-headline must carry cadence, and currently
  does not.
- **Channel/voice guide and SEM messaging** will inherit from this doc when those workstreams
  start.
- **[[DOC-5]] §4 defect:** the section is titled "Three Modes of Working" and describes two.
  Either a mode is missing or the title is wrong.
- **[[DOC-8]]** is not release-ready; the public paper offer is DOC-4 + DOC-5 for now.
