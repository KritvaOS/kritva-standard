# Common formats and specifications

Copyright (c) 2026 Kritva Robotics Private Limited.
SPDX-License-Identifier: Apache-2.0

| Field | Value |
|---|---|
| Document | Index and migration note for common formats and specifications |
| Repository | `KritvaOS/kritva-standard` |
| Version | 0.3.0 |
| Status | DRAFT |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Last Updated | 2026-11-15 |

This folder holds specifications and formats that apply to every KritvaOS repository. They move here from `kritva-program` and `kritva-core` under Owner decisions recorded in chat on 2026-11-14 and 2026-11-15. This note does not approve any document and does not change the approval status that each copied document declares for itself.

## 1. Owner decisions that govern this folder

| Date | Decision |
|---|---|
| 2026-11-14 | Common formats (README standard, commit format, acceptance format, status schema) move from `kritva-program` to `kritva-standard`. |
| 2026-11-15 | The copies in `kritva-standard` are authoritative from 2026-11-15 onward. |
| 2026-11-15 | `kritva-program` keeps only planning, status monitoring and project-management work. All other specifications move to `kritva-standard` under `common`, `software`, `embedded`, `mechanical` and `vlsi`. |
| 2026-11-15 | The README migration plan stays in `kritva-standard`. |
| 2026-11-15 | Old copies in `kritva-program` and `kritva-core` are deleted only after this setup is clean. Pointers are updated wherever needed. |
| 2026-11-15 | `VLSI/` renamed `vlsi/` by the Owner; path references updated. |
| 2026-11-15 | `check_readme.py`, `check_commit_format.py` and other common scripts go to `common/tools/` (see [tools/README.md](tools/README.md)). |
| 2026-11-15 (refinement) | Where needed, keep both copies: the program-level checker in `kritva-program` and the local checker in each repository. |
| 2026-11-15 (final) | Scripts needed for a local commit live inside each repository's own folder. All program-level checks, including standard-conformance checks, live in `kritva-program`. `kritva-standard` holds no authoritative scripts; `common/tools/` copies are reference only. (Supersedes the two earlier script decisions of the same day.) |

## 2. Migrated files (verbatim copies)

Each file is a byte-for-byte copy of its source. No text, link, ID or status was changed. Each still describes `kritva-program` or `kritva-core` in its own wording. SHA-256 values were taken from the sources before copying, and the copies were read back from this repository and compared (section 5).

