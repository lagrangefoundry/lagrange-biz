---
uid: decision-46593d49
id: DECISION-7
type: decision
title: Build AI tooling as a reusable configurable component, not a per-surface custom
  solution
created_by: xgd
created_at: '2026-08-08T23:48:35.417064+00:00'
updated_at: '2026-08-09T00:03:00.772865+00:00'
completed_at: null
last_field_updated: body
status: null
fields:
  decided_at: '2026-08-08'
  rationale: Every AI surface was re-implementing tool registration, policy gating
    and validation by hand. Doing it once as a declarative configurable object should
    make every future toolset faster to add and harder to get wrong, particularly
    on the security side - but it cost most of a day that would otherwise have gone
    to the two dated deliverables.
  caused:
  - goal-9cdf5f09
  deferred:
  - goal-1a5a8d2b
  - goal-d5e96abe
---

## Situation

The AI tooling in play - ai_ticketing, ai_knowledge, the goal-map tools, the built-in filesystem toolset - each carried its own registration, its own notion of which operations and ticket types a caller may address, and its own validation. The pattern was visible but had never been named.

The immediate prompt was concrete. On this day the goal-map assistant tried to file a REQ and was refused: creating type request is not enabled for this session. The cross-project filing plumbing already existed, free_coded the day before - xgd/REQ-750 (xgd ticket create --project) and lagrange-framework/REQ-67 (xgd-cli access kind: create() for cross-project filing). Nothing was missing except a policy gate, and there was nowhere principled to put the change.

## Alternatives

- **Patch the allowlist.** Minutes of work. Unblocks the assistant immediately and leaves the fourth hand-rolled gating implementation in place, to be rediscovered the next time a surface needs different permissions.
- **Build the tooling object properly.** A declared API plus config, with projection, validation, policy gating, structural dispatch, provenance and audit in one place. Costs a day now; every subsequent toolset is configuration rather than code.

## What tipped it

Security, mostly. Tool gating decides what an AI may touch, and four hand-rolled implementations mean four places to get it wrong and no single place to audit. That argument is also the product argument: both whitepapers rest on accountability being structural rather than promised, and an AI tooling layer whose permissions are ad hoc per surface is hard to defend in a document claiming otherwise.

The secondary argument was pace. The operator adds AI surfaces often. Configuration scales with that; bespoke integration does not.

## Cost, and why it is not a trade

Design work on 2026-08-08: DOC-13 and DOC-20 written, five REQs filed in framework at 14:13 local. REQ-73 completes the design; REQ-74, 75, 76 and 77 are the build and the three refactors, expected to be built in a single pass on 2026-08-09.

**No dates slipped and none were intended to.** An earlier version of this record marked XGD packaging v1 and Site builder as deferred. That was wrong on the evidence and is corrected here.

Packaging advanced substantially the same day: REQ-755 (./bin/build) and REQ-756 (./bin/deploy) both reached ready_to_reconcile, REQ-759 (install/install.sh bootstrap installer plus documented install command) reached ready_to_reconcile at 16:45, and REQ-761 (serve install.sh at xgd.dev/install/install.sh via Cloudflare) reached free_coded at 16:49. The install tool the n=1 onboarding depends on is nearly finished, not unstarted. Only REQ-754 (xgd update) remains draft.

The site builder did not move on this day, but its long pole is product discovery rather than available time - a different thing from a date under pressure, and not attributable to this decision.

## The leverage argument

The framing of infrastructure winning over deliverables is the wrong shape, and it is worth stating why so it is not re-derived every time this pattern appears.

The chat stack being fixed is simultaneously: the interface this planning conversation runs in, the operator constant tool for building everything else, and the primary interface of the web builder product itself. One repair lands in three places. The same holds for the tooling object - ai_ticketing, ai_knowledge, the goal-map tools and the filesystem toolset are all consumers.

This is foundation, not detour. Framework work compounds across every surface, which is precisely why lagrange-framework was extracted (decision-52c22717). The honest accounting is leverage, not cost.

Related: decision-c9de87f9 (2026-08-07, operator ergonomics and packaging) is the same shape and should be read the same way.