---
uid: goal-d5e96abe
id: GOAL-48
type: goal
title: XGD packaging v1 - install tool
created_by: xgd
created_at: '2026-08-08T22:54:00.879209+00:00'
updated_at: '2026-08-16T01:12:16.481550+00:00'
completed_at: null
last_field_updated: status
status: realized
fields:
  provenance: planned
  target_date: '2026-08-20'
  children:
  - ticket://lagrangefoundry/xgd/REQ-759
  - ticket://lagrangefoundry/xgd/REQ-761
  - ticket://lagrangefoundry/xgd/REQ-755
  - ticket://lagrangefoundry/xgd/REQ-756
  - ticket://lagrangefoundry/xgd/REQ-754
  workstream: true
  completed_date: '2026-08-15'
---

An install path that a first-time user can walk through, end to end, without the author sitting next to them.

## REALIZED 2026-08-15 - and ahead of its date

Target was 2026-08-20, set by the n=1 onboarding. Complete on 08-15, five days early. Operator: "The v1 packaging tool is complete."

All five components are at `ready_to_reconcile` or beyond, which the operator has directed be treated as done:

- xgd/REQ-759 - install/install.sh bootstrap installer plus documented install command.
- xgd/REQ-761 - serve install.sh at xgd.dev/install/install.sh via Cloudflare.
- xgd/REQ-755 - ./bin/build release-packaging script.
- xgd/REQ-756 - ./bin/deploy release-publishing script.
- xgd/REQ-754 - xgd update command.

Someone can now be pointed at a URL, run one command, and end up with a working install that can update itself.

## What was deliberately excluded

The min_required_version forced-update gate moved to its own goal (goal-fbb64cd0). The tool ships and updates; *enforcing* an update is a separate capability and not needed for v1.

## History worth keeping

This work was invisible to the map until 2026-08-08. It existed as three drafts filed under an ergonomics goal, with nothing recording that an install tool sat on the critical path for a dated commitment - the operator had to say it out loud for it to surface. Seven days later it is the second goal on this map to reach realized.

It is also the first dated commitment on this map to be met early.