# Agent and contributor rules for kritva-standard

Status: DRAFT for Owner approval. Owner and sole approver (interim): Dinesh Annayya (`dineshannayya`).

1. **The Owner decides.** AI output is advisory. A draft, proposal or passing check approves nothing.
2. **Scope.** This repository holds specifications: standards, formats, schemas, templates and the engineering contract. Planning, decisions, baselines, approvals, credit, status monitoring and project management belong to kritva-program. Do not edit kritva-program from here; write proposals in this repository.
3. **Scripts.** Scripts needed for a local commit live in the folder of the repository that commits. Program-level checks, including standard-conformance checks, live in kritva-program. This repository holds no authoritative scripts.
4. **Migrated copies.** Files under `common/` that were copied from other repositories are verbatim until a recorded change says otherwise. Record the SHA-256 when copying and verify after writing.
5. **Identifiers.** Document IDs are `KSTD-<DOMAIN>-NNN`. Never renumber or reuse an ID. Preserve identifiers in approved documents, including `KNX-RTL-STD-001`.
6. **Public boundary.** This repository is public. Do not add private rule text (for example the Nexus rule mapping), credentials or private infrastructure detail.
7. **Honest status.** Do not mark a document APPROVED without a recorded approval. Do not present software checks, calculations or simulation as physical or safety validation.
8. **Copyright.** New files use `Copyright (c) 2026 Kritva Robotics Private Limited.` with `SPDX-License-Identifier: Apache-2.0`. Upstream notices are never replaced.
9. **Commits.** Follow the Kritva commit format (`common/acceptance/ACCEPTANCE_STANDARD.md` section 4): `type(scope): summary` and one `Task:` footer from `planning/TASKS.md`. Do not add AI-session trailers or session links.
10. **Pull requests.** Work happens on a branch and lands through a pull request. No direct push to `main`, no force-push of shared branches, no history rewrite without the Owner's explicit approval.
