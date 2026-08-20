---
uid: comment-7b12fb19
id: COMMENT-17
type: comment
title: Comment on goal GOAL-50
created_by: xgd
created_at: '2026-08-20T01:08:15.940066+00:00'
updated_at: '2026-08-20T01:08:15.940066+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-959f56f3
  kind: note
---

**2026-08-19 evening sweep. The core is done. One gap disagrees with itself and it is the one that bites tomorrow.**

Operator: *"Most of the day today was spent on access controls, I think we have everything we need. I anticipate bugs and the UI is UGLY but we can refine over time."*

## What landed today

- **REQ-806** (the (where, what) redesign) - `ready_to_reconcile`.
- **REQ-807** (deny-Edit the whole installed distribution root) - `ready_to_reconcile`. It was `draft` this morning. Filed, scoped and closed inside a day.
- **BUG-1132** (goal map collapses every non-terminal ticket status to in_progress) - `ready_to_reconcile`. Answered at 16:04, implemented by evening.
- **BUG-1202** - the 1stcontact-originated report that the sandbox blocks all socket binding, so 22% of that suite cannot run in-session. Added `network` and `mach_lookup` toggles to the schema and compiler. `ready_to_reconcile`.
- Plus BUG-1206, BUG-1209, BUG-1210, BUG-1211, BUG-1212, BUG-1213, BUG-1214, BUG-1215, BUG-1216 - `xgd` moved 0.15.306 to 0.15.322 across the day.
- **DOC-981 was rewritten.** It went from a 17-section running journey record into a design document: three axes (WHAT / WHERE / ESCAPE) with one compiler, the final schema, the live configuration, and an explicit known-gaps section. The journey is preserved as an appendix ticket log. That is the artifact that makes this handoverable, and it did not exist this morning.

## The disagreement worth resolving before tomorrow

**DOC-981 s8 and the ticket store contradict each other, and the contradiction sits exactly on the network sandbox.**

DOC-981 s8 (written today) says:

> **Network egress control (REQ-808, `draft`) - not implemented.** BUG-1202 added the `network`/`mach_lookup` toggles to the schema and compiler, and both are live-`on` for this project interactive role today, but **neither has been live-verified against a real sandboxed launch**... This is the blocker for 1stcontact network-dependent UAT suite and needs a real allowed-domain-reachable / disallowed-domain-refused regression test via REQ-802 `--report-test` harness before it can be trusted.

The ticket store says REQ-808 is **abandoned**, and REQ-809 (process/spawn confinement, which s8 also lists as `draft`, scope undecided) is **legacy_done**. Neither carries a resolution note. Both were created this morning as drafts, which makes a bulk draft-cleanup sweep the likeliest cause - CHAT-143 is titled "Clean up of draft bugs and reqs".

**Why this matters rather than being bookkeeping:** BUG-1202 built the mechanism, but the design doc is explicit that the mechanism has never been live-verified - and REQ-796 own history is the argument for taking that seriously, since three rounds were declared fixed there without the live check ever running. The remaining work is the verification, and the ticket that held it is closed. BUG-1208 is the symptom already showing up: `playwright install chromium` hangs indefinitely under `allowedHosts: []`, no error, no timeout.

**Recommendation, and it is a genuine choice:**

- **(a)** Re-open REQ-808 scoped down to just the live verification, and keep this goal `in_progress` until it passes. Honest, and it keeps the 1stcontact blocker visible.
- **(b)** Split network egress out into its own goal, and declare *this* goal `realized` today with a `completed_date` of 2026-08-19. The (where, what) redesign, the distribution-root deny and the audit trail genuinely are done, and they should be credited as done rather than held hostage to a fourth axis that was always scoped as separate.

I lean (b). The thing you set out to build is finished; network egress is a different axis that got pulled in by a 1stcontact deadline, and keeping it inside this goal makes a completed piece of work read as unfinished for weeks.

## The other two open gaps, for completeness

Both from DOC-981 s8, neither urgent: BUG-1201 (`fix_structural_validation` and some fix-loop prompts still lack `xgd ticket create`) and BUG-1215 (dashboard-launched sessions have no persisted permission-audit trail - the resolution is correct, but the dashboard never calls `configure_global_logger()` at startup so the records are generated and dropped). BUG-1215 is `ready_to_reconcile` already.

## On the ugly UI

Recorded, not argued with. BUG-1203 (Allow Any Command switch) and BUG-1212 (permissions tile blocking on redundant cross-project git sweeps) both landed today, and REQ-803 renamed the tile. The tile works and is unlovely - which is the correct order to do those in.