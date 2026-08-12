---
uid: goal-c54b83e0
id: GOAL-57
type: goal
title: New chat implementation
created_by: xgd
created_at: '2026-08-12T00:14:58.277933+00:00'
updated_at: '2026-08-12T00:14:58.277933+00:00'
completed_at: null
last_field_updated: created_at
status: concept
fields:
  provenance: planned
  children: []
  workstream: false
---

Replace the current chat implementation rather than continue repairing it.

Named by the operator on 2026-08-11 as a distinct item from the ongoing chat bug-fixing.

The case for replacement rather than repair is in the record already: lagrange-framework/REQ-72 (durable store review, multi-writer streaming, stop, mid-turn prompts) is a rewrite-shaped ticket, not a fix, and transcript loss has been recurring enough that the operator has tested it by hand - sending a turn purely to generate content, then restarting the dashboard to see whether it survived.

What raises the stakes is reach. The chat stack is simultaneously the interface the goal map runs in, the operator constant tool for building everything else, and the primary interface of the website builder product. One replacement lands in three places - and one unreliable implementation fails in three places.

No tickets yet beyond REQ-72.