| File here | Source | Original ID | Status declared in the file | SHA-256 |
|---|---|---|---|---|
| [readme/README_STANDARD.md](readme/README_STANDARD.md) | kritva-program v2/planning/standards/ | KOS-STD-README | APPROVED by the owner (D-066) | `2af0cec491565638851607cca30e88303ce48006cbb6facab568644675f1da1e` |
| [readme/README_REVIEW_CHECKLIST.md](readme/README_REVIEW_CHECKLIST.md) | same | none | per file | `56e57edfd416102423540bf73e6eef1601d3584890042da1d5c068fef842dacc` |
| [readme/README_TEMPLATE_PUBLIC.md](readme/README_TEMPLATE_PUBLIC.md) | same | none | per file | `24b8f693e4c7cf6b29bc0961d7d1f3494b398e401ce9d79ab6503a70aac98d3d` |
| [readme/README_TEMPLATE_PRIVATE.md](readme/README_TEMPLATE_PRIVATE.md) | same | none | per file | `f50c5afa1fdbb949b2c10837efccd0542ddc71c3250136260a24c67792c65fb5` |
| [readme/README_MIGRATION_PLAN.md](readme/README_MIGRATION_PLAN.md) | same | none | per file | `16b6d8f6e9862aeb128944346b982deaaa00590ae4a76a2b9a87a366e02d45ec` |
| [readme/DOCUMENT_HEADER_STANDARD.md](readme/DOCUMENT_HEADER_STANDARD.md) | same | KOS-STD-DOCHDR | PROPOSED (D-055, D-056) | `5e1238f753e4e8f0b68025d38bf130df5b66ede6587e2f3f61fb1f92a0e01e57` |
| [acceptance/ACCEPTANCE_STANDARD.md](acceptance/ACCEPTANCE_STANDARD.md) | kritva-program v2/planning/ | none | APPROVED (D-080, D-047, D-053) | `449912dcd10a49093ab0ea2db066b1c98449ad2db26c6478128c9836ff1d3094` |
| [acceptance/templates/ACCEPTANCE_CRITERIA.template.md](acceptance/templates/ACCEPTANCE_CRITERIA.template.md) | kritva-program v2/planning/templates/ | none | template | `da941da97b13ec4c7c35122cdd7390b09806b47fc1548e10f73aa97902d3aa7d` |
| [acceptance/templates/COMPLETION_RECORD.template.md](acceptance/templates/COMPLETION_RECORD.template.md) | same | none | template | `98c93f87534b6676c58bffd426aa0e4b5466c764ce2d332a6e490b2a17f73979` |
| [acceptance/templates/PULL_REQUEST_TEMPLATE.md](acceptance/templates/PULL_REQUEST_TEMPLATE.md) | same | none | template | `b541b558bfb8adee3470e6dddfdccbed1e865fa015746230bdb6f1ab9870f59f` |
| [schemas/status.schema.json](schemas/status.schema.json) | kritva-program schema/ | none | status schema 2.0 | `0c12f2a652936fd3c9db5a571e61491e1bacb8047087e5567c3c5e0fa1c1231d` |
| [contract/ENGINEERING_CONTRACT.md](contract/ENGINEERING_CONTRACT.md) | kritva-core docs/development/ | none | DRAFT for owner approval (D-023, PD-015) | `b57e24ba9771b0d156a352ed88aeb0462123af3bf14e0b23b9ecb18a07127021` (equals the SHA-256 in core's pin file) |

The acceptance standard carries the commit format (section 4), test gates, tags, definition of done and required files. The Engineering Contract states that it controls over the acceptance standard where they differ.

## 3. Not moved

| Item | Reason |
|---|---|
| Approval procedure, decisions log, baseline, approvals ledger, milestones, gate and risk registers, status views, the engineering compliance report | Planning, status and project management; stays in `kritva-program` |
| Program-specific scripts and tools (baseline, approvals, consolidation, dashboard, pipeline manifest and ship scripts) | Planning and status tooling; stays in `kritva-program`. Program-level checks stay in `kritva-program`; local-commit scripts live in each repository (reference copies in [tools/](tools/README.md)) |
| The pin file `ENGINEERING_CONTRACT.pin.json` | It records a hash and a commit in `kritva-core` and is checked there; a copy here would mean nothing |

## 4. Consequences and cautions

1. **Authority now sits here; the old copies are not yet changed.** Until `kritva-program` and `kritva-core` are updated, their copies look authoritative to anyone who reads them. They should carry a pointer to this folder and must not be edited independently.
2. **Broken relative links in the copies.** The acceptance standard links to `repo-pipeline.json`, `V2_REPO_PLAN.md` and `APPROVAL_PROCEDURE.md`, which stay in `kritva-program`. Within this repository those links do not resolve.
3. **Engineering Contract.** Its text is still DRAFT. `kritva-core` runs a pin check (`check_contract_pin.py`) against its own copy, so that copy cannot be changed or removed without updating the pin and the check. The contract says changes need a new owner approval, a new pin and a program decision.
4. **Citations.** The READMEs of core, community, sense, mind, motion, skill and raas cite `v2/planning/standards/README_STANDARD.md`; the checkers and gates reference the old paths.
5. **No `KSTD-` IDs yet.** Original IDs are kept. Proposed aliases below are not approved.

## 5. Verification

All twelve copies were read back from this repository after writing and compared with the SHA-256 of their sources (result recorded in the session that made this change). A reviewer can repeat this with `sha256sum` against section 2.

## 6. Proposed IDs (PROPOSED, not approved)

| Original | Proposed |
|---|---|
| KOS-STD-README | KSTD-GOV-002 |
| KOS-STD-DOCHDR | KSTD-GOV-003 |
| Acceptance standard | KSTD-GOV-004 |
| Engineering Contract | KSTD-GOV-005 |

Original IDs stay valid as aliases.

## 7. Open items

| ID | Item |
|---|---|
| CMN-OI-002 | Old copies stay until the setup is clean, then are deleted (deletion needs delete permission on the device). Pointer updates in `kritva-program`, `kritva-core` and the citing repositories are to be made when needed; not done yet |
| CMN-OI-004 | Whether the README templates need a copyright-header section |
| CMN-OI-005 | Program-level checks stay authoritative in `kritva-program`; each repository keeps the scripts its local commit needs; the reference copies in [tools/](tools/README.md) are to be removed when setup is clean. Which scripts count as local-commit and which as program-level is to be listed (TLS-OI-004) |
| CMN-OI-006 | Document header standard is PROPOSED, not approved. D-15 approves it as KSTD-GOV-003 with changes (KSTD document ID field, new copyright header); the revised text is not written |
| CMN-OI-007 | Engineering Contract approval, new pin location and the pin check after the move (GOV-OI-003) |
| CMN-OI-008 | CLOSED 2026-11-15: `VLSI/` renamed `vlsi/` by the Owner; path references in the VLSI documents and the repository docs updated |
