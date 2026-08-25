---
uid: comment-cad36031
id: COMMENT-33
type: comment
title: Comment on goal GOAL-66
created_by: xgd
created_at: '2026-08-25T05:39:53.041861+00:00'
updated_at: '2026-08-25T05:39:53.041861+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-aa268eb1
  kind: note
---

**2026-08-24 evening - promoted to a named priority, and the framing sharpened.**

The operator listed this fourth of four next priorities: *"Create some new docs on how xgd is used today."* Marked xgd/GOAL-12 a workstream on that basis so it appears in On Deck rather than competing from memory.

## "How xgd is used today" is a narrower and better brief than the one I filed

When I created this goal on 08-19 the open scoping question was *what does a beta user actually need* - install-to-first-ticket, the workflow model, the branch topology. That framing is about a hypothetical reader.

The operator phrasing is different and more tractable: **as used today**. That is a description of a system whose behaviour is known, written from the actual current practice rather than from an idealised model of it - and it is the kind of document that can be drafted from evidence rather than invented.

It also implicitly dates the artifact. "How xgd is used today" admits that today is not last month: the free-coding lifecycle, the overlay ticket store, the (where, what) permissions schema and the goal map are all recent enough that any older description is wrong. A doc written now is a snapshot, and saying so is more honest than pretending to permanence.

## The one artifact that already works this way

DOC-981 - rewritten 08-18 from a 17-section running journey record into three axes, one compiler, current schema, live configuration, known gaps, with the journey preserved as an appendix. That is the template.

**And it demonstrates the failure mode too:** its s8 still records network egress as "not implemented" and "never live-verified", which stopped being true on 08-19. The section a newcomer reads to learn what is unfinished went stale within a day. Any doc written under this goal needs an answer to who updates it and when, or it inherits that problem by default.

## Interaction with priority 3

xgd/GOAL-8 (knowledge management in xgd) is priority 3 and this is priority 4, which is the right order if - and only if - the KB is going to hold this documentation. The scoping question from 08-19 still stands and is now urgent rather than theoretical: **if the shipped KB becomes a first-class artifact, user-facing docs and session-priming knowledge may be one corpus with two readers.** Writing the docs first and the KB second risks writing them twice.