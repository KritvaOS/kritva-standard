# kritva-standard

> Common engineering standards, schemas, templates and specifications for KritvaOS, organised by domain. Every document is a draft or carries the status it declares for itself; nothing here approves any IP, tool, design or release.

Copyright (c) 2026 Kritva Robotics Private Limited.
SPDX-License-Identifier: Apache-2.0

| Property | Value |
|---|---|
| Project | KritvaOS |
| Repository | `KritvaOS/kritva-standard` |
| Repository Type | Documentation |
| Visibility Class | Not yet decided (no visibility decision is recorded for this repository) |
| GitHub Setting | PUBLIC (seen on the repository page on 2026-11-14; not owner-attested) |
| Lifecycle Status | ACTIVE (VLSI drafts and migrated common specifications exist; software, embedded and mechanical not started) |
| Repository Owner | Dinesh Annayya (`dineshannayya`) |
| Architecture | Not applicable (a standards repository); the domain layout is in [ENGINEERING_STANDARDS_ROADMAP.md](ENGINEERING_STANDARDS_ROADMAP.md) |
| Milestones | Not yet defined (phases are in [ENGINEERING_STANDARDS_ROADMAP.md](ENGINEERING_STANDARDS_ROADMAP.md); program milestones live in kritva-program) |
| Tasks | Proposed task IDs in [planning/TASKS.md](planning/TASKS.md) (repository-local, not registered in kritva-program) |
| Acceptance Criteria | Not yet defined; acceptance rules are in [common/acceptance/ACCEPTANCE_STANDARD.md](common/acceptance/ACCEPTANCE_STANDARD.md) |
| Status Reporting | Not yet defined (no status file exists in this repository) |
| License | [LICENSE](LICENSE) (Apache License 2.0) |

## 1. Purpose and Scope

This repository holds the specifications other KritvaOS repositories follow: engineering standards by domain, common formats, schemas, templates and the engineering contract. Domains are `common`, `software`, `embedded`, `mechanical` and `vlsi`.

It owns all specifications (authoritative here from 2026-11-15). It does not own program planning, decisions, baselines, approvals, credit, status monitoring or project management, which belong to kritva-program. It does not hold implementations, and it does not hold the commit-approval checkers, which stay in kritva-program.

## 2. Position in the KritvaOS Ecosystem

