---
uid: comment-4e51fc56
id: COMMENT-20
type: comment
title: Comment on goal GOAL-50
created_by: xgd
created_at: '2026-08-20T03:13:00.478157+00:00'
updated_at: '2026-08-20T03:13:00.478157+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-959f56f3
  kind: note
---

**REALIZED 2026-08-19.** Closed on operator direction. Target was 2026-08-13; six days late, and the reason is on the record rather than lost - decision-9a363d88 (branch to feature flag) and decision-edf40036 (stop patching, redesign the schema).

## Why it closes now

The network question resolved in the direction that made the goal completable. Operator, 2026-08-19: *"the network permissions are granted, they are just network on/off right now - that is sufficient. And it is tested and working."*

That retires REQ-808, and its `abandoned` status was correct. **My scoping of that ticket was wrong** - I specified domain allowlisting, MITM proxy for TLS-terminated traffic and credential masking, drawn from REQ-796 deferred non-goal list. On/off is what the actual requirement needed, BUG-1202 built it, and the rest was capability that no one had asked for. Recording that because the abandonment reads as a dropped blocker otherwise, and it was not one.

REQ-809 (`legacy_done`) similarly folded into BUG-1214, which investigated the bypassPermissions and unsandboxed-command semantics and is `ready_to_reconcile`.

## What is actually finished

The single choke point (REQ-781), the OS sandbox (REQ-796), the feature-flagged rollout (REQ-801), the reproduction harness (REQ-802), the (where, what) redesign (REQ-806), the distribution-root deny (REQ-807), network on/off (BUG-1202), and a design document that a newcomer can read (DOC-981, rewritten today from a 17-section journey record into three axes plus one compiler, with the journey preserved as an appendix).

Roughly twenty-five tickets across three projects, from 2026-08-11 to 2026-08-19.

## Expected roll-up disagreement, and the mechanical fix

Declared `realized`, derived will read `in_progress`. This is not staleness - it is four children still at `free_coded`, all from the 08-17 cluster:

**BUG-1142, BUG-1143, BUG-1159, REQ-801.**

They are stuck for a reason recorded at the time: `xgd ticket move-to-free-coded` ancestor-of-`xgd-working` gate would have refused their SHAs while `free-REQ-796` was unmerged. That branch has since merged (`47c790dadf46`). **Re-running the gate on those four should move them to `ready_to_reconcile` and the disagreement resolves itself.** Note BUG-1161 (`draft`) - the gate SHA-superset check does not normalize short vs full SHAs - may bite when it is re-run.

Leaving the disagreement visible rather than papering over it: it is pointing at four tickets that need a command run, which is exactly what it is for.

## Not closed, deliberately

These are real and belong elsewhere, not held against this goal:

- **DOC-981 s8 is stale.** It still reads "Network egress control (REQ-808, `draft`) - not implemented... neither has been live-verified against a real sandboxed launch." That is now false. **The document did not update itself** - checked directly this evening. It needs a correction, and it matters more than an ordinary doc nit because s8 is the section a newcomer reads to learn what is unfinished.
- BUG-1180, BUG-1185, BUG-1218, BUG-1220 remain `draft` in xgd - none are access control.
- The UI is unlovely by operator assessment and that is accepted. BUG-1203, BUG-1212 and REQ-803 all landed today; refinement continues under goal-adac9e3a.