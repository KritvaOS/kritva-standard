# KRITVA Open-Source IP Policy

| Field | Value |
|---|---|
| Document ID | KSTD-OSIP-001 |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | Public |
| Owner | Dinesh Annayya |
| Applies to | KRITVA IP repositories and approved IP intake activities |
| Related standard | `KRITVA_IP_STANDARD.md` |
| Related SoC profile | `KNX-RTL-STD-001` |
| Last updated | 2026-11-13 |

---

## 1. Purpose

This policy defines how open-source and other third-party intellectual property (IP) is identified, evaluated, recorded, approved, incorporated, maintained, and distributed within the KRITVA ecosystem.

It establishes a controlled process for using external source code, RTL, verification components, software, documentation, generated artifacts, and supporting tools.

The policy is intended to:

- Establish consistent source and license classification.
- Prevent unreviewed or incompatible third-party material from entering KRITVA repositories.
- Preserve traceable provenance to immutable upstream revisions.
- Separate upstream material from KRITVA-owned modifications and integration records.
- Ensure third-party license and notice obligations are satisfied.
- Protect private implementation information and unreleased SoC details.
- Make adoption decisions explicit, reviewable, and auditable.

This document is a public policy baseline. It does not disclose private repository structures, unreleased SoC implementation details, or confidential supplier information.

## 2. Scope

This policy applies to third-party material considered for use in:

- RTL and synthesizable hardware IP.
- RTL verification components, testbenches, and reference models.
- Simulation and development infrastructure.
- Hardware description and interface packages.
- Firmware and software components associated with IP.
- Build, lint, synthesis, formal, simulation, and implementation flows.
- Documentation, specifications, schemas, and reference collateral.
- Generated source code and generated design artifacts.
- Scripts, utilities, and supporting development tools.

It applies whether the material is copied, imported, vendored, submoduled, generated, adapted, or referenced as an external dependency.

This policy does not replace:

- The KRITVA IP design and integration requirements in `KRITVA_IP_STANDARD.md`.
- SoC-specific design profiles and decisions.
- Repository-specific contribution and release procedures.
- Legal review where required.
- The terms of the applicable third-party license.

## 3. Normative Language

The terms below define the interpretation of requirements in this document.

| Term | Meaning |
|---|---|
| MUST | Mandatory requirement. Non-compliance prevents approval or adoption unless an explicitly approved exception permits it. |
| MUST NOT | Prohibited action. |
| SHOULD | Recommended requirement. A deviation requires a documented rationale and review. |
| SHOULD NOT | An action that should be avoided unless a documented rationale supports it. |
| MAY | Permitted action. |

Where another applicable KRITVA standard imposes a stricter requirement, the stricter requirement applies within its scope.

Owner decision (2026-11-12): common KRITVA standards use RFC 2119 `MUST`. Where an approved SoC-specific profile such as `KNX-RTL-STD-001` uses `SHALL`, `SHALL` has the same normative force as `MUST`.

## 4. Policy Principles

The following principles govern all third-party IP intake and use.

| ID | Principle | Policy |
|---|---|---|
| OSIP-PR-001 | Traceability | Every adopted third-party component MUST have traceable source provenance. |
| OSIP-PR-002 | License clarity | Every adopted component MUST have a classified license and documented usage basis. |
| OSIP-PR-003 | Immutable reference | An adopted upstream dependency MUST be associated with an immutable revision or equivalent verifiable source reference. |
| OSIP-PR-004 | Explicit adoption | Downloading, reviewing, or evaluating a component MUST NOT automatically authorize its adoption. |
| OSIP-PR-005 | Separation | Upstream material and KRITVA-owned changes MUST be distinguishable. |
| OSIP-PR-006 | Notice preservation | Applicable copyright, license, attribution, and third-party notice obligations MUST be preserved. |
| OSIP-PR-007 | Controlled distribution | Redistribution MUST comply with the applicable license and KRITVA release controls. |
| OSIP-PR-008 | Public/private separation | Public records MUST NOT disclose private implementation details or confidential information. |
| OSIP-PR-009 | Technology boundary | RTL technology dependencies MUST be governed by the approved RTL library manifest defined by the applicable KRITVA IP standard and SoC profile. |
| OSIP-PR-010 | Reviewability | Adoption decisions and exceptions MUST be recorded with sufficient evidence for independent review. |

## 5. Source Categories

Every candidate third-party component MUST be assigned a source category.

### 5.1 Source classification

| Category ID | Source category | Description | Typical examples |
|---|---|---|---|
| SRC-001 | Upstream open-source project | Public project distributed under an identifiable open-source license. | RTL cores, verification libraries, software libraries. |
| SRC-002 | Standards reference implementation | Public implementation associated with a technical standard or specification. | Protocol reference models, bus functional models. |
| SRC-003 | Vendor-provided collateral | Material supplied by a commercial vendor under public or restricted terms. | Evaluation models, interface collateral, scripts. |
| SRC-004 | Public-domain material | Material explicitly dedicated to the public domain or otherwise established as having no applicable copyright restrictions. | Public-domain reference code. |
| SRC-005 | Permissively licensed generated material | Generated source or collateral whose licensing and provenance can be established. | Generated register packages, generated interface code. |
| SRC-006 | Restricted or proprietary material | Material subject to commercial, confidential, evaluation-only, or other restrictive terms. | Proprietary IP, licensed models, confidential SDKs. |
| SRC-007 | Unknown or incomplete provenance | Material for which origin, authorship, license, or revision cannot be established. | Unattributed code snippets, copied source without history. |
| SRC-008 | KRITVA-owned material | Original material developed within KRITVA repositories and governed by KRITVA repository licensing and contribution rules. | KRITVA-authored RTL and verification code. |

