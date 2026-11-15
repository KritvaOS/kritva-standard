# KRITVA Engineering Standards Roadmap

Copyright (c) Kritva Robotics.

| Field | Value |
|---|---|
| Document ID | KSTD-GOV-000 (roadmap; not a standard) |
| Repository | `KritvaOS/kritva-standard` |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | PUBLIC |
| Owner / Approver | Dinesh Annayya (interim, not independent) |
| Last Updated | 2026-11-15 |
| Approval | PENDING |

> This roadmap proposes how the engineering standards are organised and in what order they are written. It approves no standard, tool, IP or design. Items marked PROPOSED need Owner approval.

## 1. Basis of this roadmap

Reviewed 2026-11-14: kritva-core, kritva-sense, kritva-mind, kritva-motion, kritva-skill, kritvaos-community, kritva-nexus, kritva-raas (local clones), kritva-mechanical (GitHub, default branch), and the VLSI content of kritva-standard. Not reviewed: kritva-program (not connected to this session), actuator repositories, source code, CI runs, branch protection.

## 2. Owner decisions recorded 2026-11-14

| # | Decision |
|---|---|
| D-1 | The copyright holder is `Kritva Robotics Private Limited`, for all KRITVA repositories. Public repositories use the header `Copyright (c) 2026 Kritva Robotics Private Limited.` plus `SPDX-License-Identifier: Apache-2.0`. Private repositories (kritva-raas, kritva-enterprise-program) use `Copyright (c) 2026 Kritva Robotics Private Limited.` plus `All rights reserved.` Upstream notices are never replaced. (Recorded 2026-11-14 and 2026-11-15; supersedes the shorter `Kritva Robotics` wording of 2026-11-12.) |
| D-2 | The README standard, commit format, acceptance format and status schema move from `kritva-program` to `kritva-standard`. |
| D-3 | Standard document IDs use `KSTD-<DOMAIN>-NNN`. |
| D-4 | Copies in `kritva-standard` are authoritative from 2026-11-15 onward. (2026-11-15) |
| D-5 | `kritva-program` keeps only planning, status monitoring and project management. All other specifications move to `kritva-standard` under `common`, `software`, `embedded`, `mechanical` and `vlsi`. (2026-11-15) |
| D-6 | The README migration plan stays in `kritva-standard`. (2026-11-15) |
| D-7 | Old copies are deleted only after setup is clean; pointers are updated where needed. (2026-11-15) |
| D-8 | `VLSI/` is renamed `vlsi/`. (2026-11-15; rename done by the Owner 2026-11-15, path references updated) |
| D-9 | Common scripts move to `common/tools/`. (2026-11-15; first set copied, see `common/tools/README.md`) |
| D-11 | All checkers stay in `kritva-program` so that one common entity controls commit approval; supersedes D-9 for checkers. `common/tools/` copies are reference only. (2026-11-15) |
| D-12 | Final script decision: scripts needed for a local commit live inside each repository's own folder; all program-level checks, including standard-conformance checks, live in `kritva-program`; `kritva-standard` holds no authoritative scripts. Supersedes D-9 and D-11. (2026-11-15) |
| D-13 | Refines D-12: where needed, both copies are kept: the program-level checker in `kritva-program` and a local checker in the repository that commits. Copies must not drift (see `common/tools/README.md` section 6). (2026-11-15) |
| D-10 | The kritva-program version of `check_commit_format.py` is the standard commit format checker. (2026-11-15) |

Earlier decisions (2026-11-12) remain in force: separate namespaced requirement ID schemes, no renumbering, MUST in common standards, A/T/R enforcement classes, KVRF/cocotb default flow.

Open follow-ups from these decisions are in section 9.

## 3. Principles

1. Separate domain standards under one governance framework; no single oversized document.
2. Existing approved standards are preserved. `KNX-RTL-STD-001` v1.0.1 is not rewritten or superseded by this work.
3. `kritva-program` keeps planning, baselines, approvals, gates and credit. `kritva-standard` defines reusable rules only.
4. Engineering acceptance (the artifact meets its specification and review criteria) is distinct from program acceptance (baseline, evidence and credit rules). A merge is neither.
5. Software checks, simulation and calculation are never presented as physical or silicon validation.
6. A standard is written when real work needs it. Directories are created with their first reviewed document.
7. Public and private boundaries are kept: Nexus rule text and per-rule mapping stay in the private `kritva-nexus` repository.

