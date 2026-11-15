# KRITVA IP Adoption Process

| Field | Value |
|---|---|
| Document ID | KSTD-IPADP-001 |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | Public |
| Owner | Dinesh Annayya |
| Applies to | KRITVA IP repositories and third-party IP adoption activities |
| Related standard | `KRITVA_IP_STANDARD.md` |
| Related policy | `OPEN_SOURCE_IP_POLICY.md` |
| Related SoC profile | `KNX-RTL-STD-001` |
| Last updated | 2026-11-13 |

---

## 1. Purpose

This document defines the controlled process for discovering, evaluating, approving, integrating, and maintaining IP components within the KRITVA ecosystem.

It establishes a repeatable adoption lifecycle that ensures:

- Candidate IP is identified and its intended use is documented.
- Source provenance and licensing are established before adoption.
- Technical, verification, security, and maintenance suitability are assessed.
- Integration readiness is checked against the KRITVA IP Standard.
- Technology dependencies remain within the approved RTL library manifest.
- Adoption decisions are explicit and traceable.
- ALLOW, REVIEW, and DENY outcomes are applied consistently.
- Adoption records and supporting evidence remain available for audit and future reassessment.

This document defines a process, not an approval of any specific IP, upstream project, tool, implementation, or SoC integration.

## 2. Scope

This process applies to:

- KRITVA-developed IP intended for reuse.
- Third-party open-source IP.
- Vendor-provided IP and collateral.
- Reference implementations.
- Imported RTL and verification components.
- Firmware, software, and supporting IP components.
- Generated IP collateral and source.
- IP dependencies required by build, verification, and integration flows.

The process applies to new adoption, upstream updates, replacement of an existing component, changes in intended use, and changes in distribution scope.

This process does not replace:

- `KRITVA_IP_STANDARD.md`, which defines the cross-SoC IP design and integration baseline.
- `OPEN_SOURCE_IP_POLICY.md`, which defines third-party source, license, provenance, and redistribution controls.
- Applicable SoC-specific RTL profiles.
- Repository-specific contribution and release procedures.
- Legal or contractual review obligations.

## 3. Normative Language

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used as normative terms.

The common KRITVA standards use RFC 2119 `MUST` terminology. The `SHALL` terminology used by `KNX-RTL-STD-001` is equivalent in normative force to `MUST`.

KRITVA-authored files use the copyright holder wording `Kritva Robotics`. This wording MUST NOT replace or obscure upstream copyright and license notices in adopted IP.

Where multiple applicable standards impose requirements on the same subject, the stricter applicable requirement governs within its scope.

An approval under this process does not waive or override requirements in an applicable standard or license.

## 4. Adoption Principles

| ID | Principle | Description |
|---|---|---|
| ADP-PR-001 | Explicit adoption | No IP is adopted solely because it has been discovered, downloaded, evaluated, or successfully built. |
| ADP-PR-002 | Traceability | Every adopted IP component has an identifiable source, revision, and adoption record. |
| ADP-PR-003 | License compliance | Adoption and redistribution comply with applicable license and contractual obligations. |
| ADP-PR-004 | Technical suitability | IP is evaluated against its intended functional and integration requirements. |
| ADP-PR-005 | Evidence-based decisions | Adoption decisions are supported by technical, licensing, security, and integration evidence appropriate to the component. |
| ADP-PR-006 | Controlled integration | Integration occurs only after the required adoption gates have been satisfied. |
| ADP-PR-007 | Technology boundary | Technology-dependent RTL uses only the approved RTL library manifest as its technology boundary. |
| ADP-PR-008 | Verification evidence | Verification outcomes and evidence are recorded in a reproducible and reviewable form. |
| ADP-PR-009 | Separation of records | Upstream source history, KRITVA modifications, and KRITVA adoption decisions remain distinguishable. |
| ADP-PR-010 | Reassessment | Material changes to source, license, security status, or intended use trigger reassessment. |

## 5. Adoption Lifecycle

The adoption lifecycle consists of the following stages.

| Stage | Name | Primary activity | Exit condition |
|---|---|---|---|
| ADP-ST-01 | Discovery | Identify candidate IP and intended use. | Candidate identified and discovery record created. |
| ADP-ST-02 | Initial screening | Check source availability, apparent licensing, and basic suitability. | Candidate proceeds to evaluation or is rejected. |
| ADP-ST-03 | Intake | Create the formal IP intake record. | Required intake fields completed or explicitly marked pending. |
| ADP-ST-04 | Provenance and license assessment | Verify origin, immutable revision, rights, and obligations. | Provenance and license disposition recorded. |
| ADP-ST-05 | Technical assessment | Evaluate functionality, architecture, quality, and maintainability. | Technical assessment completed. |
| ADP-ST-06 | Verification and evidence assessment | Assess existing verification evidence and define KVRF-schema evidence needs for adoption. | Verification and evidence assessment recorded. |
| ADP-ST-07 | Security and maintenance assessment | Evaluate security, supply-chain, and upstream maintenance risks. | Security and maintenance assessment completed or risks explicitly recorded. |
| ADP-ST-08 | Integration-readiness assessment | Check compliance with the KRITVA IP Standard and applicable profile. | Integration-readiness result recorded. |
| ADP-ST-09 | Adoption decision | Assign ALLOW, REVIEW, or DENY. | Authorized decision recorded. |
| ADP-ST-10 | Controlled integration | Incorporate approved IP and retain provenance. | Integration evidence and records updated. |
| ADP-ST-11 | Verification and release readiness | Verify the integrated component and applicable distribution obligations. | Required evidence and release conditions satisfied. |
| ADP-ST-12 | Maintenance and reassessment | Track updates, issues, and changed conditions. | Adoption status remains valid or is revised. |

A stage MAY be combined with another stage if all required checks and evidence remain identifiable.

A candidate MUST NOT bypass a mandatory stage merely because the upstream project is widely used, has a successful release, or is already used by another organization.

