---
uid: goal-adac9e3a
id: GOAL-51
type: goal
title: Interface tidy-up for external use
created_by: xgd
created_at: '2026-08-11T23:44:18.243826+00:00'
updated_at: '2026-08-12T00:16:00.530186+00:00'
completed_at: null
last_field_updated: body
status: in_progress
fields:
  provenance: user_feedback
  children:
  - ticket://lagrangefoundry/xgd/REQ-777
  - ticket://lagrangefoundry/xgd/REQ-778
  - ticket://lagrangefoundry/xgd/REQ-779
  - ticket://lagrangefoundry/xgd/REQ-782
  - ticket://lagrangefoundry/xgd/REQ-783
  - ticket://lagrangefoundry/xgd/REQ-784
  workstream: false
---

**Standing goal - ongoing, confirmed by the operator on 2026-08-11: "there is more coming I am afraid."** The dashboard reads as a product rather than as a set of controls its author happens to remember. Work lands here continuously as more of the product is seen through a newcomer eyes.

Six requests filed on 2026-08-11, prompted by thinking about putting the tool in front of someone else rather than by the operator own friction. That distinction is why this is separate from XGD Remove friction: that goal is about the author speed, this one is about a newcomer being able to work out what a button does.

**Actions made explicit rather than implied:**

- REQ-777 - Intent editor: Free Code / Investigate action buttons (ready_to_reconcile).
- REQ-779 - Ticket controls: replace status-advance buttons with Develop / Ready to reconcile (free_coded). Naming the workflow step rather than the state transition - a newcomer knows what Develop means and does not know what advancing a status does.
- REQ-783 - Intent tab: batch Investigate button next to Free Code (free_coded).
- REQ-784 - Dashboard: match Develop button style to Free Code / Investigate (free_coded).

**Batch operations:** REQ-778 - batch Free Code with depends_on-aware queueing (free_coded). The same insight the goal map needed: ordering has to be respected, and depends_on is what expresses it.

**Wording:** REQ-782 - free-coding reminder mentions cutting a branch (ready_to_reconcile).

All six were built the same day they were filed.

Siblings under XGD ready for someone else hands carry the larger pieces that are not just renaming - the Design tab consolidation, state transition safety, status and configuration, and onboarding. This goal holds the continuous stream of smaller corrections.

As a standing goal it can never reach realized, so it contributes nothing to the accumulation register and sits on the list permanently. That is a known gap in the model, not a property of this work - see goal-98f48e17.