A component MAY contain multiple source categories at the file or subdirectory level. In such cases, classification MUST be sufficiently granular to identify the different origins and obligations.

### 5.2 Source classification requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-SRC-001 | Every candidate component MUST be assigned a source category before adoption. | R |
| OSIP-SRC-002 | The source project, original author or organization, and authoritative source location MUST be recorded where available. | R |
| OSIP-SRC-003 | Material with unknown or incomplete provenance MUST NOT be adopted until its origin and usage rights are resolved. | R |
| OSIP-SRC-004 | Generated material MUST identify the generator and, where available, the generator version and input source revision. | R |
| OSIP-SRC-005 | Vendor-provided and restricted material MUST be handled according to its contractual restrictions and MUST NOT be assumed to be open source. | R |
| OSIP-SRC-006 | KRITVA-owned modifications MUST be distinguishable from unmodified upstream content. | R |

## 6. License Classification

### 6.1 License identification

Every candidate component MUST have an identifiable license or documented legal basis for use.

The license assessment MUST consider:

- The license applying to the component as a whole.
- File-level license differences.
- License exceptions and additional terms.
- Copyright and attribution requirements.
- Source-disclosure and redistribution obligations.
- Patent grants, patent conditions, and termination clauses.
- Notice and attribution obligations.
- Restrictions on use, modification, or distribution.
- Compatibility with the intended KRITVA distribution model.
- Obligations introduced by combining the component with other material.

A repository-level license MUST NOT be assumed to cover every file in that repository.

### 6.2 License classes

The following classification is used for intake assessment.

| License class | Description | Initial disposition |
|---|---|---|
| LIC-001: Permissive | Licenses generally permitting use, modification, and redistribution subject to conditions such as notices and disclaimers. | Eligible for approval review. |
| LIC-002: Weak copyleft | Licenses imposing obligations on covered files or components while potentially allowing combination with separately licensed material. | Mandatory review. |
| LIC-003: Strong copyleft | Licenses imposing broader source and redistribution obligations on covered derivative or combined works. | Mandatory legal and owner review. |
| LIC-004: Network copyleft | Licenses with obligations triggered by network interaction or service provision. | Mandatory legal and owner review. |
| LIC-005: Public domain or equivalent dedication | Material with a verifiable public-domain dedication or equivalent rights basis. | Eligible for approval review. |
| LIC-006: Proprietary or commercial | Material distributed under commercial, evaluation, or vendor-specific terms. | Not eligible for open-source adoption without explicit rights approval. |
| LIC-007: Custom or non-standard | Individually drafted, unusual, or non-standard license terms. | Mandatory legal review. |
| LIC-008: Unknown or conflicting | Missing, ambiguous, inconsistent, or conflicting license information. | Deny adoption until resolved. |

The classification is an intake and review mechanism. It is not a legal determination that a particular license is compatible with every KRITVA use case.

### 6.3 License examples

The examples below are illustrative and do not constitute blanket approval.

| License | Typical classification | Initial disposition |
|---|---|---|
| MIT | Permissive | Review for approval. |
| BSD-2-Clause | Permissive | Review for approval. |
| BSD-3-Clause | Permissive | Review for approval. |
| Apache-2.0 | Permissive | Review for approval, including notice and patent terms. |
| ISC | Permissive | Review for approval. |
| MPL-2.0 | Weak copyleft | Mandatory review. |
| LGPL family | Weak copyleft | Mandatory review. |
| GPL family | Strong copyleft | Mandatory legal and owner review. |
| AGPL family | Network copyleft | Mandatory legal and owner review. |
| CC0 | Public-domain dedication | Review of dedication and applicability. |
| Unlicense | Public-domain-style dedication | Review of applicability and jurisdictional considerations. |
| Proprietary EULA | Proprietary or commercial | Restricted; explicit rights approval required. |
| No license identified | Unknown | Deny adoption until resolved. |

The presence of a license name in this table does not authorize automatic adoption.

## 7. Allow, Deny, and Review Rules

### 7.1 Disposition classes

Every candidate component MUST receive one of the following dispositions.

| Disposition | Meaning | Permitted activity |
|---|---|---|
| ALLOW | Reviewed and approved for a defined scope of use. | Adoption within the approved scope and conditions. |
| REVIEW | Potentially usable, but additional technical, license, security, or owner review is required. | Evaluation in an isolated or otherwise controlled context; no production adoption. |
| DENY | Prohibited from adoption under the current policy or unresolved rights conditions. | No incorporation into KRITVA deliverables. |