## 6. Stage 1 — Discovery

### 6.1 Discovery sources

Candidate IP MAY be discovered through:

- Public open-source repositories.
- Standards organizations.
- Academic and research projects.
- Vendor documentation and public collateral.
- Existing KRITVA repositories.
- Internal engineering proposals.
- Known reference implementations.
- Existing dependency inventories.
- Community recommendations.

Discovery does not establish suitability, license compatibility, or approval.

### 6.2 Discovery information

The proposer SHOULD record:

- Candidate name.
- Source project or provider.
- Public source location, if available.
- General IP category.
- Intended KRITVA use.
- Expected functionality.
- Initial technical rationale.
- Known alternatives.
- Known restrictions or concerns.
- Proposer and discovery date.

### 6.3 Discovery requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-DIS-001 | A candidate MUST have a documented intended use before formal evaluation. | R |
| ADP-DIS-002 | The original source or provider SHOULD be identified during discovery. | R |
| ADP-DIS-003 | Discovery MUST NOT be interpreted as adoption approval. | R |
| ADP-DIS-004 | Candidates with an apparent legal or contractual restriction MUST be identified for initial review. | R |
| ADP-DIS-005 | Unreleased implementation details MUST NOT be included in public discovery records. | R |

## 7. Stage 2 — Initial Screening

Initial screening determines whether a candidate is suitable for detailed evaluation.

### 7.1 Screening checks

| Check ID | Screening area | Questions |
|---|---|---|
| SCR-001 | Functional fit | Does the candidate address an identified KRITVA requirement? |
| SCR-002 | Source availability | Is the source or provider identifiable and accessible under valid terms? |
| SCR-003 | License visibility | Is a license or usage basis identifiable? |
| SCR-004 | Maintenance | Is the project maintained or otherwise supportable? |
| SCR-005 | Technical maturity | Is there sufficient documentation and implementation evidence? |
| SCR-006 | Verification | Is there evidence of testing or verification? |
| SCR-007 | Integration | Does the candidate appear compatible with the intended KRITVA IP interface and integration model? |
| SCR-008 | Security | Are there known security or supply-chain concerns? |
| SCR-009 | Alternatives | Are there simpler or more suitable alternatives? |
| SCR-010 | Scope | Is the proposed use consistent with the available license and intended distribution? |

### 7.2 Screening outcomes

| Outcome | Meaning |
|---|---|
| PROCEED | Candidate is suitable for formal intake and detailed evaluation. |
| HOLD | More information is required before formal evaluation can proceed. |
| REJECT | Candidate is unsuitable or has a blocking issue. |

A screening outcome is not the formal ALLOW, REVIEW, or DENY adoption decision.

### 7.3 Screening requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-SCR-001 | Initial screening MUST record its outcome and rationale. | R |
| ADP-SCR-002 | A candidate with an unresolved rights or provenance blocker MUST NOT proceed to adoption. | R |
| ADP-SCR-003 | A REJECT decision MUST include the reason for rejection. | R |
| ADP-SCR-004 | A HOLD candidate MUST identify the missing information or action required to proceed. | R |

## 8. Stage 3 — IP Intake Record

### 8.1 Intake record creation

A formal intake record MUST be created for every candidate that proceeds to detailed evaluation.

The intake record is the primary reference linking discovery, assessments, adoption decisions, integration evidence, and later reassessments.

Each candidate MUST have a stable KRITVA component identifier.

The identifier MUST remain stable across revisions of the same adopted component. A different component MUST receive a different identifier.

The identifier format is repository or programme controlled and MUST NOT conflict with the requirement-ID namespaces defined by the KRITVA standards.

### 8.2 Required intake fields

| Field | Description |
|---|---|
| Intake ID | Stable identifier for the adoption intake. |
| Component ID | Stable identifier for the candidate IP component. |
| Component name | Name of the candidate. |
| Component category | Functional category of the IP. |
| Source category | Source classification from `OPEN_SOURCE_IP_POLICY.md`. |
| Proposer | Person or team proposing adoption. |
| Intended use | Proposed KRITVA use and scope. |
| Target repository | Intended repository or controlled destination. |
| Upstream organization | Original project, author, or provider. |
| Upstream location | Authoritative source location, where available. |
| Upstream revision | Immutable commit or equivalent revision, when available. |
| Release identifier | Upstream release or tag, if applicable. |
| License | Identified license and relevant exceptions. |
| Initial disposition | PROCEED, HOLD, or REJECT from screening. |
| Technical reviewer | Assigned technical reviewer. |
| License reviewer | Assigned license reviewer. |
| Security reviewer | Assigned security reviewer. |
| Assessment status | Current state of required assessments. |
| Adoption disposition | ALLOW, REVIEW, or DENY, once decided. |
| Decision owner | Authorized adoption approver. |
| Decision date | Date of the adoption decision. |
| Evidence references | References to assessment and verification evidence. |
| Known limitations | Known constraints and unresolved issues. |

Fields that are not yet known MUST be marked TBD or UNKNOWN rather than populated with assumptions.

### 8.3 Intake requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-INT-001 | Every candidate entering formal evaluation MUST have an intake record. | R |
| ADP-INT-002 | Every intake record MUST identify the component and intended use. | R |
| ADP-INT-003 | Unknown information MUST be explicitly marked TBD or UNKNOWN. | R |
| ADP-INT-004 | The intake record MUST link to all subsequent assessment and decision records. | R |
| ADP-INT-005 | The intake record MUST preserve the history of material changes and decisions. | R |
| ADP-INT-006 | The intake record MUST distinguish upstream facts from KRITVA assessment results. | R |

## 9. Stage 4 — Provenance and License Assessment

This stage follows the requirements of `OPEN_SOURCE_IP_POLICY.md`.

### 9.1 Provenance assessment

The reviewer MUST establish, where applicable:

