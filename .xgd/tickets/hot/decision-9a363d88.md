---
uid: decision-9a363d88
id: DECISION-10
type: decision
title: Ship the access-control rewrite behind config flags rather than hold it on
  a branch
created_by: xgd
created_at: '2026-08-17T21:13:17.746505+00:00'
updated_at: '2026-08-17T21:13:17.746505+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  decided_at: '2026-08-17'
  rationale: 'The permissions rewrite had grown to a six-ticket cluster sharing one
    branch (free-REQ-796), and on 2026-08-16 it broke everything downstream of it
    - the filesystem perimeter guard regression (BUG-1142) cascaded into BUG-1154,
    BUG-1159 and a failed reconcile bundle, and cost a full day of reconstruction.
    Holding it on a branch until it was safe everywhere meant the blast radius kept
    growing while the branch aged. REQ-801 inverted that: the behaviour became runtime-switchable
    (claude_code.headless_permission_mode, headless_sandbox_enabled, and xgd test-workflows
    --bypassPermissions/--os_sandbox), so the cluster could merge into xgd-working
    the next day with the risky path defaulted off rather than merged in. The same
    change collapsed free_code into interactive, removing a whole second code path
    as the price of the flag.'
---

## The situation

By 2026-08-16 the access-control rewrite (goal-959f56f3) was six tickets deep on a single branch, `free-REQ-796`: REQ-796 (the OS sandbox base), BUG-1142, BUG-1154, BUG-1143, BUG-1144 and REQ-801. It was not a feature waiting to merge, it was a subsystem.

And it broke. REQ-796 sandbox machinery introduced a regression in `compute_filesystem_perimeter` that resolved silently to a nonexistent path (BUG-1142); the fix for that rejected every project primary checkout (BUG-1154); the guard broke four test fixtures (BUG-1159); reconcile sessions could not take main ticket-index lock (BUG-1144); reconcile BUNDLE-2 failed outright on 08-16 at 20:23 (BUG-1157, closed wont_fix). Operator, 2026-08-17: *"yesterday was horrible - everything broke and it took the day to reconstruct it."*

## The alternatives

**Keep it on the branch until green.** The branch was already carrying six interdependent tickets and had needed a sync merge from `xgd-working` to stay current. Every further day of isolation increased the merge-back cost and the number of things that could only be tested in the isolated shape.

**Merge it and accept the risk.** Not available - the sandbox path was demonstrably breaking reconcile runs, and reconcile is the mechanism that promotes everything else.

**Make it switchable and merge.** What was taken.

## What tipped it

The failure mode was not the code being wrong, it was the code being unconditional. Every session, headless and interactive, went through the new path whether or not it was ready. Putting the mode and the sandbox behind config made "is the sandbox on" a per-run choice instead of a per-branch one, which meant the cluster could land on `xgd-working` (commit 47c790dadf46, 2026-08-17) with the risky path defaulted off, and the remaining Seatbelt problem could be chased on main rather than on an aging branch.

## What it bought and what it cost

**Bought:** a merged cluster instead of a diverging branch; `xgd test-workflows --bypassPermissions/--os_sandbox` as a first-class way to run the workflow test suite with and without enforcement; the collapse of `free_code` into `interactive`, which removed a role, a CLI mode and a code path rather than adding a flag on top of them.

**Cost:** two configuration switches that are now a supported surface, and the fact that "sandbox on" is no longer the only shape the system runs in. The CLAUDE.md rule against legacy modes applies here - these are deployment toggles for work in flight, not a permanent dual path, and they should come out once the Seatbelt issue is closed and the sandbox can be unconditional.

## Still open

The Seatbelt/`denyWithinAllow` problem (xgd/CHAT-142 "Permissions hell") is the reason the flag defaults where it does. It is the last thing between this goal and done.