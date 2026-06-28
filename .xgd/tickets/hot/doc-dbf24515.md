---
uid: doc-dbf24515
id: DOC-5
type: doc
title: 'Extreme Generative Development: An Experiment in AI Software Development'
created_by: xgd
created_at: '2026-06-28T21:43:04.157835+00:00'
updated_at: '2026-06-28T21:43:04.157835+00:00'
completed_at: null
last_field_updated: created_at
status: draft
fields:
  doc_kind: project_context
---

# Extreme Generative Development (XGD): An Experiment in AI Software Development

Martin Westhead · GenDev Labs

---

## Overview

A previous paper in this series argued that the scaling wall in AI-driven development is a structural problem: as systems grow, behavioral integrity erodes unless an explicit, maintained record of what software is supposed to do is kept and verified against the running system. The paper described the structural requirement — _behavioral identity_ — and argued that its maintenance must be automated.

This paper describes Extreme Generative Development XGD, a governed generative development platform built to satisfy that requirement, and reports on nine months of using it to build itself.

---

## Contents

1. The Problem Restated

2. XGD: Three Contributions

3. Building XGD with XGD: Nine Months at the Frontier

4. Three Modes of Working

5. What We Don't Yet Know

6. An Invitation

---

## 1. The Problem Restated

The scaling wall is produced by a specific structural absence: no explicit, maintained record of what the software is supposed to do. When code and tests are both changing continuously under AI-driven development, the question "was this a regression or an intentional change?" has no reliable answer unless intended behavior was recorded explicitly. Without that record, behavioral integrity erodes silently. With it, regression detection is mechanically grounded.

The requirement is specific: a behavioral specification that reflects current intended behavior (not just historical decisions), is continuously verified against the running system through executable tests, and exists as a human-readable artifact independent of any model session. The challenge is maintaining that record at scale, under continuous change, without creating a bottleneck.

## 2. XGD: Three Contributions

Most development tools execute steps. XGD pursues outcomes.

The distinction is the same one that separates a steam governor from a throttle. A throttle does what you tell it: open, close, hold. A steam governor monitors actual engine speed, compares it against the target, and continuously adjusts — not by executing a script, but by closing the gap between where the system is and where it should be. That feedback loop is what made industrial steam power reliable and scalable. The engine was already powerful; the governor is what made that power usable at scale.

Every governor requires three things: a target state it is trying to reach, a correction mechanism that detects deviation and drives toward the target, and a control surface through which the operator sets intent and monitors progress. XGD contributes one of each.

### 2.1 The Capability Matrix — Target State

XGD implements behavioral identity as the Capability Matrix: a persistent, managed artifact that is the authoritative record of what the software is supposed to do.

The Capability Matrix is organized around familiar objects. Behaviors are grouped into _capabilities_ — logical areas of functionality that reflect how users and developers think about the system. Each capability contains _stories_ that describe specific behaviors from a user perspective. Each story has _acceptance criteria_ that make the behavioral expectations explicit and testable. Each acceptance criterion has an associated _user acceptance test_ that runs against the actual code.

This structure — capabilities, stories, acceptance criteria, tests — is one every practitioner already knows. The Capability Matrix does not introduce new concepts. It maintains existing ones rigorously, automatically, and in correspondence with the running system.

The critical distinction is between what the Capability Matrix records and what the code records. Code tells you _how_ each component works — its structure, its logic, its dependencies. The Capability Matrix records _what_ each capability is supposed to do. When a behavior changes, the code alone cannot tell you whether that change was intentional. The Capability Matrix can — because it records the intended behavior explicitly, and the user acceptance tests verify that the code currently satisfies it.

A specification document diverges from the code silently over time. The Capability Matrix cannot diverge silently — the tests fail the moment the code deviates from the stated intent. The behavioral claims are operationally grounded, not maintained by discipline. This is what makes regression detection reliable.

The Capability Matrix also solves the session boundary problem directly. Every AI session starts at zero — no accumulated sense of intent, no informal understanding built over months of working on the system. When XGD begins a development cycle, the Capability Matrix is the persistent answer to "what were we building and why?" Not reconstructed by inference from the code. Carried forward from accumulated decisions, verified against the running system.

### 2.2 Automated Agentic Engineering — Correction Mechanism

The previous paper identified _agentic engineering_ — writing specifications before coding, reviewing every diff, building evaluation loops — as the right discipline for professional AI-assisted development. It is. But discipline alone cannot bear the load at scale: review capacity saturates, context windows limit what any single session can hold, and the human attention required to govern each cycle becomes the bottleneck.

