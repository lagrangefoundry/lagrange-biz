---
uid: doc-893a2ac9
id: DOC-4
type: doc
title: 'Beyond the Scaling Wall: Behavioral Identity for Generative Development'
created_by: xgd
created_at: '2026-06-28T21:42:57.734252+00:00'
updated_at: '2026-06-28T23:15:13.156501+00:00'
completed_at: null
last_field_updated: audience
status: draft
fields:
  doc_kind: project_context
  audience: public
---

# Beyond the Scaling Wall: Behavioral Identity for Generative Development

Martin Westhead · GenDev Labs

---

## Overview

In 2025, a new mode of development went viral: describe intent, accept AI-generated changes wholesale, ship at extraordinary speed. It acquired a name — _vibe coding_ [1]. Within a year its creator, Andrej Karpathy, had declared it a transitional phase. Its successor, which he termed _agentic engineering_ [2], is a professional discipline: coordinating AI agents while preserving correctness, quality, and taste — designing specs, supervising plans, writing tests, building evaluation loops. Vibe coding raised the floor; agentic engineering raises the ceiling. The shift was really driven by something that all practitioners see when using AI coding: the _scaling wall_ — the point at which AI-assisted development, previously exhilarating in its speed, starts running aground because new changes create behavioral regressions that cannot be managed.

We use _generative development_ to describe any software development process in which AI systems produce the overwhelming majority of the code — the regime that current tools have already reached for many practitioners. Vibe coding, agentic engineering, and governed generative development are all variants. This paper's question is not whether to develop this way, but how to do so with behavioral integrity intact.

The scaling wall is not a failure of AI capability. At the task level, productivity gains are real and sustained: the AI keeps writing code, and the code largely works. The problem is cumulative regressions. Each change to a growing codebase carries risk — something that worked before may break — and without reliable mechanisms to detect regressions, behavioral integrity silently erodes. Forward progress eventually stalls altogether, not because the AI stops producing code, but because the changes it introduces have unanticipated consequences. We argue that the solution to this problem is structural — a matter of process infrastructure, not model capability.

This paper identifies the forces that produce the scaling wall, distinguishes those that better models will eventually resolve from those they can not, and describes the structural requirement that remains: an explicit, maintained record of what software is supposed to do — _behavioral identity_ — that makes regression detection reliable and system behavior auditable. We introduce the Software Artificer as the emerging technical human role that governs AI-driven development at scale. A companion paper describes XGD, a platform built to automate these ideas, and reports on nine months of using it to build itself.

---

## Contents

**Part I — The Shift**

1. Four Waves: Where AI Development Is Heading

2. Hitting the Wall

3. What Better Models Will and Won't Solve

**Part II — The Framework**

1. Behavioral Identity for Software Systems

2. The Software Artificer: A Role for the New Development Paradigm

---

## Part I — The Shift

### 1. Four Waves: Where AI Development Is Heading

The development of AI-assisted software is following a recognizable pattern: each wave amplifies capability while exposing a new class of structural problem that the technology and practices of that wave alone cannot solve.

**Wave 1: Augmented development.** The first wave gave developers AI as a collaborator — GitHub Copilot, then increasingly capable code assistants that suggest completions, answer questions, and generate functions on demand. The human remains firmly in the loop: every line of AI output is reviewed and accepted or rejected. The productivity gain is real — studies suggest 30–40% for routine tasks. The ceiling is equally real: output is bounded by how much code a human can review and understand.

**Wave 2: Vibe coding.** The second wave is generative development without governance. Vibe coding raises the floor — as Karpathy put it — making working software accessible at a speed and scale no human team can match. But without process discipline, code complexity accumulates unchecked: no specs, no structured review, no evaluation loops. Changes are accepted wholesale, technical debt compounds, and the codebase becomes progressively harder to navigate and extend. Forward progress eventually stalls.

**Wave 3: Governed generative development.** The third wave reimports the process discipline that vibe coding abandoned. At its entry — what Karpathy terms _agentic engineering_ — the developer writes specs, supervises plans, reviews every diff, and builds evaluation loops. The governance chaos of Wave 2 recedes, and the developer's role shifts from author to steward. But individual discipline, even rigorously applied, does not fully close the gap: without an explicit, maintained record of what the software is supposed to do — _behavioral identity_ — regressions remain undetectable and system behavior unauditable. Wave 3 matures as platform infrastructure closes that gap: behavioral criteria, regression detection, and process enforcement built into the development environment itself, not dependent on individual vigilance.

