---
uid: decision-ae52db2f
id: DECISION-13
type: decision
title: 'Split the payer from the tenant: one account operates several businesses'
created_by: xgd
created_at: '2026-09-03T02:28:29.139041+00:00'
updated_at: '2026-09-03T02:28:29.139041+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-09-02'
  rationale: An account is the payer; a business is the unit of isolation and owns
    exactly one site in v1. Collapsing the two made a second user impossible - two
    people logging in landed in the same tenant. Splitting them now, while identity
    is being built for the first time, is far cheaper than splitting them after real
    accounts exist.
  caused:
  - ticket://lagrangefoundry/1stcontact/REQ-178
  - ticket://lagrangefoundry/1stcontact/REQ-179
  - ticket://lagrangefoundry/1stcontact/REQ-180
  - ticket://lagrangefoundry/1stcontact/REQ-181
  - ticket://lagrangefoundry/1stcontact/REQ-168
  - ticket://lagrangefoundry/1stcontact/REQ-170
---

## What changed

The product had one level where it needed two. DOC-40 (Identity, Accounts & Entitlement) now names four nouns and separates the two that were fused:

- **Business** - the unit of isolation, spelled tenant in the schema and Business in the product. Owns a website (v1: exactly one), a customer list, a calendar, payments, marketing, monitoring, and the knowledge the assistant accumulates. It is the hard information barrier; nothing reaches across it.
- **Account** - the payer, and *not* a tenant of its own. One account may own several businesses.
- **User** - a person, a verified email, scoped to a tenant.
- **Membership** - the join that says this person may operate that business.

DOC-40 records that an earlier draft said *Account - a tenant*, collapsing two levels into one. This is the correction.

## Why it was decided now rather than later

Until this week the builder served exactly one operator. apps/control-app named its tenant in a deployment var, Cloudflare Access gated the hostname, and the Worker re-verified the Access JWT. That is a complete design for **one** user with no room for a second - two people logging in would land in the same tenant and edit each other sites. Nothing persisted about a person at all: Access proved an email on every request and stored nothing.

So identity had to be built before the class cohort could be onboarded, and the moment you build identity you have to answer whether the payer and the tenant are the same object. The operator answer is that they are not.

The deciding argument is that the split is nearly free today and expensive later. REQ-178 found the assumption baked into exactly **one** place in shipped code - accountFor() returning a single account id, and Admission carrying it singular. Everything else already had the right shape: memberships (user_id, account_id) was always a join, account_id always held a tenant id, and provisionInvite already wrote the builder user into the platform own tenant with the business as a separate tenants row. The design had been drifting toward this for a while; the code just had one sentence that had not caught up. After real accounts exist, the same change is a data migration across live tenants.

Lagrange Foundry is its own worked example: one account holding *Lagrange Foundry*, *1st Contact* and *XGD* - three businesses, three websites, three customer lists, and three assistants that know nothing of each other.

## What was deliberately not decided

**Multiple sites per business.** v1 is one site per business, and REQ-181 (badge the exception, not the rule) encodes that as a UI stance rather than a schema constraint. The operator position is that this may open up at some future point but not today. Worth noting the asymmetry: the account-to-business split was taken early precisely because it is cheap now, while the business-to-site split was deferred on the same kind of reasoning inverted - it is not needed yet and the shape is not settled.

**Payments.** DOC-40 stops at what access does this account have, and why. The money that produces some of those answers is a separate concern.

## Consequence for denial, which is the visible behaviour change

Admission returns the *set* of businesses an account may operate, each with its own entitlement. ok stays a property of the person; what varies per business is access. Today a single lapsed entitlement denies the person - with several businesses that is wrong, because an account whose second business has lapsed must still reach the first.

## Why this is on the log

Two of the guide signatures at once: a subtree appeared fully formed (REQ-167 through REQ-181, plus DOC-40, filed 09-01 and 09-02 with no prior aspiration on the map), and the shape of the product changed materially. The vocabulary change alone - Business as a product-facing noun, distinct from account - will read as arbitrary in six months without this record.