An ALLOW decision MUST state the approved scope. It MUST NOT be interpreted as universal approval for all KRITVA repositories, products, or distribution models.

### 7.2 Allow rules

A candidate MAY be classified ALLOW only when:

1. Its source origin is identifiable.
2. Its license or legal basis is established.
3. Its intended use is compatible with the applicable license terms.
4. Its immutable upstream revision is recorded.
5. Required notices and attribution obligations are understood.
6. Technical suitability has been reviewed.
7. Security and maintenance risks have been considered.
8. Any required legal or owner approval has been obtained.
9. Its intended repository and distribution scope are documented.
10. The adoption decision is recorded.

### 7.3 Review rules

A candidate MUST be classified REVIEW when one or more of the following applies:

- The license is weak copyleft, strong copyleft, network copyleft, custom, or otherwise requires interpretation.
- File-level license information is incomplete.
- The component contains mixed licensing.
- The source contains generated or copied material with uncertain provenance.
- The intended use or redistribution model is not established.
- The component has unresolved security or maintenance concerns.
- The component introduces a new technology dependency.
- The component has an unclear relationship to the approved RTL library manifest.
- Its modification or integration model could introduce additional obligations.
- Its source contains material that may be subject to commercial or confidentiality restrictions.

REVIEW is not an approval to merge the candidate into a production IP baseline.

### 7.4 Deny rules

A candidate MUST be classified DENY when:

- Its origin cannot be established and cannot be resolved.
- No valid license or other usage right can be established.
- Its terms prohibit the intended use or distribution.
- Its use would violate a contractual or legal restriction.
- It contains knowingly misappropriated or unauthorized material.
- Required rights or permissions have been refused.
- It contains undisclosed proprietary material that cannot be lawfully incorporated.
- A required legal or owner review rejects the proposed use.

A DENY decision MUST include a reason and MUST be retained in the relevant intake record.

### 7.5 Disposition requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-LIC-001 | Every candidate MUST receive an ALLOW, REVIEW, or DENY disposition. | R |
| OSIP-LIC-002 | A candidate MUST NOT be adopted while its disposition is REVIEW or DENY. | R |
| OSIP-LIC-003 | An ALLOW decision MUST define the approved scope of use. | R |
| OSIP-LIC-004 | License compatibility MUST be assessed against the intended modification, integration, and distribution model. | R |
| OSIP-LIC-005 | License exceptions and additional terms MUST be recorded. | R |
| OSIP-LIC-006 | Missing or conflicting license information MUST prevent adoption until resolved. | R |
| OSIP-LIC-007 | A change in license, source content, or intended use MUST trigger reassessment. | R |
| OSIP-LIC-008 | License classification MUST NOT be treated as a substitute for legal review where legal review is required. | R |

## 8. Provenance and Immutable Upstream Tracking

### 8.1 Provenance record

Every adopted third-party component MUST have a provenance record.

The record MUST contain, where applicable:

| Field | Description |
|---|---|
| Component ID | Stable KRITVA identifier for the adopted component. |
| Component name | Upstream project or component name. |
| Source category | Category defined in Section 5. |
| Upstream organization | Original author, maintainer, or organization. |
| Upstream repository | Authoritative repository location. |
| Upstream revision | Immutable commit hash or equivalent immutable revision identifier. |
| Release identifier | Upstream release or tag, if applicable. |
| Source snapshot | Identifier or checksum of the imported source snapshot. |
| License | Identified license and any applicable exceptions. |
| Copyright | Original copyright and attribution information. |
| Intake date | Date the candidate was evaluated. |
| Adoption date | Date adoption was approved. |
| Disposition | ALLOW, REVIEW, or DENY. |
| Approved scope | Repositories, components, or use cases covered by the decision. |
| Modifications | Summary or reference to KRITVA modifications. |
| Review record | Technical, license, security, and owner review references. |
| Notices | Location or reference for required third-party notices. |

A provenance record MAY include additional fields required by the component, license, or repository.

### 8.2 Immutable revision requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-PROV-001 | Every adopted upstream dependency MUST identify an immutable upstream revision. | R |
| OSIP-PROV-002 | A mutable branch name such as `main`, `master`, or `develop` MUST NOT be the sole revision reference for an adopted dependency. | R |
| OSIP-PROV-003 | A release tag MUST be accompanied by an immutable commit or equivalent verifiable source reference where the upstream system supports it. | R |
| OSIP-PROV-004 | The imported source snapshot SHOULD have a checksum or equivalent integrity reference. | R |
| OSIP-PROV-005 | The upstream source location and original revision MUST remain traceable after local modifications. | R |
| OSIP-PROV-006 | An upstream update MUST be recorded as a new intake or update event, with its own immutable revision. | R |
| OSIP-PROV-007 | The provenance record MUST NOT be rewritten to make a modified KRITVA copy appear to be an unmodified upstream revision. | R |

### 8.3 Upstream updates

An upstream update is a new candidate revision, not an automatic replacement.

For every proposed update:

1. Identify the current adopted revision.
2. Identify the proposed upstream revision.
3. Record the revision difference.
4. Reassess license and provenance changes.
5. Review relevant source changes.
6. Evaluate technical compatibility.
7. Evaluate security and maintenance implications.
8. Review any changes to notices or attribution.
9. Record the update decision.
10. Preserve the history of the previous adopted revision.

A component MUST NOT be updated solely because a newer upstream release is available.

## 9. No Automatic Adoption

### 9.1 Adoption control

Discovery, download, cloning, mirroring, dependency resolution, or successful build integration MUST NOT be interpreted as approval for adoption.

Adoption requires an explicit decision.

The following activities are distinct:

| Activity | Meaning | Adoption approval implied? |
|---|---|---|
| Discovery | Identifying a possible upstream source. | No |
| Download | Obtaining a source copy for inspection. | No |
| Evaluation | Testing technical or functional suitability. | No |
| License review | Assessing rights and obligations. | No |
| Integration experiment | Testing compatibility in a controlled environment. | No |
| Adoption approval | Authorizing use within a defined scope. | Yes |
| Release approval | Authorizing inclusion in a specified release or distribution. | Separate decision |

### 9.2 Adoption requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-ADP-001 | Third-party material MUST NOT be adopted without an explicit ALLOW decision. | R |
| OSIP-ADP-002 | Adoption MUST identify the approved component revision and scope. | R |
| OSIP-ADP-003 | Adoption MUST preserve the upstream provenance record. | R |
| OSIP-ADP-004 | Adoption MUST identify required third-party notices and license obligations. | R |
| OSIP-ADP-005 | Automated dependency updates MUST NOT bypass the adoption review process. | R |
| OSIP-ADP-006 | A change in intended use, repository, or distribution scope MUST trigger an approval review. | R |
| OSIP-ADP-007 | An adopted component MUST be reassessed when material license, security, or provenance information changes. | R |

### 9.3 Automated tooling

Automation MAY assist with:

- Dependency discovery.
- License identification.
- License inventory generation.
- Source revision capture.
- Checksum generation.
- Change detection.
- Notice generation.
- Security scanning.
- Provenance report generation.

Automated results are evidence for review. They do not replace the required adoption decision.

A tool reporting a license or a clean scan MUST NOT be treated as final legal or security approval.

## 10. Third-Party Notices and Attribution

### 10.1 Notice preservation

All applicable third-party copyright, license, attribution, disclaimer, and notice requirements MUST be preserved.

KRITVA-authored files use the copyright holder wording `Kritva Robotics`. This wording applies only to KRITVA-authored material. It MUST NOT replace, remove, or obscure upstream copyright or license notices.

The exact obligations depend on the applicable license and the manner in which the component is used or distributed.

Where required, KRITVA distributions MUST include:

- Copyright notices.
- License text.
- Required attribution.
- Required modification notices.
- Required patent notices or disclaimers.
- Required source-offer or corresponding-source information.
- Other notices mandated by the applicable license.

### 10.2 Notice management

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-NOT-001 | Required upstream copyright and license notices MUST be retained. | R |
| OSIP-NOT-002 | Required third-party attribution MUST be included in the applicable distribution materials. | R |
| OSIP-NOT-003 | KRITVA modifications MUST NOT remove or obscure required upstream notices. | R |
| OSIP-NOT-004 | Third-party notices MUST be traceable to the corresponding adopted component. | R |
| OSIP-NOT-005 | A redistribution review MUST verify applicable notice obligations before release. | R |
| OSIP-NOT-006 | Notice changes resulting from an upstream update MUST be reviewed and recorded. | R |

### 10.3 Notice inventory

An adopted component SHOULD have a corresponding notice inventory containing:

- Component identifier.
- Upstream project name.
- License identifier and license text reference.
- Copyright holders.
- Attribution requirements.
- Modification notice requirements.
- Patent-related notices, if applicable.
- Redistribution obligations.
- Location of the applicable notice material.

The notice inventory MAY be maintained centrally or within the relevant repository, provided that it remains traceable and available during release review.

## 11. Upstream and KRITVA Record Separation

### 11.1 Record ownership

Upstream records and KRITVA records serve different purposes and MUST remain distinguishable.

| Record type | Ownership | Purpose |
|---|---|---|
| Upstream source | Original project or author | Original source material and upstream history. |
| Upstream license and notices | Original project or rights holder | Original legal and attribution terms. |
| Upstream release and revision history | Original project | Evidence of the source revision. |
| KRITVA intake record | KRITVA | Evaluation and adoption decision. |
| KRITVA provenance record | KRITVA | Traceability between upstream and adopted material. |
| KRITVA modification record | KRITVA | Description of local changes. |
| KRITVA verification evidence | KRITVA | Evidence of technical evaluation and validation. |
| KRITVA integration record | KRITVA | Approved use and integration scope. |
| KRITVA release record | KRITVA | Distribution and notice compliance evidence. |

