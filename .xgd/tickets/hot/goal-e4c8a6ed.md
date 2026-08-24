---
uid: goal-e4c8a6ed
id: GOAL-67
type: goal
title: '1stcontact: email capture, user portal and CRM Lite'
created_by: xgd
created_at: '2026-08-18T20:03:27.872049+00:00'
updated_at: '2026-08-24T22:25:12.514369+00:00'
completed_at: null
last_field_updated: children
status: aspiration
fields:
  provenance: planned
  workstream: false
  depends_on:
  - goal-198516d1
  children:
  - ticket://lagrangefoundry/1stcontact/GOAL-18
  - ticket://lagrangefoundry/1stcontact/GOAL-10
  - ticket://lagrangefoundry/1stcontact/GOAL-4
---

**A sequencing statement over three goals that 1stcontact already owns.** Not a new goal - the modules themselves are 1stcontact/GOAL-18 (Email capture backend), GOAL-10 (User portal) and GOAL-4 (CRM), all filed 2026-08-06. Those are authoritative.

**Correction on the record:** when I created this on 2026-08-19 I wrote it as though these modules were unrepresented. They were - in 1stcontact, where I had not looked. Second instance of the same mistake as goal-5d987c56, and the reason the operator set the goal-placement rule on 08-24.

What this goal contributes, and the only reason it survives as a wrapper: **the ordering, and the date it was stated.**

## The operator statement, 2026-08-19

> *"1stcontact will need to add email capture modules, user portals/login and basic crm/user management - that is next."*

That sequence is not recorded in any of the three underlying goals, and it is not derivable from them. It says these three come after the platform migration and before anything else in the commercial block.

## Why the ordering matters

These are the first revenue-bearing modules - the point at which 1stcontact stops being a site generator and becomes something a small business pays for. The Site builder proves 1c can produce a site; these decide whether the site earns anything.

They should be built on the Cloudflare platform rather than ported to it afterwards, which is precisely the argument that justified migrating early (decision of 2026-08-15: *"many things differ in the cloud, and building the CX on a laptop means developing against a comfortable illusion"*). Building the first revenue-bearing modules on the laptop and moving them later would spend that decision value twice.

Held at `aspiration`: no date, and it should not compete with the class-cohort deadline (2026-08-31) until the builder has been used to build the few sites the operator planned.