Engineering repositories (core, sense, mind, motion, skill, community, nexus, raas and the mechanical repository) follow the standards here. kritva-program plans and monitors the work and decides approvals; see [kritva-program](https://github.com/KritvaOS/kritva-program). Private profile rules, such as the Nexus RTL standard, stay in their private repositories.

## 3. Architecture

Not applicable as a software architecture. The intended domain layout, document ID scheme (`KSTD-<DOMAIN>-NNN`) and phase plan are in [ENGINEERING_STANDARDS_ROADMAP.md](ENGINEERING_STANDARDS_ROADMAP.md) (DRAFT). A listed folder does not exist until it has a reviewed document.

## 4. Documents to Read First

| Document | Label, status | What it answers |
|---|---|---|
| [GOVERNANCE.md](GOVERNANCE.md) | AUTHORITATIVE for standards governance, DRAFT | Ownership, approval, IDs, statuses, public and private content |
| [ENGINEERING_STANDARDS_ROADMAP.md](ENGINEERING_STANDARDS_ROADMAP.md) | REFERENCE (plan), DRAFT | What is planned, in what order, and which decisions are open |
| [common/README.md](common/README.md) | REFERENCE (index), DRAFT | Which common specifications were migrated and from where |
| [common/readme/README_STANDARD.md](common/readme/README_STANDARD.md) | AUTHORITATIVE for README layout, APPROVED per its own status line | How every repository README is structured |
| [common/acceptance/ACCEPTANCE_STANDARD.md](common/acceptance/ACCEPTANCE_STANDARD.md) | AUTHORITATIVE for acceptance, commit format, test gates and tags, APPROVED per its own status line | What makes work accepted and how commits are written |
| [common/contract/ENGINEERING_CONTRACT.md](common/contract/ENGINEERING_CONTRACT.md) | AUTHORITATIVE role for lifecycle, branch, commit and tag rules, DRAFT for owner approval | The controlling engineering convention |
| [vlsi/README.md](vlsi/README.md) | AUTHORITATIVE for the VLSI domain index, DRAFT | VLSI standards, IP source categories and boundaries |

A label names a role, not an approval. Each migrated document keeps the status it declares for itself.

## 5. Repository Structure and File Responsibilities

| Path | Responsibility | Label, status | Edit by hand? |
|---|---|---|---|
| [GOVERNANCE.md](GOVERNANCE.md) | Standards governance (KSTD-GOV-001) | AUTHORITATIVE, DRAFT | Yes, by Owner-reviewed change |
| [ENGINEERING_STANDARDS_ROADMAP.md](ENGINEERING_STANDARDS_ROADMAP.md) | Roadmap and open decisions | REFERENCE, DRAFT | Yes |
| [common/](common/README.md) | Migrated common specifications, templates, schemas, contract, tools | MIXED | Per file; migrated copies are edited only through a recorded change |
| [common/readme/](common/readme/README_STANDARD.md) | README standard set and document header standard | AUTHORITATIVE, per file | Per file |
| [common/acceptance/](common/acceptance/ACCEPTANCE_STANDARD.md) | Acceptance standard and templates | AUTHORITATIVE, per file | Per file |
| [common/schemas/](common/schemas/status.schema.json) | Status schema 2.0 | AUTHORITATIVE, per file | Per file |
| [common/contract/](common/contract/ENGINEERING_CONTRACT.md) | Engineering contract text | AUTHORITATIVE role, DRAFT | By Owner approval only |
| [common/tools/](common/tools/README.md) | Reference copies of checker scripts; see section 6 | REFERENCE | No |
| [vlsi/](vlsi/README.md) | VLSI domain: IP standard, KVRF, schemas and templates | MIXED, DRAFT | Per file |

Domain folders for software, embedded and mechanical do not exist yet.

## 6. Toolchain, Getting Started and Development Workflow

The standards are Markdown, YAML and JSON. No build is needed. The README checker is stdlib Python and lives in kritva-program, which controls commit and README checks.

| Tool | Purpose | Version | Check |
|---|---|---|---|
| Python 3 | Run the README checker | Not pinned (3.12 was used for the last run) | `python3 --version` |

| Command | Effect | Needs | Preview |
|---|---|---|---|
| `python3 ../kritva-program/scripts/docs/check_readme.py README.md` | check | A sibling clone of kritva-program | Read-only |

The copies in [common/tools/](common/tools/README.md) are reference copies of the checkers. The Owner decided on 2026-11-15 that the checkers stay in kritva-program; the copies here are not authoritative and are due for removal once the setup is clean.

## 7. Dependencies and Interfaces

| Dependency | Direction | Kind | Contract | State |
|---|---|---|---|---|
| kritva-program | upstream and downstream | governance; planning, status, approvals and checkers live there | Approved decisions and approvals ledger | ESTABLISHED |
| Engineering repositories | downstream | each follows the applicable standards | Per-repository declaration of applicable standards | PROPOSED |
| kritva-nexus (private) | peer | holds the Nexus RTL standard and the populated rule mapping | Public mapping methodology in the VLSI index | ESTABLISHED |

## 8. Roadmap

| Item | Document | Status and meaning of dates |
|---|---|---|
| Roadmap | [ENGINEERING_STANDARDS_ROADMAP.md](ENGINEERING_STANDARDS_ROADMAP.md) | DRAFT; phases carry no dates and are not delivery commitments |
| Milestones | Not yet defined | Program milestones live in kritva-program |

## 9. Tasks and Acceptance Criteria

Proposed repository-local task IDs (KOS-STD-001 to 013) are in [planning/TASKS.md](planning/TASKS.md); they are not registered in kritva-program. Work is also tracked through the roadmap's phases and the Owner's decisions. Acceptance follows [common/acceptance/ACCEPTANCE_STANDARD.md](common/acceptance/ACCEPTANCE_STANDARD.md). A merge, a commit or a passing check is not acceptance.

## 10. Status Reporting and Program Integration

No status file or generator exists here. Execution is described in the roadmap. Evidence for migrated files is the SHA-256 table in [common/README.md](common/README.md). Acceptance and approval are decided by the Owner and recorded as described in [GOVERNANCE.md](GOVERNANCE.md). Release readiness is not applicable. This repository does not claim program credit.

## 11. Build, Test, Regression and Validation

| Check | Command | Effect | Runs in CI? | Expected |
|---|---|---|---|---|
| README structure | `python3 ../kritva-program/scripts/docs/check_readme.py README.md` | check | No | PASS means the implemented structural checks passed; it does not show the content is accurate |
| Copy integrity | `sha256sum` on a migrated file against the table in `common/README.md` | check | No | Hash equals the recorded value |

No CI workflow exists in this repository. Schema validation of the VLSI records is described in the VLSI index.

## 12. Git Workflow and Review

Changes go through Owner review. The Kritva commit standard (see [common/acceptance/ACCEPTANCE_STANDARD.md](common/acceptance/ACCEPTANCE_STANDARD.md) section 4) has not been recorded as formally adopted for this repository, and no checker is enforced here. Changes to normative text, identifiers, schemas or approval policy require explicit Owner review ([GOVERNANCE.md](GOVERNANCE.md) section 9).

## 13. Safety and Security

This repository contains documents only; it does not move hardware. Software checks, calculations and simulation described in these standards do not prove physical safety. The reporting route is a DRAFT in [SECURITY.md](SECURITY.md) and has not been tested; the Owner will confirm it. Do not post details of an unfixed vulnerability in a public issue or pull request. Do not commit credentials or private engineering records; see [GOVERNANCE.md](GOVERNANCE.md) section 7.

## 14. Release and Versioning

Each document carries its own version and status (DRAFT, UNDER_REVIEW, APPROVED, DEPRECATED, SUPERSEDED). The repository has no release scheme, tags or changelog yet. Document versions are separate from any repository release.

## 15. Ownership and Escalation

Owner and sole approver (interim): Dinesh Annayya (`dineshannayya`). The interim arrangement is not independent review. Blockers are raised to the Owner. A draft [.github/CODEOWNERS](.github/CODEOWNERS) names the Owner; contributor and agent rules are in [CONTRIBUTING.md](CONTRIBUTING.md) and [AGENTS.md](AGENTS.md).

## 16. Related Repositories and References

[kritva-program](https://github.com/KritvaOS/kritva-program) (planning, status, approvals, checkers), and the engineering repositories that follow these standards: kritva-core, kritva-sense, kritva-mind, kritva-motion, kritva-skill, kritvaos-community, kritva-nexus, kritva-raas and the mechanical repository.

## 17. License

Apache License 2.0. See [LICENSE](LICENSE).