## 4. Existing standards inventory

| Standard or rule set | Location | State | Plan |
|---|---|---|---|
| VLSI IP standard, policies, KVRF, schemas, templates | `kritva-standard/vlsi/` | v0.1.0 DRAFT | Continue; fix index (section 7) |
| KNX-RTL-STD-001 (Nexus RTL) | `kritva-nexus/standards/` | v1.0.1 APPROVED (NX-DEC-023) | Keep; map to common rules (IPSTD-OI-010) |
| README standard, review checklist, migration plan, public and private templates | `kritva-program` v2/planning/standards/ | Exist; README_STANDARD.md not yet read in full | Migrate (D-2) |
| Document header standard (KOS-STD-DOCHDR) | `kritva-program` v2/planning/standards/ | PROPOSED (D-055, D-056) | Migrate with the README standard; align with D-1 |
| Acceptance standard and acceptance-criteria template | `kritva-program` v2/planning/ACCEPTANCE_STANDARD.md, templates/ | Exist; not yet read | Migrate (D-2) |
| Status schema 2.0 | `kritva-program` schema/status.schema.json, vendored in repos | Exists | Migrate (D-2); repos keep vendored snapshots |
| Commit format, test gates, tags, definition of done, required files | `kritva-program` v2/planning/ACCEPTANCE_STANDARD.md (sections 1 to 7, APPROVED via D-080, D-047, D-053); restated in the Engineering Contract | Exist; commit checker is `scripts/security/check_commit_format.py` | Migrate with the acceptance standard (D-2) |
| Engineering Contract (D-023) | `kritva-core` docs/development/ENGINEERING_CONTRACT.md, pinned by SHA-256 (D-113) | DRAFT for owner approval; controls over the acceptance standard where they differ | Decide its home before migration: moving it changes the pin that other repos check (GOV-OI-003) |
| Approval procedure, engineering contract compliance | `kritva-program` v2/planning/ | Exist | Stay in kritva-program (program governance); reference only |
| Core API-first, real-time documentation, compatibility policy | `kritva-core` AGENTS.md, docs/compatibility | In force | Reference for the software standard |
| Contract-first rules (versioning, conformance, errors) | sense, motion, mind, skill | Differ per repo | Unify (KSTD-CON-001) |
| Contribution, CLA, third-party code | `kritvaos-community` | In force | Reference; do not duplicate |
| Mechanical process rules (baselines, evidence, hold D-003) | `kritva-mechanical` | PLANNING | Reference for the mechanical standard |
| Toolchain definition | `kritvaos-community/toolchain/VERSIONS.yaml` | Pre-alpha | Input to the verified toolchain baseline |

## 5. Target architecture (PROPOSED)

Create each folder only when its first reviewed document exists.

~~~text
kritva-standard/
├── README.md
├── GOVERNANCE.md                 # KSTD-GOV-001
├── ENGINEERING_STANDARDS_ROADMAP.md
├── common/                       # exists: README, acceptance, commit, status schema, contract
├── software/                     # KSTD-SW-001 and KSTD-CON-001 (contract standard; folder split TBD)
├── embedded/                     # KSTD-EMB-001 (real-time and control)
├── mechanical/                   # KSTD-MECH-001
└── vlsi/                         # KSTD-VLSI-001 (renamed from VLSI/ 2026-11-15, CMN-OI-008 closed)
~~~

## 6. Document IDs (D-3)

Document IDs follow `KSTD-<DOMAIN>-NNN`. `KSTD-VLSI-001` already exists and is unchanged.

| Domain code | Meaning | First document |
|---|---|---|
| GOV | Governance and common formats | KSTD-GOV-001 |
| SW | Software engineering | KSTD-SW-001 |
| CON | Interface contracts | KSTD-CON-001 |
| EMB | Embedded and real-time control | KSTD-EMB-001 |
| MECH | Mechanical | KSTD-MECH-001 |
| VLSI | Semiconductor | KSTD-VLSI-001 |

Requirement IDs stay in their own namespaces (for example `KIP-STD-<AREA>-NNN`, `KNX-RTL-<CAT>-NNN`); each new domain proposes its namespace for Owner approval. IDs are never renumbered or reused. Statuses: PROPOSED, DRAFT, UNDER_REVIEW, APPROVED, DEPRECATED, SUPERSEDED. An approved standard is never silently replaced.