XGD automates the agentic engineering workflow. An intent is expressed — a behavioral requirement, a bug, a capability to add. XGD drives from that intent to a validated outcome: generating a technical design, breaking work into tasks, implementing via TDD, running quality checks, triggering fix loops when tests fail, iterating until the running system satisfies the stated criteria. The platform takes responsibility for the gap between instruction and outcome.

This is not a code generator. It is a correction mechanism. The Capability Matrix defines the target state; the automated engineering cycle detects the gap and closes it. What previously required constant human supervision — checking that each change didn't break prior behavior, verifying coverage, catching regressions — happens automatically, continuously, and at the pace of the machine rather than the pace of the human.

### 2.3 The Software Artificer's Operating Environment — Control Surface

The previous paper introduced the Software Artificer: the emerging technical human role that governs AI-driven development at scale. Defining the role is necessary but not sufficient. The role requires an environment in which it can actually be performed.

XGD's dashboard is that environment. It provides the control surface through which the Artificer sets intent, monitors progress, and validates outcomes without needing to supervise every line of generated code. A ticket system captures and tracks behavioral intent. An intent editor — with LLM assistance for drafting specifications — lowers the cost of expressing requirements clearly. A workflow monitor surfaces the state of every running or completed development cycle. An evidence view shows which capabilities are verified, which have gaps, and where the system's behavioral record is incomplete.

Together these surfaces make the Software Artificer role sustainable. Without them, governing AI-driven development at scale requires the same level of direct attention that conventional software development does — the role becomes a title without an operating environment. With them, a single Artificer can oversee a volume of development activity that would otherwise require a team.

## 3. Building XGD with XGD: Nine Months at the Frontier

XGD has been built with generative development from the very beginning. At time of writing it is over 130,000 lines of code, with over 300,000 lines of test code. It was created by a single software artificer over nine months. Although there have been extensive technical discussions with Claude Code over that time, not a single line of production code has been reviewed by a human.

The velocity data: a single SA implementing 30–50 tickets in a typical week, contributing approximately 3,800 lines of production code. Peak weeks have exceeded 8,000 lines and 100 tickets. On the current codebase, XGD automatically catches one regression for every two tickets created.

The most significant finding is not the velocity. It is the stability. A 130,000-line system, no human code review, one developer — and behavioral integrity is maintained automatically. Not by discipline, but by infrastructure.

## 4. Three Modes of Working

XGD supports three operational modes, each suited to different development needs.

**Interactive (free) coding.** Direct interaction with Claude Code, with lightweight process enforcement: an intent ticket is created, tests are built, code is committed with traceability metadata. A background reconciliation process takes the free-coded feature and builds specification and test infrastructure around it, incorporating it into the Capability Matrix. This mode preserves the iteration velocity that makes vibe coding valuable — results in five to ten minutes — while ensuring the feature is eventually brought into the governed structure.

**Autonomous coding.** Full automation: technical design, planning, TDD-based development, code review, and intent-level review, all unattended. Results in several hours. This is the mode that runs overnight, producing validated, regression-proof output while no one is watching.

**The tension between modes** is real and worth naming. Iteration time matters not just for speed but for discovery — both engineering discovery (learning how a new architecture or API actually behaves under real conditions) and product discovery (learning what software should be by seeing a version of it). The faster the loop, the more you can learn. Free coding preserves that loop at the cost of some immediate structural rigour, with reconciliation closing the gap afterward. Autonomous coding trades velocity for rigor — the right choice once the direction is established. The two modes are complementary, not competing.

## 5. What We Don't Yet Know

XGD is still early. Three areas of genuine uncertainty:

**Practical experience.** The Capability Matrix has not been applied outside of XGD itself. We have confidence it scales to low hundreds of thousands of lines of code. Whether the approach holds on larger systems is untested.

**Knowledge management.** XGD stores a large corpus — tickets, conversations, design decisions, historical intent. Making that corpus reliably accessible to AI systems at the point of decision is an unsolved problem.

**Workflow stability.** Long-running autonomous workflows still have reliability issues that affect velocity estimates. The figures above reflect stable periods; downtime during workflow failures can skew the numbers significantly.

## 6. An Invitation

We are still learning. If you are building at this frontier — with XGD or with your own approach — we want to hear from you. Findings that contradict what we have described here are as valuable as ones that confirm it. We are running a closed beta for teams who want early access to the platform.

beta@gendevlabs.ai