**Wave 4: Self-evolving systems.** The fourth wave, enabled by the third, is software that safely evolves through direct interaction with users and other systems. Bug reports and feature requests flow directly into governed development cycles. Validated changes roll out automatically. The human's role becomes one of intent-setting and oversight rather than active intervention. This is not a distant prediction — the infrastructure being built in Wave 3 is its prerequisite.

We are writing within Wave 3 — at the point where individual governance discipline is being automated into platform infrastructure. The methodology described in this paper is how we are navigating that transition.

### 2. Hitting the Wall

The scalability wall is real. Eighty-one percent of enterprise technology leaders reported production failures attributable to AI-generated code in 2026 [3]. Among startups pursuing AI-first development, 73% hit critical scaling failures by the six-month mark [4]. Despite task-level productivity gains, overall delivery velocity improved only modestly in real organisations — the bottleneck shifted from writing code to architecture, coordination, and quality assurance.

The developer community's response has been to call for more disciplined practice. Karpathy's agentic engineering — writing specs before coding, reviewing every diff, building evaluation loops — is now the dominant framework for professional AI-assisted development [2]. Large-scale telemetry across more than 10,000 developers documents what follows under disciplined practice: teams with high AI adoption merged 98% more pull requests, but review times grew 91% and average pull request size grew 154% [5]. The binding constraint has shifted from generation to validation and comprehension. Agentic engineering moves the wall; it does not eliminate it.

### 3. What Better Models Will and Won't Solve

The wall has several distinct causes. They do not all have the same solution, and not all of them are problems that agentic discipline or better models leave behind.

As codebases grow into the tens of thousands of lines, two forces start to bite. Firstly, architectural coherence becomes critical: code that was not appropriately structured accumulates technical debt that compounds with every change. And secondly the codebase starts to exceed what a model can hold in context — changes that look correct in isolation break things the model couldn't see. Both of these causes will be substantially mitigated as models improve. Larger context windows, better architectural reasoning, more reliable changes at scale: these are genuine directions of progress. Although, for practitioners building today, both remain significant sources of friction.

The third force is different in kind, and it is where regression detection itself breaks down. In conventional development, regression testing works because the development team knows what the code is supposed to do: when a test fails, the intended behavior is understood, and the question "was this failure due to a regression or a requirement change?" has a reliable answer. In AI coding at scale, both the code and the tests are changing continuously. When something breaks, if intended behavior has not been explicitly recorded and maintained, that question becomes unanswerable. This is known as _functionality flickering_ — the experience where a UI element is one color today and a different color tomorrow, because intended behavior was never explicitly anchored.  Practitioners report that agents routinely misunderstand early requirements and build entire features on faulty premises, compounding across five or more pull requests before detection [5]. A 2026 benchmark found that 12 of 20 state-of-the-art code agents score below 10% on clarification-seeking when given ambiguous instructions [5] — the agents do not check assumptions because there is no maintained record of intended behavior to check against. What is needed to mitigate this is a synthesized, maintained artifact that captures current intended behavior explicitly, and continuously verifies it against the running system through executable tests.

The fourth force is auditability. As systems grow in scale and complexity, the question shifts from whether the developers believe the system works to whether anyone — including the developers — can demonstrate it. Understanding that lives only inside a model session or in people's heads cannot be inspected, challenged, or handed off. The same artifact that supports regression detection solves this problem: an explicit behavioral record that exists independently of any session, human-readable, available for inspection and audit, verifiable against the running system. Without it, trustworthiness can only be asserted, never demonstrated.

The instinct to impose more structure — specifications before coding, enforced test runs, disciplined check-ins — is correct. The problem is not intelligence but process. But empirical evidence establishes that discipline alone cannot bear the load. Review-capacity saturation is structural: high-AI-adoption teams produce pull requests 154% larger on average, with review times 91% longer — more code per review, harder to validate, and less consistently checked [5]. A subtler dynamic documented in controlled trials is more concerning: AI-assisted developers score 17% lower on debugging, code reading, and conceptual understanding than developers working without AI [8, 9], while believing themselves to be 20% faster. Karpathy's framework relies on the engineer's own judgment as the irreducible anchor for correctness and intent; that anchor is measurably degrading.