- Original source project and owner.
- Authoritative upstream repository.
- Immutable upstream commit or equivalent revision.
- Release identifier.
- Source snapshot integrity.
- Original copyright and attribution information.
- Relationship between upstream source and any local modifications.
- Any generated or copied content.
- Any additional source dependencies.

A mutable branch name MUST NOT be the only reference to an adopted upstream revision.

### 9.2 License assessment

The license reviewer MUST assess:

- License identity.
- File-level license differences.
- Additional license terms and exceptions.
- Modification obligations.
- Redistribution obligations.
- Notice and attribution requirements.
- Source-disclosure obligations.
- Patent provisions.
- Compatibility with the intended use and distribution model.
- Any vendor or commercial restrictions.

The license assessment MUST assign a license class and record the proposed disposition.

### 9.3 Provenance and license gate

| Check ID | Check | Required result |
|---|---|---|
| PRO-001 | Source origin | Identifiable and recorded. |
| PRO-002 | Immutable revision | Recorded or explicitly marked unavailable with a blocking or review rationale. |
| PRO-003 | Source integrity | Verified where practical and relevant. |
| PRO-004 | Copyright | Original notices identified and preserved. |
| LIC-001 | License identity | Established or explicitly unresolved. |
| LIC-002 | License obligations | Relevant obligations documented. |
| LIC-003 | Intended use | Assessed against applicable terms. |
| LIC-004 | Redistribution | Assessed for the intended distribution scope. |
| LIC-005 | Additional restrictions | Identified and resolved or escalated. |

An unresolved license or rights blocker MUST prevent ALLOW.

### 9.4 Assessment requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-LIC-001 | Provenance and license assessment MUST follow `OPEN_SOURCE_IP_POLICY.md`. | R |
| ADP-LIC-002 | Adopted upstream material MUST be associated with an immutable revision or equivalent verifiable reference. | R |
| ADP-LIC-003 | License obligations MUST be assessed against the intended use and distribution scope. | R |
| ADP-LIC-004 | Original upstream notices MUST be preserved. | R |
| ADP-LIC-005 | A candidate with unresolved usage rights MUST NOT receive ALLOW. | R |
| ADP-LIC-006 | Upstream and KRITVA-owned records MUST remain distinguishable. | R |
| ADP-LIC-007 | Changes to upstream revision or license MUST trigger reassessment. | R |

## 10. Stage 5 — Technical Assessment

### 10.1 Technical objectives

The technical assessment determines whether the candidate is functionally and architecturally suitable for its intended use.

It SHOULD evaluate:

- Functional completeness.
- Interface definition and compatibility.
- Parameterization and configurability.
- Reset and clock behavior.
- Data and control interfaces.
- Performance characteristics.
- Resource utilization, where evidence is available.
- Timing and latency characteristics.
- Memory and buffering requirements.
- Error handling and recovery behavior.
- Portability.
- Maintainability.
- Documentation quality.
- Verification maturity.
- Known limitations and technical debt.

The assessment MUST distinguish verified properties from assumptions and estimates.

### 10.2 Functional and interface checks

The reviewer SHOULD establish:

1. What function the IP provides.
2. What function is outside its scope.
3. What interfaces it exposes.
4. What interfaces and dependencies it requires.
5. Which parameters affect behavior.
6. Which operating assumptions are required.
7. How reset and clock behavior are specified.
8. How errors and exceptional conditions are handled.
9. What evidence supports the claimed functionality.
10. What adaptation is required for KRITVA integration.

### 10.3 Technical maturity

The assessment SHOULD consider:

- Source completeness.
- Documentation completeness.
- Design quality.
- Coding consistency.
- Lint and elaboration results.
- Verification coverage and quality.
- Reproducibility.
- Issue history.
- Upstream maintenance activity.
- Compatibility with the intended development and release process.

A candidate MUST NOT be considered technically approved solely because it elaborates or passes a basic simulation.

### 10.4 Technical assessment requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-TEC-001 | Technical suitability MUST be assessed against the documented intended use. | R |
| ADP-TEC-002 | Functional scope and known limitations MUST be recorded. | R |
| ADP-TEC-003 | Interface and parameter assumptions MUST be documented. | R |
| ADP-TEC-004 | Technical claims MUST be distinguished from verified evidence. | R |
| ADP-TEC-005 | Required adaptation MUST be identified before adoption approval. | R |
| ADP-TEC-006 | Known technical blockers MUST be recorded and resolved or explicitly dispositioned. | R |
| ADP-TEC-007 | Technical assessment MUST identify the applicable KRITVA standards and profiles. | R |

## 11. Stage 6 — Verification and Evidence Assessment

### 11.1 Evidence-based verification policy

KRITVA IP adoption is outcome and evidence based.

Verification methodology is selected according to the component type, development origin, maturity, and intended integration level.

The verification record MUST make the tested behavior, test environment, execution result, and supporting evidence identifiable.

A tool name or successful command invocation alone is not sufficient evidence of correctness.

### 11.2 KVRF reference flow

KVRF/cocotb is the default reference verification flow for new KRITVA-developed IP at Level 2 (L2) and above.

The applicable KVRF evidence schema defines the expected machine-readable evidence records.

An equivalent verification flow MAY be used when it produces evidence records conforming to the KVRF schema.

The use of an equivalent flow MUST NOT be interpreted as an exemption from the required verification outcomes or evidence.

### 11.3 Upstream IP verification

Upstream IP MAY retain its native testbenches and verification methodology.

For adoption into KRITVA, upstream IP at the applicable integration level MUST have a wrapper-level KVRF test that produces KVRF-schema evidence.

The wrapper-level test SHOULD exercise the adopted component through its intended integration interface and verify the behavior relevant to the KRITVA use case.

The wrapper-level test does not require replacing or rewriting the upstream testbench.

### 11.4 Evidence content

Verification evidence SHOULD identify:

- Component ID and source revision.
- Test or verification suite identifier.
- Verification methodology.
- Tool and configuration information.
- Test environment.
- Test inputs and relevant configuration.
- Execution result.
- Pass, fail, or inconclusive status.
- Logs and reports.
- Relevant coverage or assertion results.
- Known limitations.
- Evidence artifact references.

Tool versions that have not been independently established MUST be marked UNVERIFIED.

### 11.5 Verification requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-VER-001 | Verification MUST be assessed against the intended use and integration level. | R |
| ADP-VER-002 | New KRITVA-developed IP at L2+ MUST use KVRF/cocotb as the default reference flow. | R |
| ADP-VER-003 | An equivalent verification flow MAY be used if it produces evidence records conforming to the KVRF schema. | R |
| ADP-VER-004 | Upstream IP MAY retain its native testbench, with a wrapper-level KVRF test for the adopted integration scope. | R |
| ADP-VER-005 | Verification results MUST identify the tested source revision and relevant configuration. | R |
| ADP-VER-006 | Verification evidence MUST distinguish PASS, FAIL, and INCONCLUSIVE outcomes. | R |
| ADP-VER-007 | Tool versions MUST be marked UNVERIFIED when not independently established. | R |
| ADP-VER-008 | Adoption MUST NOT be approved solely on the basis of a successful build or elaboration. | R |
| ADP-VER-009 | Verification evidence MUST be retained or referenced by the intake record. | R |

## 12. Stage 7 — Security and Maintenance Assessment

### 12.1 Security assessment

The security reviewer SHOULD assess:

- Known vulnerabilities.
- Security advisories.
- Untrusted source or build dependencies.
- External downloads during build or verification.
- Unnecessary privileges.
- Unsafe scripts or generated artifacts.
- Supply-chain integrity.
- Integrity of upstream release artifacts.
- Security-sensitive functionality.
- Known weaknesses in the component's design or implementation.

The depth of assessment MUST be appropriate to the component's intended use and exposure.

### 12.2 Maintenance assessment

The reviewer SHOULD consider:

- Upstream maintenance status.
- Release frequency and stability.
- Issue and defect history.
- Availability of fixes.
- Number and nature of external dependencies.
- Documentation and support.
- Risk of upstream abandonment.
- Ability to maintain a KRITVA-controlled fork if required.

### 12.3 Security and maintenance requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-SEC-001 | Security risks MUST be assessed and recorded before adoption. | R |
| ADP-SEC-002 | Known unresolved vulnerabilities MUST be recorded with their impact and disposition. | R |
| ADP-SEC-003 | A security issue that makes the intended use unacceptable MUST prevent ALLOW. | R |
| ADP-SEC-004 | Maintenance and upstream continuity risks SHOULD be assessed. | R |
| ADP-SEC-005 | Material changes to security or maintenance status SHOULD trigger reassessment. | R |
| ADP-SEC-006 | Security scan results MUST NOT be represented as proof that the component is vulnerability-free. | R |

## 13. Stage 8 — Integration-Readiness Assessment

### 13.1 Purpose

Integration readiness determines whether the candidate can be integrated into KRITVA IP development under the applicable standards.

The assessment MUST use `KRITVA_IP_STANDARD.md` as the common IP baseline.

The applicable SoC-specific profile MUST also be checked for the intended integration.

This section defines public integration criteria without disclosing unreleased SoC architecture or implementation details.

### 13.2 Standard compliance

The reviewer MUST check the candidate against the applicable requirements for:

- IP identity and documentation.
- Module and interface conventions.
- Parameterization.
- Clock and reset behavior.
- Verification and evidence.
- Technology dependencies.
- Memory and interface wrappers.
- Integration hooks.
- Quality and maintainability.
- Release and provenance records.

Any deviation MUST be recorded with its requirement ID, rationale, risk, and proposed resolution.

### 13.3 Control and register interface

The common KRITVA IP integration baseline identifies APB as the primary control and register interface (owner decision, 2026-11-12).

The APB revision and profile remain TBD pending the applicable owner decision.

The reviewer MUST assess:

- Whether the IP exposes a suitable control/register interface.
- Whether the interface is compatible with the applicable KRITVA standard and integration profile.
- Whether register access behavior is documented.
- Whether reset and clock assumptions are explicit.
- Whether any required interface bridge is documented.
- Whether any non-standard control interface requires an explicit integration decision.

The following interface policy applies:

| Interface | Adoption assessment |
|---|---|
| APB | Primary control/register interface (owner decision, 2026-11-12); revision and profile TBD. |
| AXI4 | Permitted for data or high-bandwidth interfaces where justified. |
| AXI4-Lite | Permitted through a documented bridge. |
| AHB-Lite | Permitted through a documented bridge. |
| Wishbone | Permitted through a documented bridge. |
| Other interface | Requires documented technical assessment and owner disposition. |

This policy does not establish an APB revision, timing profile, or implementation-specific configuration.

### 13.4 Clock and reset readiness

The candidate MUST be assessed for:

- Clock inputs and outputs.
- Clock-domain assumptions.
- Reset inputs and outputs.
- Reset assertion and deassertion behavior.
- Reset-domain interactions.
- Reset synchronizer usage.
- Clock and reset dependencies across interfaces.

The common reset baseline is active-low.

Reset naming follows:

`rst_<domain>_n_i`

Active-high reset usage requires an approved waiver with documented rationale.

Reset synchronizers MUST be sourced from the approved RTL library manifest. An IP component MUST NOT independently reimplement a reset synchronizer where the approved library provides the required implementation.

### 13.5 Port naming and sequential logic

The candidate MUST be assessed against the applicable common naming and sequential logic conventions:

- Input ports use `_i`.
- Output ports use `_o`.
- Bidirectional ports use `_io`.
- Sequential logic uses positive-edge triggering as required by the applicable standard.
- Any deviation is recorded and assessed before adoption.

### 13.6 Approved RTL library manifest

The approved RTL library manifest is the only technology boundary for technology-dependent RTL dependencies.

