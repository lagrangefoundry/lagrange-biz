---
uid: decision-46593d49
id: DECISION-7
type: decision
title: Build AI tooling as a reusable configurable component, not a per-surface custom
  solution
created_by: xgd
created_at: '2026-08-08T23:48:35.417064+00:00'
updated_at: '2026-08-09T00:02:41.144973+00:00'
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

## Cost

Five REQs filed in framework at 14:13 local (REQ-73 through REQ-77) plus DOC-13 and DOC-20 written - design done, none of it built yet; all five still draft.

**This did not come out of the packaging work.** Packaging advanced substantially the same day: REQ-755 (./bin/build) and REQ-756 (./bin/deploy) reached ready_to_reconcile at 13:49 and 14:00, REQ-759 (install/install.sh bootstrap installer) at 16:45, and REQ-761 (serve install.sh at xgd.dev via Cloudflare) went free_coded at 16:49. The installer exists and is served; only the update path (REQ-754, REQ-763) remains. An earlier version of this record listed packaging as deferred and described its tickets as untouched. That was wrong - it was drawn from an enumeration that stopped at REQ-758 and missed everything filed after it.

What did not advance: Site builder (target 2026-08-31), untouched since 2026-08-06.

## On the infrastructure-versus-deliverable framing

This is the second decision in two days routing effort into foundations - see decision-c9de87f9 (2026-08-07, operator ergonomics and packaging). Recording that pattern is useful; reading it as a detour is not, and the operator pushed back on exactly that.

The leverage is not incidental, it is structural. The chat infrastructure being fixed is simultaneously (1) the interface this planning conversation runs in, (2) the operator constant tool for building everything else, and (3) the primary interface of the website builder itself - the dated 2026-08-31 deliverable. Work on it is not taken *from* the site builder; a substantial part of it *is* the site builder. The tooling object sits one layer below that, gating what every AI surface may touch.

The honest frame is compounding rather than trade-off. Two registers, not one: foundations are accumulation - they do not decay and every later surface is cheaper for them existing - while only genuinely displaced work counts as distance. The record should note where effort went without implying it was misspent.