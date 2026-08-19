---
uid: comment-ff012c9d
id: COMMENT-15
type: comment
title: Comment on goal GOAL-43
created_by: xgd
created_at: '2026-08-19T18:38:25.906749+00:00'
updated_at: '2026-08-19T18:38:25.906749+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-61027b65
  kind: note
---

**2026-08-19 - operator reports the in_progress saturation again, unprompted: *"I am still seeing lots of tickets as in_progress when I know they are not."* This is xgd/BUG-1132, filed 2026-08-16, severity high / priority high, and STILL `draft` three days later. Noted here because comments cannot be written cross-project from this map.

The two intervening days made it worse, not flat. Counting only tickets actually read during today sweep - not exhaustive - at least 29 sit at `ready_to_reconcile` right now, meaning done and awaiting machinery:

- xgd: REQ-781, REQ-796, REQ-802, REQ-803, REQ-804, BUG-1144, BUG-1154, BUG-1160, BUG-1165, BUG-1166, BUG-1175, BUG-1185, BUG-1190, BUG-1194, BUG-1195, BUG-1196, BUG-1198
- 1stcontact: REQ-141, REQ-143, REQ-144, REQ-145, REQ-147
- lagrange-framework: BUG-32, BUG-33, REQ-97, REQ-98, REQ-99, REQ-100, REQ-101

Under the current projection none of that can register as progress. `realized` holds at 2 goals out of 65 while ~30 finished pieces of work are invisible to the register that is supposed to be monotonic.

BUG-1132 secondary observation also re-confirmed today: goal-959f56f3 still reports `leaves: []` in on_deck, so a workstream ~25 tickets deep with a target date six days past offers nothing actionable.

**The open question at the foot of BUG-1132 has never actually been put to the operator**, and it is what blocks implementation: should `ready_to_reconcile` project to `realized`? Put to them directly today. Their answer decides whether this is a one-line mapping change or needs a new visual treatment for "operator-done, machine-pending".