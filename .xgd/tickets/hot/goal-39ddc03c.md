---
uid: goal-39ddc03c
id: GOAL-46
type: goal
title: Chat transcript storage is durable
created_by: xgd
created_at: '2026-08-08T17:40:56.661301+00:00'
updated_at: '2026-08-14T21:03:27.177880+00:00'
completed_at: null
last_field_updated: children
status: aspiration
fields:
  provenance: bug
  children:
  - goal-c54b83e0
  - ticket://lagrangefoundry/lagrange-framework/BUG-28
  - ticket://lagrangefoundry/lagrange-framework/BUG-24
  - ticket://lagrangefoundry/lagrange-framework/BUG-23
  - ticket://lagrangefoundry/lagrange-framework/REQ-96
  - ticket://lagrangefoundry/lagrange-framework/REQ-72
  - ticket://lagrangefoundry/lagrange-framework/BUG-5
  - ticket://lagrangefoundry/xgd/BUG-967
  - ticket://lagrangefoundry/xgd/BUG-1020
  workstream: true
---

Session transcripts survive a dashboard restart, reliably.

Operator assessment on 2026-08-08: transcript storage is flaky, and it was flaky enough on 2026-08-07 to prompt a deliberate test - a turn was sent purely to generate content, then the dashboard restarted to check whether it survived.

Why this is not cosmetic: this interface exists to supply recall the operator does not have. A transcript that loses turns is the failure of the one thing the product promises. It also destroys the audit trail that the accountability whitepapers rest on.

A concrete instance from 2026-08-07: the evening consolidation sweep read roughly 90 tickets across three project stores. All of that evidence lived only in session context - it was never written to the transcript or the map, and two operator interruptions meant it produced no visible assistant text either. Had the session dropped, the work would have been lost entirely with no trace that it had happened.

Related: BUG-967 in xgd (chat session permanently fails to resume with No conversation found after a workspace-trust failure) and BUG-933 (Goals tab not resuming session).

Tracked by ticket://lagrangefoundry/lagrange-framework/REQ-72 - Chat sessions: durable store review, multi-writer streaming, stop, and mid-turn prompts - filed 2026-08-08, still draft. State is aspiration rather than in_progress: wanted and filed, but no work started and no date set.