### 11.2 Separation requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-SEP-001 | Upstream source history MUST remain distinguishable from KRITVA modification history. | R |
| OSIP-SEP-002 | KRITVA-specific decisions MUST NOT be represented as upstream project decisions. | R |
| OSIP-SEP-003 | Upstream license and notice material MUST NOT be replaced by a KRITVA license statement. | R |
| OSIP-SEP-004 | KRITVA modifications MUST be identifiable through source control history or an equivalent record. | R |
| OSIP-SEP-005 | The adopted upstream revision MUST remain recoverable from the provenance record. | R |
| OSIP-SEP-006 | KRITVA integration and verification evidence MUST be maintained as KRITVA records, not attributed to the upstream project. | R |

### 11.3 Repository organization

Repositories SHOULD use a structure that makes upstream content, KRITVA modifications, and integration material distinguishable.

The exact directory structure is repository-specific and is not prescribed by this public policy.

Possible approaches include:

- A separately maintained upstream source directory.
- A dedicated third-party component directory.
- A source-control submodule or subtree.
- A documented patch series.
- A maintained fork with explicit upstream tracking.

The selected approach MUST preserve provenance and make local modifications reviewable.

No specific repository layout is mandated by this document.

## 12. Public and Private Boundary

### 12.1 Public policy and records

Public KRITVA repositories MAY contain the information necessary to establish lawful use, provenance, and compliance, including:

- Upstream project names.
- Public upstream source locations.
- Public immutable revision identifiers.
- Public license identifiers and license texts.
- Public copyright and attribution notices.
- KRITVA-authored adoption decisions suitable for public disclosure.
- Publicly distributable modification records.
- Public verification results that do not disclose restricted information.
- Public third-party notice inventories.

Public disclosure MUST comply with applicable license terms and KRITVA release controls.

### 12.2 Private or restricted information

The following information MUST NOT be published in a public policy or public intake record unless explicitly cleared for release:

- Confidential vendor material.
- Proprietary IP source or implementation details.
- Non-public license agreements and commercial terms.
- Credentials, tokens, or access-controlled source locations.
- Private supplier correspondence.
- Security-sensitive vulnerability details not cleared for disclosure.
- Unreleased SoC architecture, implementation, or integration details.
- Private repository paths, branch names, or internal review artifacts that expose unreleased implementation information.
- Confidential technical or business information.

A public record MAY refer to a private review or approval without disclosing its restricted contents, provided the public record remains meaningful and does not imply an approval that has not occurred.

### 12.3 Public/private boundary requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-PUB-001 | Public records MUST contain only information approved for public disclosure. | R |
| OSIP-PUB-002 | Private or restricted third-party material MUST NOT be copied into a public repository without authorization. | R |
| OSIP-PUB-003 | Public provenance references MUST NOT expose confidential credentials or access tokens. | R |
| OSIP-PUB-004 | Unreleased SoC implementation details MUST remain outside this public policy and its public records. | R |
| OSIP-PUB-005 | Public documentation MUST distinguish public facts from private or pending decisions. | R |
| OSIP-PUB-006 | Public redistribution MUST satisfy the applicable third-party license and notice obligations. | R |
| OSIP-PUB-007 | Private evidence MAY be referenced through a non-sensitive identifier without publishing its contents. | R |

### 12.4 SoC-specific information

This policy applies across KRITVA IP development without publishing unreleased SoC architecture or implementation details.

SoC-specific adoption profiles, integration decisions, and restricted evidence remain governed by their respective SoC repositories and approved access controls.

This policy does not establish or disclose any unreleased Nexus or Edge implementation decision.

## 13. RTL Technology Boundary

### 13.1 Approved RTL library manifest

Third-party RTL adoption MUST comply with the technology boundary defined by the applicable KRITVA IP standard and SoC profile.

The approved RTL library manifest is the only permitted technology boundary for technology-dependent RTL dependencies.

A third-party RTL component MUST NOT introduce direct dependencies on unapproved technology-specific cells, libraries, or implementation primitives.

The manifest defines the approved reusable RTL technology boundary. It is not a blanket authorization to import arbitrary vendor or foundry collateral.

### 13.2 Technology boundary requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-TECH-001 | Technology-dependent RTL dependencies MUST be checked against the approved RTL library manifest. | R |
| OSIP-TECH-002 | The approved RTL library manifest MUST be the only technology boundary used by an adopted IP component. | R |
| OSIP-TECH-003 | Third-party RTL MUST NOT introduce direct foundry-cell dependencies outside the approved manifest. | R |
| OSIP-TECH-004 | Any proposed change to the approved technology boundary MUST be handled as an explicit owner decision. | R |
| OSIP-TECH-005 | An adopted component MUST identify any technology-dependent assumptions discovered during review. | R |
| OSIP-TECH-006 | Technology-dependent dependencies MUST NOT be treated as approved merely because they are present in upstream source. | R |

### 13.3 Reset and interface conventions

Third-party RTL intended for integration MUST be assessed against the applicable KRITVA IP standard and SoC profile.

The following conventions are part of the common assessment baseline:

- Reset signals are active-low by default.
- Reset naming follows `rst_<domain>_n_i`.
- Active-high reset usage requires an approved waiver with documented rationale.
- Port suffixes follow `_i`, `_o`, and `_io`.
- Sequential logic uses positive-edge triggering in accordance with the applicable standard.
- Reset synchronizers MUST be sourced from the approved RTL library manifest and MUST NOT be independently reimplemented within an IP component.

A third-party component that does not follow these conventions MUST be classified for review and assessed for the required adaptation or waiver.

The use of an upstream implementation does not exempt it from applicable KRITVA integration requirements.

## 14. Verification and Tooling

### 14.1 Tool assessment

Tools used to inspect, build, verify, or integrate third-party components MUST be identified in the relevant technical assessment.

Tool versions and configurations MUST be recorded when available and relevant to reproducibility.

**Tool versions for the current public policy baseline are UNVERIFIED.**

No tool version is asserted or approved by this document.

### 14.2 Tooling requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-TOOL-001 | Tools used for adoption assessment SHOULD be recorded with their versions and relevant configuration. | R |
| OSIP-TOOL-002 | Tool availability or successful execution MUST NOT be treated as evidence of license compatibility. | R |
| OSIP-TOOL-003 | Automated license and provenance scan results MUST be retained as review evidence where used. | R |
| OSIP-TOOL-004 | Tool versions MUST be marked UNVERIFIED when they have not been independently established. | R |
| OSIP-TOOL-005 | Tool output MUST NOT replace an explicit adoption decision. | R |

### 14.3 Verification evidence

The adoption review SHOULD include evidence appropriate to the component, such as:

- Source integrity and revision verification.
- Build and elaboration results.
- Lint results.
- Simulation results.
- Formal verification results, where applicable.
- Interface and reset compliance checks.
- Technology-boundary checks.
- Security and dependency scan results.
- Reproducibility observations.
- Known limitations and unresolved issues.

The evidence type and completeness depend on the component's intended use and risk.

## 15. Security and Maintenance Review

Third-party components introduce risks beyond licensing and technical functionality.

The review SHOULD consider:

- Known vulnerabilities.
- Security advisories.
- Unmaintained or abandoned upstream projects.
- Unreviewed source changes.
- Unnecessary functionality or dependencies.
- Build-time and runtime dependencies.
- Supply-chain integrity.
- Integrity of release artifacts.
- Security implications of generated code.
- Availability of upstream fixes.
- The impact of discontinuation or upstream license changes.

### 15.1 Security and maintenance requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-SEC-001 | Third-party candidates SHOULD undergo a security and maintenance assessment appropriate to their intended use. | R |
| OSIP-SEC-002 | Known security issues MUST be recorded before adoption. | R |
| OSIP-SEC-003 | A known unresolved security issue that makes the proposed use unacceptable MUST prevent adoption. | R |
| OSIP-SEC-004 | Material changes in upstream security status SHOULD trigger reassessment. | R |
| OSIP-SEC-005 | Abandoned or unmaintained components MUST have their maintenance risk documented before adoption. | R |
| OSIP-SEC-006 | Security scan results MUST NOT be represented as proof that a component is free from vulnerabilities. | R |

## 16. Adoption Review and Approval

### 16.1 Review stages

The following stages define the expected adoption workflow.

| Stage | Activity | Expected result |
|---|---|---|
| 1 | Candidate identification | Source and intended use identified. |
| 2 | Source classification | Source category assigned. |
| 3 | Provenance verification | Upstream origin and immutable revision recorded. |
| 4 | License assessment | License class and obligations recorded. |
| 5 | Technical assessment | Suitability and integration risks reviewed. |
| 6 | Security and maintenance assessment | Relevant risks recorded. |
| 7 | Notice assessment | Attribution and redistribution obligations identified. |
| 8 | Owner review | Decision and approved scope recorded. |
| 9 | Adoption | Approved source revision incorporated. |
| 10 | Verification and release review | Required evidence and distribution obligations checked. |

A stage MAY be combined with another stage when the review record preserves all required information.

### 16.2 Review roles

The following roles are used as functional responsibilities. Specific assignments for a repository or component MUST be recorded in its applicable review record.

| Role | Responsibility |
|---|---|
| Component proposer | Identifies the candidate and intended use. |
| Technical reviewer | Evaluates technical suitability, integration, and verification evidence. |
| License reviewer | Evaluates license classification and obligations. |
| Security reviewer | Evaluates security and maintenance risks. |
| Repository maintainer | Ensures repository records and source-control changes are consistent with the approval. |
| Owner / authorized approver | Records the adoption decision and approved scope. |

Dinesh Annayya is the owner for decisions and open items defined by this policy.

A reviewer's participation does not by itself constitute adoption approval.

### 16.3 Approval record

An adoption approval MUST record:

- Component ID and name.
- Upstream source and immutable revision.
- License classification and disposition.
- Approved scope of use.
- Review references and evidence.
- Required third-party notices.
- Known limitations and conditions.
- Approver and approval date.
- Any applicable expiry or reassessment condition.

An approval MUST NOT be inferred from a merged pull request, successful CI run, or repository presence alone.

## 17. Waivers and Exceptions

A deviation from this policy requires an explicit, documented exception.

An exception request MUST include:

