# Copyright holder rollout plan

| Property | Value |
|---|---|
| Document | Rollout plan for decision D-1 |
| Status | PROPOSED (Task KOS-STD-003) |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Last Updated | 2026-11-15 |

Target headers (D-1):

- Public repositories: `Copyright (c) 2026 Kritva Robotics Private Limited.` and `SPDX-License-Identifier: Apache-2.0`.
- Private repositories (kritva-raas, kritva-enterprise-program): the same copyright line and `All rights reserved.`
- Upstream notices are never replaced.

Current state: the core, sense, mind, motion, skill, community and raas READMEs show `Copyright (c) 2026 KritvaOS`. The header lints in core, community and raas hardcode that wording. KNX-RTL-DOC-002 and the VLSI documents say `Kritva Robotics`.

## Steps per repository

1. **Transition lint.** Change the repository's header lint to accept both the old and the new holder wording. One commit; run the lint before and after.
2. **Scripted header change.** One scripted change per repository that rewrites only the holder line in file headers. Review the diff for upstream notices, which must not change. One commit.
3. **Tighten the lint.** Change the lint to accept only the new wording. One commit after step 2 is merged.
4. **README and docs.** Update the copyright line in the README and any other document that states the holder.

## Special cases

- kritva-nexus: `KNX-RTL-STD-001` is APPROVED (NX-DEC-023). Changing its header needs a change request and a new decision record, not an edit in place.
- kritva-raas and kritva-enterprise-program: use the private header. The raas SPDX line stays as it is today until the Owner says otherwise.
- kritva-mechanical: planning only (hold D-003); header change only if it holds files that carry one.

## Order

Core and community first (they share the lint design), then sense, mind, motion, skill, raas, then nexus after its decision record. Each repository goes through its own branch, pull request and commit format.

## Not decided here

The relationship between the copyright wording and the Apache-2.0 LICENSE text in each repository is still to be documented.