---

## Part II — The Framework

### 4. Behavioral Identity for Software Systems

Every development team carries a shared understanding of what their software is supposed to do — held in conversation, memory, and the heads of the people who built the system. When a test fails, an experienced developer doesn't just read the code: they consult that shared knowledge to determine whether the code or the test is wrong. This is behavioral identity: the maintained understanding of intended behavior that sits alongside the code and gives it meaning. In a human team, it can survive imperfect documentation because people fill in the gaps. In an AI-driven system, it must be externalized — written down, maintained, and verifiable — or it does not exist.

Getting behavioral identity out of people's heads and into an explicit artifact changes the development equation. The same AI models that write code can build and maintain a behavioral specification — keeping it current as intents are applied, checking its integrity, using it to resolve the question a failing test cannot answer from code alone. Once behavioral intent is captured this way, the development workflow becomes automatable in ways that individual discipline cannot achieve. Human attention is freed from reconstructing intent to focus on higher-level questions of specification and direction. But this payoff depends on the artifact being well-formed — an imprecise specification, like an imprecise test, answers the wrong question.

There is a further subtlety. Behavioral identity is not a historical record — it is accumulated current state. A software system's intended behavior at any point is the sum of every design decision applied since inception: every feature, every bug resolved, every scope change. The analogy is a database schema: the schema reflects every migration ever applied, but it is not a migration log — it is the current truth. A living behavioral specification works the same way. It records the accumulated result of all decisions, consolidated into a current specification of intended behavior.

The critical distinction is between how a system works and what it is supposed to do. Code tells you the former — a capable reader, human or AI, can work through a codebase and reconstruct a detailed account of how each component functions. What code cannot tell you is whether any given behavior is intended. When a behavior changes, the code alone cannot determine whether that change was a regression or an improvement — only an explicit, maintained record of intended behavior can answer that question, and in an AI-driven system, that record must be machine-readable and current.

The natural structure for such a specification is one practitioners already know: behaviors organized into stories, grouped into logical capability areas, each story backed by acceptance criteria, each acceptance criterion verified by an executable test against the running code. The operational grounding is what distinguishes a living specification from documentation. A document can diverge from the system silently; a specification tethered to executable tests cannot — the tests fail the moment the code deviates from the stated intent.

Maintaining behavioral identity as a living artifact requires more than keeping it current. A specification can be up-to-date and still fail as a source of truth if it is internally inconsistent, incomplete, or redundant. For behavioral identity to function reliably — especially as a substrate for autonomous decision-making — it must exhibit four properties:

- **Consistency**: The specification does not contradict itself. Behavioral requirements at every level must be mutually compatible. A source of truth that contains contradictions cannot adjudicate between them.

- **Coverage**: Every layer of the specification covers its parent. Gaps in coverage are gaps in the source of truth.

- **Exclusivity**: Behavioral descriptions are disjoint. Overlap creates ambiguity about which specification governs a given behavior — and ambiguity undermines the source of truth.

- **Balance**: The specification graph has appropriate spread. Stories are similar sized with similar numbers of ACs. 

These properties cannot be maintained by humans alone as a system scales. They must be checked automatically, as a continuous integrity condition on the living artifact itself.

A governed generative development framework must therefore maintain behavioral identity as a living artifact: updated automatically as intents are applied, reflecting the current accumulated state of intended behavior. This is what makes it possible for an autonomous system to resolve a failing test — whether a change is a regression or an improvement is a question the source of truth can answer.

Behavioral identity has a further property that becomes apparent only when the specification is externalized: it makes trustworthiness demonstrable rather than merely asserted. When behavioral intent lives only in the minds of the people who built the system, it cannot be inspected or audited by anyone outside those conversations. An externalized behavioral specification — human-readable, independent of any model session, open to inspection by anyone — is what makes it possible to demonstrate that a system behaves as intended, not merely to believe it. In AI-driven development, where no human has reviewed every line of code, this accountability layer is not optional.

### 5. The Software Artificer: A Role for the New Development Paradigm

