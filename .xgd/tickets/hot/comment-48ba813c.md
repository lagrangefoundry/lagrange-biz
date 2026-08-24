---
uid: comment-48ba813c
id: COMMENT-27
type: comment
title: Comment on goal GOAL-65
created_by: xgd
created_at: '2026-08-24T01:40:10.894443+00:00'
updated_at: '2026-08-24T01:40:10.894443+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-198516d1
  kind: note
---

**2026-08-24 - the app ran in the cloud. This is the milestone this goal was created for.**

Operator: *"I got REQ-149 to complete on 1st contact and saw the app running in the cloud - that was a lot of work."*

REQ-149 - **Publish in the cloud: revisions, history and rendered output without a filesystem** - is `ready_to_reconcile`. That was the hardest of the post-block requests, and it is the one that had to work for any of this to mean anything: publishing was the last thing still assuming a filesystem.

**Every one of the original eight, plus REQ-149, REQ-150, REQ-151, REQ-152, REQ-153 and lagrange-framework/REQ-103, is now at `ready_to_reconcile` or beyond.** Filed 2026-08-15 in a four-minute burst of eight requests; running in the cloud nine days later, having grown to fourteen.

Worth stating plainly because it will not feel like it: on 08-15 this was a decision to rebuild the platform sixteen days before a hard external deadline, taken on the argument that *"building the CX on a laptop means developing against a comfortable illusion."* That argument has now been paid off - the illusion was real, the migration found it, and the app runs.

## The "not quite" is one ticket, and it is well diagnosed

**1stcontact/BUG-36** - `draft`, severity high. Logging into `app.1stcontact.io` shows the boot guard rather than the builder: `GET /api/sites: 503 No tenant 1stcontact`.

Root cause is written up and is a genuinely tidy find: `apps/control-app/src/store.ts` has two ways to open the store and they disagree about a tenant that does not exist yet. `storeFor` (every read/write route) throws `UnknownTenantError`; `storeForImport` (`POST /api/import` only) calls `createTenant` first. Both read the same `TENANT_ID` from `wrangler.toml`. So the write path registers the tenant and the read path refuses it - and `bin/deploy` runs the D1 migrations but seeds no rows.

Net effect: **a freshly deployed builder is dead on arrival until an operator runs `bin/publish` from a dev machine.** The migrations did run - the `tenants` table exists and is empty, hence `UnknownTenantError` rather than a SQL error.

That is worth more than its severity suggests. A deploy that only works if a human runs a CLI afterwards is not a deployment, and it is precisely the failure a class cohort would hit first.

## Proposal: split the second block and close this goal

Four requests remain `draft` under this goal - REQ-154 (headless browser in the cloud), REQ-155 (ReferenceStore port), REQ-156 (sharp off the fidelity path), REQ-157 (the fidelity surface). All four are one theme: **native code and filesystem assumptions in the capture and fidelity pipeline.**

They are real, but they are not what this goal asked. "1stcontact runs natively on Cloudflare workerd" has happened. The fidelity pipeline moving to the cloud is a separable second block, and holding this goal open for it means a genuine milestone reads as unfinished for another week or more - the same trade already made once with network egress on goal-959f56f3, which worked.

**Recommendation:** move REQ-154 to REQ-157 into a new goal (fidelity pipeline in the cloud), keep BUG-36 here as the last item, and mark this `realized` once BUG-36 clears. Not doing it unilaterally - a `realized` on a platform migration is a claim worth the operator making.

Target date is 2026-08-21, now three days past and still unmoved. If the recommendation is taken it wants a `completed_date` instead.