- Requirement ID.
- Component and repository scope.
- Description of the requested deviation.
- Technical and legal rationale.
- Risk assessment.
- Impact on redistribution and notice obligations.
- Compensating controls, where applicable.
- Expiry or reassessment condition.
- Owner decision.

A waiver MUST NOT override applicable law, third-party license obligations, or contractual restrictions.

A waiver for one component or revision MUST NOT automatically apply to another component or a future upstream revision.

### 17.1 Waiver requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-WVR-001 | Policy deviations MUST be documented and approved before the affected adoption or release. | R |
| OSIP-WVR-002 | A waiver MUST identify the requirement and scope of the deviation. | R |
| OSIP-WVR-003 | A waiver MUST include rationale and risk assessment. | R |
| OSIP-WVR-004 | A waiver MUST NOT authorize violation of applicable license or contractual terms. | R |
| OSIP-WVR-005 | Waivers MUST be reviewed when their scope, assumptions, or risk conditions change. | R |

## 18. Records and Auditability

The relevant KRITVA repository or approved record location MUST preserve sufficient evidence to reconstruct the adoption decision.

The record set SHOULD include:

- Candidate intake record.
- Source classification.
- Provenance record.
- Immutable upstream revision.
- License assessment.
- Notice inventory.
- Technical assessment.
- Security and maintenance assessment.
- Adoption decision.
- Approved scope.
- Modification history.
- Verification evidence.
- Waivers and exceptions.
- Release compliance evidence.

Records MUST be maintained so that upstream source, KRITVA modifications, and KRITVA approval decisions can be independently distinguished.

This policy does not prescribe a central dependency database or a particular repository directory layout. The record location and implementation approach are subject to owner decisions and repository needs.

## 19. Enforcement and Assessment

### 19.1 Enforcement classes

The following assessment classes are aligned with the KRITVA IP standard and the enforcement classification used by `KNX-RTL-STD-001`.

| Class | Name | Meaning |
|---|---|---|
| A | Automated | A requirement that can be checked by an automated script, tool, or CI process. |
| T | Tool-assisted | A requirement for which tools can provide evidence, but human interpretation or review remains necessary. |
| R | Review only | A requirement that requires human review, judgment, or explicit approval. |

The enforcement class describes the expected assessment method. It does not reduce the normative force of a requirement.

For example, an A-class requirement remains mandatory even if its automated check has not yet been implemented.

### 19.2 Assessment principles

- Automated checks SHOULD be used where reliable and practical.
- Tool-assisted checks MUST retain enough evidence for review.
- Review-only requirements MUST have a documented review outcome.
- A passing automated check MUST NOT be treated as proof of license compatibility or legal approval.
- An unresolved mandatory requirement MUST prevent adoption or release within the affected scope.

### 19.3 Relationship to KRITVA IP Standard

This policy supplements `KRITVA_IP_STANDARD.md`.

The KRITVA IP Standard defines the cross-IP design and integration baseline. This policy defines the controls for third-party and open-source IP intake, licensing, provenance, adoption, and redistribution.

Where the two documents address the same subject:

1. Applicable legal and contractual obligations take precedence.
2. The stricter applicable KRITVA requirement governs.
3. Any unresolved conflict MUST be recorded as an owner decision.
4. A policy waiver MUST NOT silently alter the requirements of the KRITVA IP Standard.

### 19.4 Relationship to KNX-RTL-STD-001

`KNX-RTL-STD-001` is a SoC-specific RTL profile.

This public policy does not reproduce its detailed design rules or disclose unreleased SoC implementation information.

For third-party RTL considered for a SoC:

- The applicable cross-SoC KRITVA IP requirements MUST be assessed.
- The applicable SoC profile MUST also be assessed.
- A stricter applicable SoC requirement prevails within that SoC's scope.
- The approved RTL library manifest remains the technology boundary.
- Reset, port naming, and sequential logic conventions MUST be assessed against the applicable standards.
- The enforcement class A/T/R MUST be recorded where the applicable assessment requires it.

## 20. Public Release Compliance

Before a third-party component is included in a public KRITVA release, the release review MUST establish that:

1. The component has an ALLOW disposition for the intended public distribution.
2. The adopted upstream revision is identifiable.
3. The license and redistribution obligations are understood.
4. Required copyright, license, and attribution notices are present.
5. KRITVA modifications are distinguishable from upstream source.
6. Required source-disclosure obligations are satisfied.
7. No private or restricted material is included without authorization.
8. The release record identifies the component and applicable notices.

### 20.1 Release requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| OSIP-REL-001 | A component MUST NOT be included in a public release unless its disposition permits the intended distribution. | R |
| OSIP-REL-002 | Applicable third-party notices MUST be included in the release. | R |
| OSIP-REL-003 | Release records MUST identify adopted third-party components and their revisions. | R |
| OSIP-REL-004 | Public release review MUST verify that restricted material has not been unintentionally included. | R |
| OSIP-REL-005 | Required source-disclosure and redistribution obligations MUST be satisfied before release. | R |
| OSIP-REL-006 | Release approval MUST be recorded separately from the original adoption approval when the release scope or obligations differ. | R |