## 7. Phase plan

| Phase | Work | Depends on |
|---|---|---|
| 0 Foundation | DRAFTED 2026-11-15: `GOVERNANCE.md` (KSTD-GOV-001), top-level README, VLSI index corrections; apply D-1 to new files. Awaiting Owner review | None |
| 1 Common formats | DONE 2026-11-15 (copies, hash-verified): README standard set and document header standard in `common/readme/`; acceptance standard (with commit format, test gates, tags) and its templates in `common/acceptance/`; status schema in `common/schemas/`; Engineering Contract text in `common/contract/`. Index in `common/README.md`. Common scripts copied to `common/tools/` (checkers, PR gate, progress report, contract pin check). Remaining: pointers and cleanup in kritva-program and kritva-core, `check_source_headers.py` and copyright rollout (TLS-OI-001), Engineering Contract approval and pin (CMN-OI-007), the `vlsi` rename (CMN-OI-008) | Owner decisions D-4 to D-6 |
| 2 Governance | KSTD-GOV-001: ID scheme, statuses, engineering vs program acceptance, waivers, evidence model generalising the KVRF idea | Phase 0 |
| 3 Software and contracts | KSTD-SW-001 (Core as reference; Core's zero-dependency rule is a Core decision, not a general rule; C++20, lint and format gates, compatibility, real-time API documentation) and KSTD-CON-001 (versioning and 0.x rules, error codes, conformance IDs, deferred-item counting) | Phase 2 |
| 4 Embedded and mechanical | KSTD-EMB-001 (timing, WCET, jitter, fault and safe-state interfaces) and KSTD-MECH-001, written as planning text only; hold D-003 stays authoritative | Phase 3 |
| 5 VLSI continuation | APB revision and profile, RTL library manifest, Edge profile and mapping, KNX-to-KIP mapping (private), later design, physical-design, timing and DFT standards | Owner decisions (section 9) |

Perception, AI and Skill-specific rules start as profiles of KSTD-SW-001 and KSTD-CON-001 once Sense, Mind and Skill have implementation to standardise.

## 8. Repository applicability (PROPOSED)

| Repository | Standards that apply |
|---|---|
| kritva-core | GOV, SW, CON |
| kritvaos-community | GOV, SW, CON |
| kritva-sense, kritva-mind, kritva-motion | GOV, SW, CON; EMB for motion |
| kritva-skill | GOV, SW, CON |
| kritva-raas | GOV, SW (service profile later) |
| kritva-mechanical | GOV, MECH |
| kritva-nexus | GOV, VLSI, KNX-RTL-STD-001 |

Each repository declares its applicable standards in its existing README or AGENTS.md. A separate methodology file per repository is deferred until that proves insufficient.

## 9. Open items for the Owner

1. D-1 rollout: the core, sense, mind, motion, skill, community and raas READMEs currently show `Copyright (c) 2026 KritvaOS`. The core and community header lint (`scripts/lint/check_source_headers.py`, configuration under `config/`) probably enforces the old holder; confirm and update it together with the headers. KNX-RTL-DOC-002 and the VLSI documents say `Kritva Robotics`; they need the full legal name through a change request (the Nexus rule is SELECTED, so it also needs a new decision record).
2. Visibility of kritva-nexus is "not yet decided"; it needs a public or private header choice. kritva-enterprise-program is not connected, so its header is unchecked.
3. D-2 migration: confirm whether kritva-program keeps a pointer file, and how repos that cite `v2/planning/standards/README_STANDARD.md` are updated. The repo-level relationship between the copyright wording and the Apache-2.0 LICENSE is still to be documented.
4. Existing VLSI open items (APB profile, approval matrix, KVRF versioning and retention, verified toolchain baseline, record locations, RTL library manifest) remain open.
5. Whether KSTD-EMB-001 is one standard or separate firmware and control standards.

## 10. Approval record

| Field | Value |
|---|---|
| Document ID | KSTD-GOV-000 |
| Version | 0.1.0 |
| Status | DRAFT |
| Approver | Dinesh Annayya |
| Approval date | PENDING |
| Approval commit | PENDING |