The reviewer MUST identify:

- Technology-dependent modules or primitives.
- Any direct cell or library references.
- Any vendor-specific implementation dependencies.
- Any clock-gating dependencies.
- Any reset synchronizer dependencies.
- Any CDC, FIFO, or memory-wrapper dependencies.
- Any technology-specific assumptions embedded in the source.

A candidate MUST NOT introduce unapproved technology-specific cells or direct foundry-cell dependencies outside the approved manifest.

The existence of a dependency in upstream source does not make it an approved KRITVA technology dependency.

### 13.7 Integration-readiness checklist

| Check ID | Area | Acceptance condition |
|---|---|---|
| IR-001 | Documentation | Functional scope and interfaces are documented. |
| IR-002 | Identity | Component identity and source revision are traceable. |
| IR-003 | Parameters | Parameters and supported configurations are documented. |
| IR-004 | Control interface | Control/register interface is assessed against the APB-primary baseline and applicable profile. |
| IR-005 | Data interface | Data or high-bandwidth interfaces are justified and documented. |
| IR-006 | Bridge requirements | Non-primary control interfaces have documented bridge requirements. |
| IR-007 | Clock | Clock assumptions and dependencies are documented. |
| IR-008 | Reset polarity | Active-low reset convention is followed or an approved waiver exists. |
| IR-009 | Reset naming | Reset naming is assessed against `rst_<domain>_n_i`. |
| IR-010 | Reset synchronizer | Reset synchronizer usage complies with the approved RTL library manifest. |
| IR-011 | Port naming | Port suffix conventions are followed or deviations are dispositioned. |
| IR-012 | Sequential logic | Sequential logic conventions are assessed against the applicable standard. |
| IR-013 | Technology boundary | Technology dependencies are within the approved RTL library manifest. |
| IR-014 | Memory and wrappers | Required memory and interface wrappers are identified and assessed. |
| IR-015 | Verification | Required verification outcomes and KVRF-schema evidence are available. |
| IR-016 | Quality | Lint, elaboration, and other applicable quality evidence is reviewed. |
| IR-017 | Security | Security findings and unresolved risks are recorded. |
| IR-018 | License | License and redistribution obligations are understood. |
| IR-019 | Provenance | Immutable upstream revision and source origin are recorded. |
| IR-020 | Integration limitations | Known integration limitations are documented. |

### 13.8 Integration-readiness result

Each checklist item MUST receive one of the following results:

| Result | Meaning |
|---|---|
| PASS | Requirement satisfied with sufficient evidence. |
| FAIL | Requirement not satisfied. |
| WAIVED | A valid, approved waiver applies. |
| NOT APPLICABLE | Requirement does not apply, with rationale. |
| UNKNOWN | Evidence is unavailable or insufficient. |

UNKNOWN MUST NOT be treated as PASS.

A FAIL or UNKNOWN result affecting a mandatory adoption requirement MUST prevent ALLOW until resolved or explicitly handled through an applicable approved exception.

### 13.9 Integration-readiness requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-IR-001 | Integration readiness MUST be assessed against `KRITVA_IP_STANDARD.md`. | R |
| ADP-IR-002 | The applicable SoC profile MUST be considered for the intended integration. | R |
| ADP-IR-003 | The primary control/register interface MUST be assessed against the APB-primary baseline. | R |
| ADP-IR-004 | The APB revision and profile MUST remain TBD until approved by the owner. | R |
| ADP-IR-005 | Active-low reset convention and reset naming MUST be assessed. | R |
| ADP-IR-006 | Reset synchronizer usage MUST comply with the approved RTL library manifest. | R |
| ADP-IR-007 | Technology-dependent RTL dependencies MUST be checked against the approved RTL library manifest. | R |
| ADP-IR-008 | Port naming and sequential logic conventions MUST be assessed. | R |
| ADP-IR-009 | Integration deviations MUST be recorded with rationale and disposition. | R |
| ADP-IR-010 | UNKNOWN integration results MUST NOT be treated as PASS. | R |

## 14. Stage 9 — Adoption Decision Gates

### 14.1 Decision model

Every formally evaluated candidate MUST receive one of three adoption dispositions:

- ALLOW
- REVIEW
- DENY

The decision MUST be recorded against the intake ID and component revision.

The disposition describes the current adoption decision. It does not replace stage-specific screening outcomes or verification results.

### 14.2 ALLOW

ALLOW means the candidate has passed the required adoption assessments for a defined scope.

An ALLOW decision requires:

1. Identifiable source and provenance.
2. Established license or legal basis.
3. Acceptable technical suitability.
4. Acceptable security and maintenance risk.
5. Completed integration-readiness assessment.
6. Required verification evidence.
7. Identified notice and attribution obligations.
8. Resolved mandatory blockers.
9. Explicit approval by the authorized owner or delegate.
10. A recorded approved scope.

ALLOW MUST identify whether the component is approved for:

- Evaluation or development use.
- Integration into a KRITVA IP repository.
- Reuse by other KRITVA IP components.
- Inclusion in a public KRITVA release.
- Inclusion in a restricted or commercial distribution.

Approval for one scope MUST NOT imply approval for another.

### 14.3 REVIEW

REVIEW means the candidate may remain under evaluation but is not approved for adoption.

REVIEW is required when:

- License interpretation is incomplete.
- Provenance evidence is incomplete.
- Technical evidence is insufficient.
- Security findings remain unresolved.
- Integration readiness is incomplete.
- Required verification evidence is missing.
- Owner decisions remain pending.
- Required notices or redistribution obligations are not yet established.
- A proposed waiver has not been approved.

The review record MUST identify the outstanding conditions and the actions required to reach a decision.

### 14.4 DENY

DENY means the candidate is not approved for adoption under the current proposal.

DENY applies when:

