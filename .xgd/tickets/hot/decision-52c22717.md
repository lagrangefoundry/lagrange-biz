---
uid: decision-52c22717
id: DECISION-2
type: decision
title: Extract lagrange-framework as reusable components from XGD
created_by: xgd
created_at: '2026-08-06T21:23:56.802742+00:00'
updated_at: '2026-08-06T21:23:56.802742+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-07-07'
  rationale: Components worth reusing across projects were trapped inside XGD. Extraction
    made them available to 1stcontact and any later project, at the cost of a third
    codebase to maintain.
  caused: []
  deferred:
  - goal-af871b76
---

Pull the reusable pieces out of XGD into a separate project (lagrange-framework) so other projects can use them.

**Date from evidence:** first commit in the lagrange-framework repository, 2026-07-07.

**Consequences.** A third project competing for the same single bottleneck — operator attention. It also created the outstanding refactor to reintroduce LF components into the XGD UI, which remains unstarted and is explicitly not beta-gating.

**Note:** lagrange-framework is **not** intended to be open-sourced. That leaves the open-source discovery funnel without an owner (GOAL-30).