## 21. Document Maintenance

This document is maintained as a public KRITVA standard.

Changes MUST be reviewed for impact on:

- License classification and disposition rules.
- Provenance requirements.
- Adoption and update controls.
- Third-party notices.
- Public/private information boundaries.
- RTL technology boundary requirements.
- Enforcement and assessment methods.
- Related KRITVA standards.

A revision MUST NOT silently change the status of previously adopted components.

Where a policy change affects existing adoption decisions, the impact and required reassessment MUST be recorded.

### 21.1 Versioning

| Version change | Meaning |
|---|---|
| Major | Incompatible policy changes or changes to fundamental adoption and compliance requirements. |
| Minor | New policy requirements, classifications, or substantive additions that preserve the existing policy framework. |
| Patch | Editorial corrections, clarifications, and non-substantive changes. |

The version and status recorded in the document header MUST match the repository's committed version.

### 21.2 Approval status

The current document status is DRAFT.

Publication of this file does not, by itself, constitute owner approval of the open items or approval of any specific third-party component.

---

## 22. Open Items

The following items require explicit owner decisions. They are not approved policy exceptions or implied technical decisions.

Owner for all items: **Dinesh Annayya**.

| ID | Open item | Decision required | Owner | Status |
|---|---|---|---|---|
| OSIP-OI-001 | License allow-list | Approve a formal list of licenses eligible for the normal approval path. | Dinesh Annayya | OPEN |
| OSIP-OI-002 | License deny-list | Decide whether specific licenses should be prohibited by default, independent of component-level review. | Dinesh Annayya | OPEN |
| OSIP-OI-003 | Mandatory legal review | Define which license classes and usage scenarios require mandatory legal review. | Dinesh Annayya | OPEN |
| OSIP-OI-004 | Adoption approval authority | Confirm whether all third-party IP adoption decisions require owner approval or whether delegated approval roles may be defined. | Dinesh Annayya | OPEN |
| OSIP-OI-005 | Provenance record format | Select the canonical machine-readable provenance and intake record format. | Dinesh Annayya | OPEN |
| OSIP-OI-006 | Repository record location | Decide whether adoption records are maintained in each consuming repository, a shared repository, or both. | Dinesh Annayya | OPEN |
| OSIP-OI-007 | Upstream synchronization model | Select the preferred approach for tracking upstream revisions and carrying local modifications. | Dinesh Annayya | OPEN |
| OSIP-OI-008 | Automated license scanning | Select the license identification and compliance tooling and define its role in the approval process. | Dinesh Annayya | OPEN |
| OSIP-OI-009 | Security scanning baseline | Define the minimum security assessment and evidence required for different source categories. | Dinesh Annayya | OPEN |
| OSIP-OI-010 | Notice inventory format | Select a common third-party notice inventory format and release packaging approach. | Dinesh Annayya | OPEN |
| OSIP-OI-011 | Public/private review authority | Define who authorizes publication of records that refer to private adoption evidence or restricted dependencies. | Dinesh Annayya | OPEN |
| OSIP-OI-012 | Toolchain baseline | Define which tool versions and configurations should be recorded as the verified KRITVA baseline. Current tool versions remain UNVERIFIED. | Dinesh Annayya | OPEN |
| OSIP-OI-013 | Policy wording harmonization | DECIDED (2026-11-12): common standards use MUST; SHALL in approved profiles is equivalent in force. | Dinesh Annayya | DECIDED |
| OSIP-OI-014 | Enforcement-class harmonization | DECIDED (2026-11-12): A/T/R enforcement classes are adopted as-is across the KRITVA IP Standard, this policy, and applicable SoC profiles. | Dinesh Annayya | DECIDED |
| OSIP-OI-015 | Third-party RTL acceptance profile | Define any additional common technical acceptance checks for imported RTL beyond the requirements in the KRITVA IP Standard. | Dinesh Annayya | OPEN |
| OSIP-OI-016 | Restricted vendor collateral | Define the intake, storage, access, and review procedure for commercially licensed or restricted vendor collateral. | Dinesh Annayya | OPEN |
| OSIP-OI-017 | Policy reassessment cadence | Define a periodic review interval for adopted components and their license, security, and upstream status. | Dinesh Annayya | OPEN |

## 23. References

The following documents and records are relevant to this policy:

1. `KRITVA_IP_STANDARD.md` — Cross-SoC IP design and integration standard.
2. `KNX-RTL-STD-001` — Nexus SoC RTL design profile.
3. Applicable KRITVA repository contribution and release policies.
4. Applicable upstream license texts and copyright notices.
5. Applicable vendor agreements and third-party usage terms.
6. Applicable security advisories and upstream project records.

The references above do not imply that any particular third-party component, license, tool, or vendor has been approved for KRITVA adoption.

---

## 24. Change History

| Version | Date | Status | Description |
|---|---|---|---|
| 0.1.0 | 2026-11-12 | DRAFT | Initial public open-source IP policy covering source classification, licensing, provenance, adoption controls, notices, record separation, and public/private boundaries. |

---

**End of Document**