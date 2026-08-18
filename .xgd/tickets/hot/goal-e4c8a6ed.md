---
uid: goal-e4c8a6ed
id: GOAL-67
type: goal
title: '1stcontact: email capture, user portal and CRM Lite'
created_by: xgd
created_at: '2026-08-18T20:03:27.872049+00:00'
updated_at: '2026-08-18T20:03:27.872049+00:00'
completed_at: null
last_field_updated: created_at
status: aspiration
fields:
  provenance: planned
  workstream: false
  depends_on:
  - goal-198516d1
  children:
  - ticket://lagrangefoundry/1stcontact/GOAL-10
  - ticket://lagrangefoundry/1stcontact/GOAL-4
---

The first modules that make 1stcontact a product a small business pays for rather than a site generator.

Named by the operator on 2026-08-18: *"1stcontact will need to add email capture modules, user portals/login and basic crm/user management - that is next."*

## Why this is a goal and not a note

It is the answer to "what is after the launch", and until now the only thing on the map after the workerd migration and the site builder was goal-3d5965fb (1stcontact commercial launch), sitting at `concept` with four cross-project children and no statement of what the first increment is. This names the increment.

## The three

- **Email capture modules.** The behaviour that turns a rendered site into something that produces leads. Closest existing work: 1stcontact/REQ-148 (behavior modules render in workerd, contact-form precompiled) - the mechanism exists in the migration, the module set does not.
- **User portal and login.** 1stcontact/GOAL-10. DOC-4 lists magic-link auth.
- **Basic CRM / user management.** 1stcontact/GOAL-4. "CRM Lite" in DOC-4 MVP scope.

## Sequencing

`depends_on` goal-198516d1 (workerd migration), not `children` of it. These are new capability, not part of the platform move - but they should be built on the Cloudflare platform rather than ported to it afterwards, which is precisely the argument that justified doing the migration early (decision, 2026-08-15: *"many things differ in the cloud, and building the CX on a laptop means developing against a comfortable illusion"*). Building the first revenue-bearing modules on the laptop and moving them later would spend that decision value.

## What it gates

The site builder (goal-1a5a8d2b) proves 1c can produce a site. These three are what decide whether the site earns anything - they are the first revenue-bearing modules, per the sequencing already recorded on the Site builder goal ("alpha website first, then those two").

Held at `aspiration`: named and wanted, no date, no tickets, no work started. It should not compete with the class-cohort deadline (2026-08-31) for attention until the builder has actually been used to build the few sites the operator plans.