- The source is unauthorized or cannot be established.
- Usage rights do not permit the intended use.
- License obligations are incompatible with the intended distribution.
- A blocking technical issue cannot be acceptably resolved.
- Security risk is unacceptable.
- Mandatory integration requirements cannot be satisfied.
- Required approval is refused.
- The candidate is otherwise unsuitable for the intended scope.

A DENY decision MUST include a reason.

A later proposal MAY reopen a denied candidate if material facts change. The original decision record MUST remain available.

### 14.5 Decision gate table

| Gate | Gate name | Required evidence | Blocking condition |
|---|---|---|---|
| GATE-01 | Discovery | Candidate and intended use | Candidate cannot be identified. |
| GATE-02 | Intake | Complete intake record | Required identity and scope information missing. |
| GATE-03 | Provenance | Source and immutable revision | Origin or source rights unresolved. |
| GATE-04 | License | License assessment | Intended use is not legally permitted or remains unresolved. |
| GATE-05 | Technical | Technical assessment | Unacceptable functional or implementation limitation. |
| GATE-06 | Security | Security and maintenance assessment | Unacceptable unresolved security risk. |
| GATE-07 | Integration | Integration-readiness checklist | Mandatory integration requirement fails or remains unknown. |
| GATE-08 | Verification | Required verification evidence | Required verification outcome or evidence missing. |
| GATE-09 | Adoption | Explicit authorized decision | No recorded ALLOW decision. |
| GATE-10 | Release | Notice and distribution compliance | Release obligations are not satisfied. |

### 14.6 Decision requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-DEC-001 | Every evaluated candidate MUST receive ALLOW, REVIEW, or DENY. | R |
| ADP-DEC-002 | ALLOW MUST identify the approved component revision and scope. | R |
| ADP-DEC-003 | REVIEW MUST identify outstanding conditions and required actions. | R |
| ADP-DEC-004 | DENY MUST include a documented rationale. | R |
| ADP-DEC-005 | Adoption MUST NOT proceed without an explicit ALLOW decision. | R |
| ADP-DEC-006 | Adoption decisions MUST be recorded with the authorized approver and decision date. | R |
| ADP-DEC-007 | Approval for development use MUST NOT imply public redistribution approval. | R |
| ADP-DEC-008 | A change in revision, license, intended use, or distribution scope MUST trigger reassessment. | R |

## 15. Stage 10 — Controlled Integration

### 15.1 Integration prerequisites

A candidate MAY enter controlled integration only when:

- Its disposition is ALLOW.
- The approved upstream revision is identified.
- The approved use scope is documented.
- Required license and notice records are available.
- Required technical and verification conditions are satisfied.
- Applicable integration requirements are met.
- Required waivers have been approved.
- The destination repository and integration owner are identified.

### 15.2 Integration controls

During integration:

1. Preserve the upstream source reference.
2. Preserve original notices and license material.
3. Identify KRITVA modifications.
4. Record local patches or adaptation changes.
5. Maintain reproducible source references.
6. Retain verification evidence.
7. Record integration dependencies.
8. Ensure that technology-dependent RTL complies with the approved RTL library manifest.
9. Ensure that the applicable IP Standard and SoC profile are followed.
10. Update the intake record with the integration result.

### 15.3 Integration requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-INTG-001 | Only ALLOW components MAY enter approved integration. | R |
| ADP-INTG-002 | Integration MUST use the approved source revision. | R |
| ADP-INTG-003 | Upstream source and KRITVA modifications MUST remain distinguishable. | R |
| ADP-INTG-004 | Required third-party notices MUST be retained. | R |
| ADP-INTG-005 | Integration dependencies MUST be recorded. | R |
| ADP-INTG-006 | Integration MUST preserve the approved technology boundary. | R |
| ADP-INTG-007 | Integration changes MUST be traceable through source control or equivalent records. | R |
| ADP-INTG-008 | Integration evidence MUST be linked to the intake record. | R |

## 16. Stage 11 — Verification and Release Readiness

### 16.1 Integrated verification

After integration, the component MUST be verified in the context of its intended KRITVA use.

The verification plan SHOULD cover:

- Interface behavior.
- Reset behavior.
- Clock assumptions.
- Parameter configurations.
- Error and boundary conditions.
- Integration dependencies.
- Required functional behavior.
- Regression stability.
- Relevant assertions and coverage.
- Known limitations.

KVRF-schema evidence requirements apply as described in Section 11.

Equivalent verification flows are permitted when they provide the required KVRF-schema evidence.

### 16.2 Release readiness

Before public or restricted release, the release reviewer MUST check:

- Adoption disposition.
- Approved source revision.
- Applicable license and redistribution conditions.
- Required third-party notices.
- KRITVA modification records.
- Required verification evidence.
- Security findings and dispositions.
- Public/private boundary compliance.
- Release-specific approval.

A component approved for internal development MUST NOT automatically be included in a public release.

### 16.3 Release requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-REL-001 | Integrated verification evidence MUST be retained or referenced. | R |
| ADP-REL-002 | Release readiness MUST be assessed separately from adoption approval. | R |
| ADP-REL-003 | Public release MUST satisfy applicable license and notice obligations. | R |
| ADP-REL-004 | Restricted material MUST NOT be included in public releases without authorization. | R |
| ADP-REL-005 | Release records MUST identify the adopted component revision. | R |
| ADP-REL-006 | Release approval MUST be recorded for the intended distribution scope. | R |

## 17. Stage 12 — Maintenance and Reassessment

### 17.1 Reassessment triggers

An adopted component MUST be reassessed when a material change affects its approval basis.

Triggers include:

- Upstream source revision changes.
- Upstream license changes.
- New or changed license exceptions.
- Security advisories or vulnerabilities.
- Major technical changes.
- Interface changes.
- New dependencies.
- Changed technology dependencies.
- Changes to the intended use.
- Changes to the integration scope.
- Changes to public or commercial distribution.
- Discovery of inaccurate provenance or license information.
- Withdrawal of required rights or permissions.

