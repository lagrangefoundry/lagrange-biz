---
uid: decision-c9de87f9
id: DECISION-6
type: decision
title: Spend an afternoon on operator ergonomics and packaging, twelve days out from
  n=1
created_by: xgd
created_at: '2026-08-08T17:38:59.194369+00:00'
updated_at: '2026-08-08T17:38:59.194369+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-08-07'
  rationale: 'Two days of workflow firefighting (45 tickets across 2026-08-06 and
    08-07) made the cost of friction legible: a stale dispatcher silently running
    old code (BUG-943), four separate cherry-pick finalize failures, a fix inducing
    the next bug (BUG-963 caused by BUG-952). The judgement was that onboarding an
    external user onto a platform this sharp-edged would spend an expiring opportunity
    badly, and that the ergonomics work is cheaper before the user arrives than during.'
  caused:
  - goal-973da915
---

## Situation

Eight requests opened between roughly 15:10 and 16:50 local on 2026-08-07 - REQ-749, 750, 752, 753, 754, 755, 756, 757 - with REQ-758 following the next morning. All of them operator ergonomics or packaging. None were on the ready frontier.

Running at the same time: First external user onboarded (n=1) targeting 2026-08-20, and Class cohort builds websites on 1stcontact targeting 2026-08-31. Both from decision-9d416da1, both on expiring windows that cannot be recovered.

## What preceded it

The two days before were near-total workflow firefighting: 31 bugs (BUG-933 to BUG-971) across reconcile, resync, develop and the ticket store. The pattern that mattered was not any single bug but the compounding - BUG-943 was a dispatcher zombie running two-day-old code that recreated a duplicate bundle and never loaded the BUG-936 fix, meaning fixes appeared not to work. BUG-963 was induced by the returncode check added for BUG-952.

## Alternatives

- Push straight at the site builder and the n=1 onboarding, and absorb the friction personally. Cheapest in the short run; spends the class window and the n=1 window on a platform whose failure modes are invisible to a newcomer.
- Fix only what blocks the deadlines. Hard to identify in advance - the two-day bug run showed the blockers were not predictable.
- Take an afternoon on ergonomics and packaging now.

## What tipped it

The friction is the product. XGD closed beta and the built-with-itself proof story both rest on someone other than the author being able to run this. An external user hitting a stalled reconcile with no way to file a bug from a log is not a bug report - it is a lost user, and there is only one n=1.

## Cost

An afternoon not spent on the site builder, twelve days out from 2026-08-20 and twenty-four from 2026-08-31. Nothing was formally deferred; the dated goals absorbed the time.

## Note on this record

Filed at the operator request against a default of keeping the decision log sparse. The value being protected is knowing where time went, which the accumulation register alone does not answer.