---
uid: decision-edf40036
id: DECISION-11
type: decision
title: Stop patching the permissions layer; redesign the schema so a role cannot express
  a path
created_by: xgd
created_at: '2026-08-19T18:10:10.971232+00:00'
updated_at: '2026-08-19T18:10:10.971232+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-08-18'
  rationale: 'Three rounds of fixes had been built on a model that turned out to be
    wrong. The design assumed two independent enforcement layers - a soft tool-permission
    layer (WHAT) and a hard kernel backstop (WHERE) - and 2026-08-18 proved live that
    they are not independent in either direction: Edit(...) deny patterns are merged
    by Claude Code into the OS-level denyWrite list, and Seatbelt never confines the
    Edit tool at all. So for Bash the two layers leak into each other, and for Edit
    there is only one layer. The root cause was structural rather than incidental:
    WHAT and WHERE were conflated in the config schema, so every fix had to be authored
    three times by hand and each copy could drift. The judgement was to stop fixing
    instances and rebuild the schema so that a role is exactly (where, what) - an
    enum naming a directory-space, and a tool list with no path specifiers - making
    the conflation structurally unrepresentable rather than merely discouraged.'
  caused:
  - goal-959f56f3
---

## The situation

By 2026-08-18 the access-control work had been through the six-ticket cluster (decision-9a363d88), the feature-flag turn, and three separate rounds of sandbox fixes. Each round had been declared done and each had been followed by another kernel denial that should not have been possible.

The reason was that everyone - including the design document - believed something false about the mechanism.

## What was actually true

DOC-981 records the two discoveries as separate corrections, which is why it took two passes to see:

- **s10.1** - WHAT-layer `Edit(...)` deny patterns do not stay in the WHAT layer. Claude Code merges them into the OS-level `denyWrite` list, so a tool-permission rule silently becomes a kernel rule governing Bash subprocesses too. Handled at the time by adding exclusions.
- **s11** - the reverse, and the one that broke the model. Seatbelt does not confine the Edit tool at all. Confirmed live with a clean single-variable test against the one file with WHERE protection and no WHAT protection: the Edit tool appended a line and succeeded with zero resistance; restoring the same absolute path via Bash `cp`, same session, same moment, got a kernel `EPERM`; Edit reverted it and succeeded again.

Operator: *"seatbelt and claude permissions are not two separate layers... we had to realize this twice - once that deny applied, and the other that include could expand the space."*

**The consequence:** the defence-in-depth claim REQ-796 was written to make - a declared schema backed by a hard OS boundary - is only true for Bash. For the Edit tool, the soft layer is the only layer. That is not a shortfall in the implementation; it is the opposite of what the architecture claimed.

## The alternatives

**Keep patching.** Each round was individually cheap and had a plausible story. But three rounds had already been declared done on a wrong model, and there was no reason to expect a fourth to be different - the failures were not converging.

**Accept the asymmetry and document it.** Defensible, and much cheaper. Rejected because the whole point of this goal is a claim about auditability, and "the boundary holds against Bash but not against the agent own edit tool" is not a claim worth making to a beta user.

**Rebuild the schema.** Taken.

## What tipped it

The three-copies finding. Governance-file protection existed in three independently hand-authored places - `session_roles.yaml`, `launch_spec.py`, `sandbox_policy.py` - each covering a different subset, in different pattern forms, with different anchors. That is not a set of bugs, it is a schema that makes correctness unrepresentable. A fourth patch would have become a fourth copy.

The operator correction that settled the shape went further than the first proposal: even storing `(included, excluded)` per role was rejected as "one level too concrete" - two independently-authorable lists per role reintroduce the same mixing one layer up. The final model is that a role names a `where` enum and a `what.tools` list, and **paths are structurally unrepresentable in a role config at all**. `directory-spaces` is the only place includes and excludes exist, as the definition of the named level itself.

## What it cost and what it bought

**Cost:** REQ-806 rewrote the schema, migrated `session_roles.yaml` and `.xgd/permissions.yaml` and its template, rewired `sandbox_policy.py`, `launch_spec.py`, `prompts/catalog.py` and the dashboard tile, and updated ~25 test files. On top of roughly seven repair tickets already spent on the cluster.

**Bought:** one compiler function replacing three hand-maintained copies; 519 tests green across the affected surface; a schema where the class of bug that produced BUG-1192, BUG-1194 and BUG-1198 cannot be authored. It also created the slot that the two remaining axes - `excluded_commands` and the network sandbox (REQ-808) - can hang off, rather than accreting beside the design the way the first three rounds did.

## A note on how this was found

Worth recording separately: the live single-variable test in s11 is what settled it, and REQ-802 (`xgd test-workflows --report-test N`) was built in the same period specifically so this class of thing can be reproduced on demand. REQ-796 own record admits its required live acceptance check was never run before two of its rounds were declared fixed - which is how a reproducible gap survived three fix cycles. The harness is the durable fix for that, and it is cheap insurance against the next wrong model.