### 17.2 Reassessment outcomes

| Outcome | Meaning |
|---|---|
| RETAIN | Existing approval remains valid. |
| UPDATE | Approval is retained subject to a revised source revision or updated conditions. |
| REVIEW | Adoption is temporarily under review pending further evidence or owner decision. |
| REVOKE | Existing adoption approval is withdrawn. |

A reassessment MUST preserve the original adoption record and decision history.

### 17.3 Maintenance requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-MNT-001 | Material changes to an adopted component MUST trigger reassessment. | R |
| ADP-MNT-002 | Reassessment MUST preserve the original approval and revision history. | R |
| ADP-MNT-003 | A revoked component MUST NOT be used for new approved integration. | R |
| ADP-MNT-004 | Changed license or distribution obligations MUST be reviewed before further release. | R |
| ADP-MNT-005 | Reassessment outcomes MUST be recorded in the intake record. | R |

## 18. Adoption Records and Evidence

### 18.1 Record set

The adoption record set MUST contain or reference the following, as applicable:

| Record | Purpose |
|---|---|
| Discovery record | Candidate origin and intended use. |
| Screening record | Initial suitability outcome. |
| Intake record | Stable identity and lifecycle reference. |
| Provenance record | Upstream source and immutable revision. |
| License assessment | License classification and obligations. |
| Technical assessment | Functional and implementation suitability. |
| Verification assessment | Verification methodology and results. |
| Security assessment | Security and maintenance risks. |
| Integration-readiness assessment | Compliance with the KRITVA IP Standard and applicable profile. |
| Adoption decision | ALLOW, REVIEW, or DENY with scope and rationale. |
| Waiver record | Approved deviations and conditions. |
| Integration record | Imported source and KRITVA modifications. |
| Release record | Distribution and notice compliance. |
| Reassessment record | Changes to approval status and conditions. |

### 18.2 Evidence integrity

Records MUST be maintained so that:

- The approved upstream revision can be identified.
- The basis for the adoption decision can be reconstructed.
- KRITVA modifications can be distinguished from upstream source.
- Assessment results can be linked to the relevant component revision.
- Waivers and exceptions can be traced to the requirements they affect.
- Release decisions can be linked to the applicable distribution scope.
- Historical decisions remain available after an update or revocation.

### 18.3 Record separation

Upstream and KRITVA records MUST remain separate in meaning and attribution.

Upstream project documentation MUST NOT be presented as KRITVA approval evidence.

KRITVA assessment and integration records MUST NOT be represented as statements or endorsements by the upstream project.

The repository-specific record location is not prescribed by this document. It MUST be selected so that required records remain accessible to authorized reviewers and maintainers.

### 18.4 Records requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-REC-001 | Every adopted component MUST have a complete or explicitly scoped adoption record set. | R |
| ADP-REC-002 | Assessment evidence MUST be linked to the relevant component revision. | R |
| ADP-REC-003 | Adoption decisions MUST remain traceable after source updates. | R |
| ADP-REC-004 | Upstream and KRITVA records MUST remain distinguishable. | R |
| ADP-REC-005 | Waivers and exceptions MUST be retained with the affected requirement and component reference. | R |
| ADP-REC-006 | Records MUST be maintained in an approved repository or record location. | R |
| ADP-REC-007 | Public records MUST comply with the public/private boundary defined by `OPEN_SOURCE_IP_POLICY.md`. | R |

## 19. Roles and Responsibilities

The following roles define the expected responsibilities in the adoption process.

| Role | Responsibilities |
|---|---|
| Proposer | Identifies the candidate, intended use, and initial rationale. |
| Intake owner | Creates and maintains the intake record. |
| Technical reviewer | Assesses functionality, implementation quality, and integration readiness. |
| Verification reviewer | Assesses verification methodology and evidence. |
| License reviewer | Assesses license, provenance, and redistribution obligations. |
| Security reviewer | Assesses vulnerabilities, supply-chain risks, and maintenance risks. |
| Repository maintainer | Ensures controlled integration and record consistency. |
| Release reviewer | Checks distribution scope and release compliance. |
| Owner / authorized approver | Records the adoption decision and approves applicable exceptions. |

Dinesh Annayya is the owner for the decisions and open items defined by this document.

Review responsibilities MAY be assigned to qualified reviewers. Delegation of review work does not automatically delegate adoption approval authority.

## 20. Enforcement and Assessment

### 20.1 Enforcement classes

This process uses the enforcement classes aligned with `KRITVA_IP_STANDARD.md` and `KNX-RTL-STD-001`.

| Class | Name | Meaning |
|---|---|---|
| A | Automated | The requirement can be checked by an automated script, tool, or CI process. |
| T | Tool-assisted | Tools can provide evidence, but human interpretation or review is required. |
| R | Review only | Human review, judgment, or explicit approval is required. |

The enforcement class describes the assessment method. It does not change the normative force of a requirement.

A mandatory requirement remains mandatory even when its enforcement is review-only or when an automated check has not yet been implemented.

### 20.2 Assessment results

Assessment results MUST use explicit states appropriate to the check:

- PASS
- FAIL
- WAIVED
- NOT APPLICABLE
- UNKNOWN

UNKNOWN MUST NOT be treated as PASS.

A failed mandatory requirement MUST prevent ALLOW unless a valid approved exception is applicable and the exception is legally and technically permissible.

### 20.3 Tool versions

Tool versions and configurations SHOULD be recorded for reproducibility.

**Tool versions for this document are UNVERIFIED.**

No specific tool version or toolchain configuration is approved by this document.

### 20.4 Assessment requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| ADP-ENF-001 | Every mandatory adoption requirement MUST have an identifiable assessment result. | R |
| ADP-ENF-002 | Enforcement classes MUST use A/T/R consistently with the KRITVA IP Standard. | R |
| ADP-ENF-003 | UNKNOWN MUST NOT be treated as PASS. | R |
| ADP-ENF-004 | Automated and tool-assisted results MUST retain sufficient evidence for review. | R |
| ADP-ENF-005 | Tool versions MUST be marked UNVERIFIED when they have not been independently established. | R |
| ADP-ENF-006 | An assessment result MUST NOT substitute for an explicit adoption decision. | R |

