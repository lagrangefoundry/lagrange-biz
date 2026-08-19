---
uid: comment-e730b862
id: COMMENT-11
type: comment
title: Comment on goal GOAL-50
created_by: xgd
created_at: '2026-08-19T18:08:57.237685+00:00'
updated_at: '2026-08-19T18:08:57.237685+00:00'
completed_at: null
last_field_updated: created_at
status: null
fields:
  subject_uid: goal-959f56f3
  kind: note
---

**Correction, 2026-08-19 - BUG-1162 was solved, and my flag on it was wrong in substance.**

I reported yesterday that BUG-1162 was closed wont_fix with no reason recorded. The closure record is still thin, but the problem itself was solved, and the answer was bigger than the ticket: **Seatbelt and the Claude permission layer are not two independent layers at all.**

Operator, 2026-08-19: *"we can set seatbelt permissions (intended for BASH commands) but the Claude `Edit(../filespace/**)` settings override what we did and grant and deny access not just to Claude but to bash too. We had to realize this twice - once that deny applied, and added exclusions; the other that include could expand the space."*

DOC-981 records both realizations as separate corrections, which is why it took two:

- **s10.1** - WHAT-layer `Edit(...)` deny patterns are merged by Claude Code into the OS-level `denyWrite` list. A tool-permission rule silently became a kernel rule. Fixed by adding exclusions.
- **s11 (2026-08-18, BUG-1192/BUG-1194)** - the reverse, and the one that broke the model: **Seatbelt never confines the Edit tool at all.** Confirmed live on a single-variable test against the installed `session_roles.yaml` - Edit appended a line and succeeded with zero resistance; `cp` to the *exact same absolute path*, same session, same moment, got a kernel `EPERM`; Edit reverted it and succeeded again.

The consequence is the part worth keeping: the "two independent layers, WHAT is soft and WHERE is the hard backstop" framing is **only true for Bash**. For the Edit tool the WHAT-layer deny is the *only* protection that exists. That is the opposite of the defence-in-depth claim REQ-796 was written to make, and it invalidated the mental model three rounds of fixes had been built on. Not a bug in the implementation - a bug in the model.

**s12** then found the root cause was structural: WHAT and WHERE were conflated in the config schema, not merely in enforcement. **REQ-806** is the step back and redesign - a role becomes exactly two fields, `where` (an enum naming a directory-space) and `what.tools` (no path specifiers, ever). Paths become structurally unrepresentable in a role config; `directory-spaces` is the only place includes/excludes exist. Three hand-maintained copies of governance-file protection collapse into one compiler.

Status: **free_coded**, 519 tests passing, 4 commits on `free-REQ-806`, not yet merged to `xgd-working`.