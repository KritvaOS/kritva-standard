# KRITVA Standards Governance

Copyright (c) Kritva Robotics Private Limited.

| Field | Value |
|---|---|
| Document ID | KSTD-GOV-001 |
| Document | Standards Governance |
| Repository | `KritvaOS/kritva-standard` |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | PUBLIC |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Last Updated | 2026-11-15 |

> **Status notice:** This document is DRAFT. It becomes normative only after explicit approval by the authorized KRITVA owner. It records existing owner decisions and proposes governance for the standards in this repository. Items marked PROPOSED are not decisions.

---

## 1. Purpose and scope

This document defines ownership, approval, document identity, status, public-content control and change control for the standards in `KritvaOS/kritva-standard`.

It does not define technical rules for any engineering domain, and it does not replace program governance in `kritva-program` (decisions, baseline, approvals, gates, credit and consolidated status).

## 2. Ownership and approval

1. The Owner and sole approver (interim) is Dinesh Annayya. The interim arrangement is not independent review and is never described as such.
2. A standard becomes APPROVED only through explicit Owner approval, recorded against a repository commit in the document's approval record.
3. A DRAFT or PROPOSED document, schema, template or example approves nothing by itself: no IP, tool, tool version, design, lifecycle transition or product integration.
4. AI output (including from Claude or ChatGPT) is advisory. Only the Owner approves.
5. Delegation to other approvers requires an Owner decision. No delegation matrix is approved yet (open item GOV-OI-001).

## 3. Relationship to kritva-program

| Concern | Owner of the record |
|---|---|
| Planning, decisions, baseline, approvals ledger, gates, credit, status monitoring, project management, and program-level checks including standard-conformance checks | `kritva-program` |
| All specifications: engineering rules, formats, schemas, templates and contracts (authoritative here from 2026-11-15) | `kritva-standard` |
| Repository-specific implementation, and the scripts its local commit needs | The engineering repository |

Two kinds of acceptance are kept apart:

- **Engineering acceptance:** an artifact meets its specification and review criteria.
- **Program acceptance:** a task meets the approved program baseline, evidence and credit rules.

A merge, a passing check or a standard's APPROVED status is neither of these by itself, and creates no program credit.

## 4. Document identity

Standard documents use `KSTD-<DOMAIN>-NNN` (Owner decision, 2026-11-14).

| Domain code | Meaning |
|---|---|
| GOV | Governance and common formats |
| SW | Software engineering |
| CON | Interface contracts |
| EMB | Embedded and real-time control |
| MECH | Mechanical |
| VLSI | Semiconductor |

Rules:

- Document IDs and requirement IDs are never renumbered or reused.
- Requirement IDs use a namespace per domain or profile (for example `KIP-STD-<AREA>-NNN`, `KNX-RTL-<CAT>-NNN`). A new namespace needs Owner approval before publication.
- A requirement promoted from a profile receives a new common ID and records what it was derived from.
- Existing identifiers in approved documents, including `KNX-RTL-STD-001`, are preserved.

## 5. Status

| Status | Meaning |
|---|---|
| PROPOSED | Idea or outline; not a draft of normative text |
| DRAFT | Written text under author control; not normative |
| UNDER_REVIEW | Submitted for Owner review |
| APPROVED | Approved by the Owner and recorded in the approval record |
| DEPRECATED | Still valid for existing users; not for new use |
| SUPERSEDED | Replaced by a named later document |

Status is earned: a document is not APPROVED without a recorded approval. An approved standard is never silently replaced; a replacement names what it supersedes. A document version is separate from any repository release version.

## 6. Normative language

Common standards use RFC 2119 MUST, MUST NOT, SHOULD and MAY. In an approved profile, SHALL has equivalent force to MUST. Enforcement classes A (automated), T (tool-assisted) and R (review only) describe how a rule is checked and never change its normative force.

## 7. Public and private content

1. This repository is PUBLIC.
2. Rule text, mappings and details owned by a private repository stay there. For Nexus, the profile `KNX-RTL-STD-001` and its per-rule mapping to common requirements stay in the private `kritva-nexus` repository; only common requirements, public mapping methodology and area-level guidance are published here.
3. Do not publish speculative profile requirements as approved rules (the Edge profile has not started).
4. Preserve upstream copyright and licence notices when including third-party material.
5. Do not include credentials, tokens or private infrastructure detail.

## 8. Copyright and licence headers

KRITVA-authored files use `Copyright (c) 2026 Kritva Robotics Private Limited.` (the year is the year of creation). Public repositories add `SPDX-License-Identifier: Apache-2.0`. Private repositories add `All rights reserved.` Upstream notices are never replaced. The licence line is the repository's real licence and is not copied from another repository.

Where a repository's header lint enforces a different holder wording, the lint configuration and the headers change together under that repository's change process (open item GOV-OI-002).

## 9. Change control

1. Changes to normative requirements, identifier schemes, schema contracts, profile scope or approval policy require explicit Owner review.
2. A normative change states rationale, scope, impact and verification evidence, and updates affected schemas and templates.
3. A standards update does not automatically modify an existing release; its impact is evaluated against affected packages and their qualification records.
4. Inconsistencies between documents are recorded for Owner review, not resolved by silently changing a requirement or record.
5. Existing documents are not rewritten in one sweep; a document gains the current header when next edited for another reason.

## 10. Waivers and exceptions

A waiver is a structured record with approver, scope, rationale and an expiry or review condition. It is effective only after approval. It does not change the underlying requirement and never turns failed or missing evidence into a pass. A waiver cannot replace an Owner decision record.

## 11. Evidence

Evidence claims name the exact commit and result, and their scope. Software checks, calculations and simulation are never presented as physical, silicon or safety validation. Evidence references immutable identifiers (commit SHAs, run IDs), not branch names.

## 12. Open items

| ID | Item |
|---|---|
| GOV-OI-001 | Approval authority and delegation matrix. Decided 2026-11-15 (D-15): the Owner stays sole approver (interim, not independent); roles are defined on paper and nothing is delegated. Open until roles are written |
| GOV-OI-002 | Rollout of the `Kritva Robotics Private Limited` wording, including header-lint configuration in other repositories. Plan in `planning/COPYRIGHT_ROLLOUT_PLAN.md` (approved under D-15, not executed) |
| GOV-OI-003 | Approval and pin of the Engineering Contract (D-023), now copied to `common/contract/`; it controls over the acceptance standard where they differ. Proposal P-1 in `planning/PROPOSALS_FOR_KRITVA_PROGRAM.md`; not approved |
| GOV-OI-004 | Pointer notices and cleanup of old copies in `kritva-program` and `kritva-core` (copies here are authoritative from 2026-11-15). Sequence approved under D-15: pointer banners, README link updates, then removal after one green check cycle; not executed |
| GOV-OI-005 | Controlled list of decision-type names used across policies and templates |

## 13. Approval record

| Field | Value |
|---|---|
| Document ID | KSTD-GOV-001 |
| Version | 0.1.0 |
| Status | DRAFT |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Approver | Dinesh Annayya (`dineshannayya`) |
| Approval date | PENDING |
| Approval commit | PENDING |

**Approval statement:** This document is not an approved KRITVA governance baseline until Dinesh Annayya explicitly approves version 0.1.0 and the approval is recorded against the applicable repository commit.

---

**End of document**