## 21. Waivers and Exceptions

A deviation from an applicable mandatory requirement MUST be handled through the waiver process defined by the KRITVA IP Standard and applicable SoC profile.

A waiver request MUST identify:

- Requirement ID.
- Component and source revision.
- Intended integration scope.
- Description of the deviation.
- Technical rationale.
- License or legal implications, where relevant.
- Risk assessment.
- Compensating controls.
- Expiry or reassessment condition.
- Authorized approver.

A waiver MUST NOT:

- Override applicable law.
- Override third-party license or contractual obligations.
- Authorize use of unapproved technology dependencies.
- Be silently applied to another component or source revision.
- Be treated as a permanent change to the common standard.

## 22. Public and Private Information Boundary

This document is a public process baseline.

Public adoption records MAY contain:

- Public upstream source locations.
- Public immutable revision identifiers.
- Public license identifiers and notices.
- Public technical assessment summaries.
- Public adoption decisions cleared for disclosure.
- Public verification evidence suitable for release.

Private or restricted records MUST remain protected, including:

- Confidential vendor collateral.
- Proprietary source code.
- Non-public license agreements.
- Private supplier correspondence.
- Credentials and access tokens.
- Unreleased SoC architecture and implementation details.
- Security-sensitive information not cleared for disclosure.
- Internal review material not approved for publication.

A public record MAY refer to private evidence through a non-sensitive identifier, without publishing the evidence itself.

This document does not define or disclose unreleased Nexus or Edge implementation details.

## 23. Document Maintenance

This document is maintained as a KRITVA public process standard.

Changes MUST be reviewed for impact on:

- Discovery and screening.
- Intake record requirements.
- Provenance and licensing.
- Technical and security assessment.
- Verification methodology and evidence.
- Integration-readiness criteria.
- Adoption decision gates.
- Records and release controls.
- Related KRITVA standards and policies.

Changes MUST NOT silently invalidate or rewrite historical adoption decisions.

### 23.1 Versioning

| Version change | Meaning |
|---|---|
| Major | Incompatible changes to the adoption lifecycle or mandatory decision gates. |
| Minor | New requirements, stages, or substantive additions that preserve the existing process framework. |
| Patch | Editorial corrections, clarifications, and non-substantive changes. |

### 23.2 Approval status

The current document status is DRAFT.

Publication of this document does not constitute approval of any candidate IP or adoption decision.

---

## 24. Open Items

The following items require explicit owner decisions. They are not approved assumptions.

Owner for all items: **Dinesh Annayya**.

| ID | Open item | Decision required | Owner | Status |
|---|---|---|---|---|
| ADP-OI-001 | Intake record schema | Approve a canonical machine-readable intake record schema and required fields. | Dinesh Annayya | OPEN |
| ADP-OI-002 | Component ID format | Approve the stable component identifier format and allocation authority. | Dinesh Annayya | OPEN |
| ADP-OI-003 | Intake record location | Decide whether intake records are maintained per repository, centrally, or through a shared registry. | Dinesh Annayya | OPEN |
| ADP-OI-004 | Review delegation | Define which review activities and approval actions may be delegated. | Dinesh Annayya | OPEN |
| ADP-OI-005 | ALLOW scope categories | Confirm the standard approval-scope categories and whether additional categories are required. | Dinesh Annayya | OPEN |
| ADP-OI-006 | Reassessment cadence | Define a periodic review cadence for adopted components. | Dinesh Annayya | OPEN |
| ADP-OI-007 | Assessment evidence retention | Define minimum retention periods and archival requirements for adoption evidence. | Dinesh Annayya | OPEN |
| ADP-OI-008 | Toolchain baseline | Establish verified tool versions and configurations for the adoption and verification process. Current tool versions remain UNVERIFIED. | Dinesh Annayya | OPEN |
| ADP-OI-009 | KVRF evidence schema versioning | Define the versioning and compatibility policy for KVRF-schema evidence records. | Dinesh Annayya | OPEN |
| ADP-OI-010 | Integration-readiness automation | Decide which integration-readiness checks should be automated and which remain tool-assisted or review-only. | Dinesh Annayya | OPEN |
| ADP-OI-011 | License review authority | Define the required reviewer or external legal authority for license classes requiring legal interpretation. | Dinesh Annayya | OPEN |
| ADP-OI-012 | Public adoption summaries | Define the approval process for publishing adoption summaries that refer to private assessment evidence. | Dinesh Annayya | OPEN |
| ADP-OI-013 | Verification levels | Confirm the common definition and acceptance criteria for IP verification levels, including L2 and above. | Dinesh Annayya | OPEN |
| ADP-OI-014 | APB revision and profile | Approve the APB revision and control/register interface profile for the common IP baseline. | Dinesh Annayya | OPEN |

## 25. References

1. `KRITVA_IP_STANDARD.md` — Common IP design and integration requirements.
2. `OPEN_SOURCE_IP_POLICY.md` — Third-party source, license, provenance, adoption, and redistribution policy.
3. `KNX-RTL-STD-001` — Nexus SoC RTL design profile.
4. Applicable KRITVA IP repository contribution and release procedures.
5. Applicable upstream license texts, notices, and provenance records.
6. Applicable KVRF verification methodology and evidence schema.

The references do not imply approval of any specific implementation, upstream component, tool version, or vendor.

---

## 26. Change History

| Version | Date | Status | Description |
|---|---|---|---|
| 0.1.0 | 2026-11-12 | DRAFT | Initial adoption process covering discovery, screening, intake, provenance, licensing, technical and security assessment, integration readiness, decision gates, controlled integration, verification, and records. |

---

**End of Document**