This shift in how software is produced implies a corresponding shift in the human role. We propose a title for this role: the Software Artificer — borrowed from the medieval craftsperson who directs a skilled workshop rather than wielding every tool personally. This is neither a "programmer assisted by AI support" nor a product manager.

Behavioral identity is what makes this oversight role tractable. With an explicit, maintained specification, the Artificer can reason about product decisions, validate outcomes against stated intent, and hand context to new collaborators or new AI sessions — rather than reconstructing intent from code alone.

The SA is an oversight role. They steer the end-to-end software development process. They have overall responsibility for product delivery and are more like a front-line engineering manager than a developer. The job breaks down into three main areas:

- **Decision ownership at boundaries.** The SA owns: when an intent development starts; prioritisation and the specification readiness; whether the result actually meets the original intention; the definition of "Done"; when direction changes are required.

- **Validation beyond what machines can fully own**, especially: experiential validation (running the system, "does this feel right?"); product validation (does this solve the user problem?); business validation (does this solve the business problem?).

- **Interfacing with the real world.** Cloud accounts, org constraints, legal, users, costs — the SA bridges those into the system _as constraints_.

#### Zones of Responsibility

In this new model of software development, we identify three zones of responsibility which can be thought of as concentric circles. The core is the software under development and its immediate tests and documentation. This is the domain of the AI. The SA has visibility and oversight into this area but is not typically working in this space directly.

The First Halo surrounds the core and is the primary domain of the SA. It includes validation of the overall user experience, decisions about and management of external systems like cloud platforms that the system would interface with, or app deployment. This area also includes aspects like hardware, system performance, and security — aspects where the AI may be involved but is out of its core strength. User experience is an obvious example where the AI can flounder. Setting up accounts with cloud systems, making the final decisions about third-party dependencies — these are all places where the AI can contribute, discuss trade-offs, and so on, but are really the realm of the Software Artificer.

The Second Halo is the domain of the human business systems around the development process. This includes defining business goals and constraints, the interface to product management teams, legal and regulatory compliance, and any other human systems. The development process needs to operate with awareness that this context exists, but all interface to it is via the SA.

As models improve, the role of the Artificer will become less technical and more managerial. A single SA will be able to oversee more and more development projects. Ultimately it may become a role combined with another function such as product management.

---

The framework described here — behavioral identity as a living, operationally-verified artifact, governed by automated process infrastructure, overseen by a Software Artificer — is not theoretical. A companion paper describes nine months of building a production platform using these principles, and reports what the data shows.

---

## References

[1] Karpathy, A. X (Twitter), 2 February 2025. https://x.com/karpathy/status/1886192184808149383

[2] Karpathy, A. _Sequoia Ascent 2026 summary._ 30 April 2026. https://karpathy.bearblog.dev/sequoia-ascent-2026/

[3] _81% of Enterprise Technology Leaders Report Production Failures from AI-Generated Code, New Research Shows._ GlobeNewswire, 19 May 2026. https://www.globenewswire.com/news-release/2026/05/19/3297549/0/en/81-of-Enterprise-Technology-Leaders-Report-Production-Failures-from-AI-Generated-Code-New-Research-Shows.html

[4] Fiaz, A. _The $30,000 Technical Debt Trap: Why 73% of AI-Built Startups Fail to Scale._ Medium, September 2025. https://medium.com/@ahmadfiazjan/the-30-000-technical-debt-trap-why-73-of-ai-built-startups-fail-to-scale-7c81ce4602f9

[5] Osmani, A. _The 80% Problem in Agentic Coding._ Substack. https://addyo.substack.com/p/the-80-problem-in-agentic-coding

[6] _The AI Productivity Paradox._ Faros AI, 2025. https://faros.ai/ai-productivity-paradox

[7] _Early 2025 AI Experienced Open-Source Developer Study._ METR, 10 July 2025. https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/

[8] Shen, J. H. and Tamkin, A. _How AI Impacts Skill Formation._ arXiv:2601.20245, January 2026. https://arxiv.org/abs/2601.20245

[9] Li, J., Wu, Y., and Chang, Y. _ClarEval: A Benchmark for Evaluating Clarification Skills of Code Agents under Ambiguous Instructions._ arXiv:2603.00187, March 2026. https://arxiv.org/abs/2603.00187