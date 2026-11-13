
# KRITVA IP LIFECYCLE POLICY

| Field | Value |
|---|---|
| Document ID | KIP-POL-LCP-001 |
| Title | KRITVA IP Lifecycle Policy |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | PUBLIC |
| Owner | Dinesh Annayya |
| Copyright Holder | Kritva Robotics |
| Effective Date | TBD |
| Review Cycle | Annual, or upon a material policy change |
| Supersedes | New document |
| Normative Language | RFC 2119 |
| Related Standard | KRITVA IP Standard |
| Related Policies | Open Source IP Policy; IP Adoption Process; IP Customization Policy; IP Upstream Maintenance Policy |

Copyright (c) Kritva Robotics. All rights reserved, subject to the applicable repository licence and any third-party notices retained in the relevant files.

---

## 1. Purpose

This policy defines the lifecycle governance requirements for intellectual property (IP) adopted, developed, maintained, integrated, and eventually retired within the KRITVA ecosystem.

It establishes:

- A common set of lifecycle states for IP.
- Promotion criteria across assurance levels L0 through L3.
- Permitted lifecycle transitions and their approval requirements.
- Required records and evidence for lifecycle decisions.
- Controls for deprecation, replacement, and retirement.
- Traceability between IP lifecycle status, verification evidence, adoption decisions, and programme or product integration.

The policy is intended to provide consistent lifecycle management across KRITVA-developed IP and third-party or open-source IP.

It does not prescribe a particular RTL implementation, verification framework, synthesis tool, physical-design flow, or SoC architecture.

## 2. Scope

### 2.1 In scope

This policy applies to:

1. RTL IP blocks developed by Kritva Robotics.
2. Third-party RTL IP adopted for KRITVA use.
3. Open-source hardware IP adopted or evaluated for KRITVA use.
4. Configurable, parameterized, customized, or forked IP.
5. Verification collateral and supporting implementation artifacts that form part of an IP deliverable.
6. IP interfaces, wrappers, adapters, integration collateral, and associated evidence where these affect the IP lifecycle decision.

Examples of IP categories include:

- Processor and compute IP.
- Bus and interconnect IP.
- Memory controllers and memory-interface IP.
- Control and peripheral IP.
- Clock, reset, and power-management IP.
- Security and system-management IP.
- Verification and infrastructure IP where formally managed as an IP deliverable.

### 2.2 Out of scope

This policy does not define:

- The complete SoC architecture or product roadmap.
- SoC-specific integration profiles.
- Foundry-specific implementation requirements.
- Detailed RTL coding rules.
- Detailed CDC/RDC methodology.
- Detailed functional verification methodology.
- Third-party licence interpretation or legal advice.
- Programme-level milestone ownership, dependency management, or consolidated programme status.

These subjects are governed by their respective standards, policies, repository requirements, or programme processes.

### 2.3 Relationship to other KRITVA documents

| Document | Relationship |
|---|---|
| KRITVA IP Standard | Defines common normative requirements for IP design and delivery. |
| Open Source IP Policy | Defines licensing, provenance, and open-source adoption requirements. |
| IP Adoption Process | Defines the evaluation and adoption workflow for candidate IP. |
| IP Customization Policy | Defines controls for wrappers, patches, forks, and other modifications. |
| IP Upstream Maintenance Policy | Defines upstream monitoring, update, and maintenance controls. |
| SoC integration documentation | Defines product- or SoC-specific integration requirements. |
| Kritva programme governance | Owns programme-level plans, milestones, dependencies, approvals, and consolidated status. |

An IP repository MUST NOT create a competing programme-level milestone or approval system. It MAY maintain IP-specific lifecycle records and evidence, provided they remain traceable to the governing programme records where applicable.

## 3. Normative language

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **RECOMMENDED**, **MAY**, and **OPTIONAL** are to be interpreted as normative requirement terms.

Common KRITVA IP standards use RFC 2119 terminology. In this policy, MUST is the preferred normative keyword.

Where an applicable approved profile uses SHALL, SHALL has the same normative force as MUST.

The normative force of a requirement is independent of its enforcement class.

### 3.1 Requirement identifiers

Requirements in common KRITVA IP standards MUST use the following identifier scheme:

`KIP-STD-<AREA>-NNN`

Where:

- `KIP-STD` identifies a common KRITVA IP standard requirement.
- `<AREA>` identifies the subject area.
- `NNN` is a unique numeric sequence within that area.

This policy uses document-local identifiers for its own policy requirements and open items. Such identifiers do not replace or reserve common standard requirement IDs.

Existing requirement IDs MUST NOT be renumbered solely to accommodate a new requirement.

Where a requirement is promoted from an implementation-specific profile into a common standard, the common standard MUST assign a new KIP requirement ID and retain a `derived-from` reference to the originating profile requirement.

## 4. Lifecycle principles

All IP managed under this policy MUST follow these principles.

### 4.1 Explicit lifecycle state

Every managed IP item MUST have exactly one current lifecycle state.

A lifecycle state MUST be supported by a recorded decision or an explicitly identified initial registration condition.

A repository MUST NOT imply lifecycle status solely from:

- The existence of RTL files.
- A successful simulation.
- A merged pull request.
- A release tag.
- A directory name.
- A milestone label.
- An informal statement that the IP is ready.

### 4.2 Evidence-based decisions

Lifecycle transitions MUST be supported by evidence appropriate to the target state and assurance level.

A claim of completion without corresponding evidence MUST NOT be treated as an accepted lifecycle result.

### 4.3 Separation of lifecycle state and assurance level

Lifecycle state and assurance level are independent dimensions.

Lifecycle state describes the IP's governance and maintenance position.

Assurance level describes the maturity and strength of the available engineering evidence.

For example:

- An IP item MAY be `active` at L1.
- An IP item MAY be `deprecated` while retaining L3 evidence.
- An IP item MAY be `replaced` by another IP that has a lower assurance level, provided the replacement decision explicitly records the resulting risk and limitations.
- An IP item MUST NOT be considered L3 merely because it is active or released.

### 4.4 Provenance and reproducibility

The lifecycle record MUST identify the relevant source revision, upstream origin where applicable, and evidence revision.

Evidence MUST be traceable to the source and configuration that produced it.

Where a source change materially affects previously accepted evidence, the affected evidence MUST be reassessed.

### 4.5 Controlled change

A change to an IP's source, configuration, interface, licence, verification environment, or supported use MAY affect its lifecycle state or assurance level.

The IP owner MUST evaluate material changes and record whether re-verification, re-approval, reassessment, or a lifecycle transition is required.

### 4.6 No silent promotion or waiver

An IP MUST NOT be promoted to a higher assurance level or lifecycle state solely through an undocumented assumption.

A waiver MUST be explicit, justified, scoped, approved, and recorded according to the applicable policy.

A waiver does not automatically establish that an assurance criterion has been satisfied.

## 5. Lifecycle model

### 5.1 Lifecycle states

KRITVA defines the following lifecycle states:

1. `proposed`
2. `adopted`
3. `active`
4. `deprecated`
5. `replaced`
6. `retired`

The state names MUST be represented consistently in machine-readable lifecycle records.

Implementations MAY display more descriptive labels in reports or dashboards, but the canonical state values MUST remain stable.

### 5.2 State definitions

#### 5.2.1 PROPOSED

`proposed` identifies an IP candidate that has been registered for evaluation, development, or possible adoption.

An IP in this state:

- Has an identifiable owner or responsible reviewer.
- Has an initial purpose and intended use.
- Has an identified origin or development classification.
- Has not yet received formal adoption approval.
- MUST NOT be represented as approved for production use.

A proposed IP MAY be evaluated, simulated, inspected, or prototyped.

The proposed state does not imply that the IP has passed any minimum assurance level.

#### 5.2.2 ADOPTED

`adopted` identifies an IP that has passed the applicable adoption decision and is authorized for controlled KRITVA use within its approved scope.

An adopted IP:

- Has a recorded adoption decision.
- Has an identified source revision or development baseline.
- Has a documented intended use and scope.
- Has completed applicable provenance and licence checks.
- Has documented known limitations and open risks.
- Has an assigned lifecycle owner.
- Has a defined verification and evidence plan appropriate to its intended use.

Adopted does not mean production-ready.

An adopted IP MAY remain at L0 or L1 while its verification, integration, or assurance work proceeds.

The adoption decision MUST state whether the IP is approved for evaluation only, controlled development, or a more specific integration scope.

#### 5.2.3 ACTIVE

`active` identifies an IP that is currently maintained and approved for use within its recorded scope.

An active IP:

- Has an accountable owner.
- Has a controlled source baseline.
- Has current lifecycle and provenance records.
- Has verification evidence appropriate to its declared assurance level.
- Has known limitations and unresolved issues documented.
- Has a defined maintenance and change-control approach.
- Has no unresolved lifecycle restriction that prohibits its declared use.

The active state MUST NOT be interpreted as unrestricted approval for every KRITVA product or SoC.

The approved use scope MUST be stated explicitly.

An active IP MAY be under development, maintenance, or controlled integration.

#### 5.2.4 DEPRECATED

`deprecated` identifies an IP that remains identifiable and may remain available for existing users, but is no longer recommended for new adoption or new integration.

An IP MAY be deprecated when:

- A replacement is planned or available.
- An interface or architecture is no longer recommended.
- Maintenance is being phased out.
- A security, quality, licensing, or support concern makes continued new use undesirable.
- The IP no longer aligns with an approved KRITVA standard or product direction.
- Its supported use scope is being reduced.

A deprecation decision MUST record:

- The reason for deprecation.
- The effective date.
- The affected use cases and consumers.
- Whether existing integrations may continue.
- Whether new integrations are prohibited.
- The recommended migration or replacement path, if known.
- The expected maintenance and support position.
- Any planned review or end-of-support date.

Deprecated IP MUST NOT be newly adopted without an explicit exception approved by the designated authority.

Deprecation does not itself remove existing source code, releases, or evidence.

#### 5.2.5 REPLACED

`replaced` identifies an IP whose approved role has been superseded by another identified IP.

A replaced IP:

- Has an explicit replacement relationship.
- Has a recorded replacement decision.
- Has an identified replacement IP, if one exists.
- Has a documented migration or compatibility position.
- Is no longer the preferred IP for the superseded scope.

The replacement relationship MUST identify both the replaced IP and the replacement IP.

A replaced IP MAY remain available for historical reproducibility, maintenance of existing deployments, or migration support.

A replaced IP MUST NOT be presented as the current preferred solution for the scope covered by its replacement decision.

A replacement decision MUST NOT imply that the replacement IP has equivalent assurance, functionality, or compatibility unless evidence supports that claim.

If the replacement IP is not yet adopted or active, the decision MUST explicitly record that the replacement is planned or conditional.

#### 5.2.6 RETIRED

`retired` identifies an IP that is no longer maintained or approved for new or continuing KRITVA use, except where a specific archival or legal retention requirement applies.

An IP MAY be retired when:

- It has no remaining approved use.
- Its replacement or migration is complete.
- It is obsolete or unsupported.
- It presents an unacceptable unresolved risk.
- Its licence or provenance status prevents continued use.
- The owner has approved discontinuation.

A retirement decision MUST record:

- The reason for retirement.
- The effective date.
- The final known source revision.
- The final evidence references.
- Known consumers or integrations affected.
- Whether migration is complete, incomplete, or not applicable.
- The retention location for source and evidence.
- Any applicable licence, security, or legal retention requirements.

Retired IP MUST NOT be used for new integration.

Continued use of retired IP in an existing deployment requires an explicit, scoped exception and risk acceptance by the designated authority.

Retirement MUST NOT silently delete historical evidence or erase provenance.

### 5.3 State summary

| State | Meaning | New adoption | Existing use | Maintenance expectation |
|---|---|---|---|---|
| proposed | Candidate under evaluation | Evaluation only | Evaluation only | As defined by evaluation owner |
| adopted | Approved for controlled use | Within approved scope | Within approved scope | Defined in adoption record |
| active | Maintained and approved within scope | Allowed within scope | Allowed within scope | Maintained |
| deprecated | No longer recommended for new use | Exception required | May continue under recorded conditions | Phased or restricted |
| replaced | Superseded by another IP for a defined scope | Not preferred | May continue during migration or under exception | Migration or legacy support |
| retired | Discontinued | Prohibited | Prohibited except approved exception | No routine maintenance |

## 6. Assurance levels

### 6.1 Overview

KRITVA defines four assurance levels:

- L0 — Registered / Initial assessment
- L1 — Evaluated / Basic evidence
- L2 — Verified / Controlled engineering evidence
- L3 — Qualified / Release-oriented evidence

Assurance levels are cumulative in intent. A higher level requires the applicable lower-level evidence and additional criteria.

The assurance level MUST be declared in the lifecycle record.

An assurance level MUST NOT be inferred from a release name, source repository, project phase, or lifecycle state.

### 6.2 L0 — Registered / Initial assessment

L0 establishes that an IP item has been identified and registered with sufficient information to support evaluation.

Minimum criteria:

1. A unique IP identifier is assigned.
2. An owner is identified.
3. The IP category and intended function are described.
4. The origin is identified as KRITVA-developed, third-party, open-source, or another documented category.
5. The source location or planned development location is recorded.
6. The intended use and initial integration context are described.
7. Known major dependencies and constraints are recorded where known.
8. Initial provenance and licence information is captured where applicable.
9. Initial risks and unknowns are recorded.
10. A preliminary evaluation or development plan is identified.

L0 evidence MAY consist of:

- An IP registration record.
- A source repository reference.
- An upstream project reference.
- An initial specification or datasheet.
- An initial risk and dependency assessment.
- A preliminary interface description.

L0 does not establish technical correctness, functional completeness, verification coverage, or suitability for integration.

### 6.3 L1 — Evaluated / Basic evidence

L1 establishes that an IP candidate has undergone an initial technical and adoption assessment.

Minimum criteria:

1. L0 criteria are satisfied.
2. The intended functionality and major interfaces are documented.
3. The source revision or development baseline is identified.
4. The applicable IP requirements are identified.
5. Initial RTL or implementation review has been performed where applicable.
6. Basic functional evaluation has been performed or a justified non-applicability statement has been recorded.
7. Known limitations and unresolved issues are documented.
8. Initial synthesis, lint, or structural analysis has been performed where applicable, or explicitly identified as pending.
9. Provenance and licence assessment is recorded for third-party or open-source IP.
10. An adoption recommendation or development continuation decision is recorded.

L1 evidence MAY include:

- Basic simulation results.
- Initial directed tests.
- Interface checks.
- Lint reports.
- Preliminary synthesis reports.
- Source review records.
- Upstream maintenance assessment.
- Licence and provenance records.
- An adoption evaluation report.

L1 does not establish comprehensive verification, integration readiness, or release qualification.

### 6.4 L2 — Verified / Controlled engineering evidence

L2 establishes that an IP has completed a defined engineering verification process against its approved requirements and configuration.

Minimum criteria:

1. L0 and L1 criteria are satisfied.
2. The IP requirement baseline is approved or otherwise formally controlled.
3. Requirement-to-test or requirement-to-evidence traceability is available.
4. Verification plans and acceptance criteria are documented.
5. Functional verification has been executed against the identified source and configuration.
6. Test results and relevant logs are retained.
7. Verification failures and unresolved defects are recorded and dispositioned.
8. Applicable lint, elaboration, synthesis, and structural checks have been completed.
9. Interface, reset, clock, and configuration assumptions are documented.
10. Relevant integration or interoperability checks have been completed or explicitly scoped out.
11. The evidence set is reproducible to the extent required by the IP's verification environment.
12. A technical review has assessed the evidence and open risks.
13. The lifecycle owner has recorded the L2 assessment decision.

The default reference verification flow for new KRITVA-developed IP at L2 and above is KVRF with cocotb.

Equivalent verification flows MAY be used if they produce evidence records conforming to the applicable KVRF evidence schema.

Examples include a simulator-based or hardware-assisted flow that emits the required evidence records.

Third-party or upstream IP MAY retain its native testbench and verification framework. A wrapper-level KVRF test or equivalent evidence-producing integration test SHOULD be used where appropriate to establish KRITVA integration behavior.

L2 is an engineering verification level. It does not automatically establish product qualification, silicon validation, safety certification, or production release approval.

### 6.5 L3 — Qualified / Release-oriented evidence

L3 establishes that an IP has completed the additional qualification and release-readiness activities required for its declared intended use.

Minimum criteria:

1. L0, L1, and L2 criteria are satisfied.
2. The release source baseline is immutable and identifiable.
3. The supported configuration and parameter set are documented.
4. Verification evidence is complete for the approved release scope.
5. Relevant regression results are available and accepted.
6. Relevant integration testing has been completed.
7. Applicable CDC/RDC, reset, clock, and timing checks have been completed or explicitly dispositioned.
8. Synthesis and implementation evidence is available where applicable.
9. Known defects and limitations have documented dispositions.
10. Security and licence reviews have been completed where applicable.
11. Upstream source and customization status are recorded where applicable.
12. Release packaging, documentation, and reproducibility requirements are satisfied.
13. The release review has evaluated residual risks.
14. Required technical and release approvals are recorded.

L3 evidence MAY include:

- Full regression reports.
- Coverage reports and coverage closure rationale.
- Integration test results.
- CDC/RDC analysis.
- Timing and synthesis reports.
- Formal verification results, where applicable.
- Security review records.
- Release manifests.
- Reproducibility records.
- Approved waivers and residual-risk decisions.
- Release approval records.

The L3 level MUST be interpreted against a declared scope.

For example, an IP may be qualified for a specific configuration, interface, technology-independent RTL baseline, or integration environment without being qualified for every possible use.

L3 does not imply silicon validation unless silicon validation evidence is explicitly included in the qualification scope.

### 6.6 Assurance criteria applicability

Not every assurance criterion applies identically to every IP category.

Where a criterion is not applicable, the lifecycle record MUST contain:

- The criterion or activity being marked not applicable.
- A technical rationale.
- The affected IP scope.
- The reviewer or approver.
- Any residual risk or limitation.

A missing result MUST NOT be represented as not applicable.

An unknown result MUST NOT be treated as a pass.

A criterion that is pending MUST remain visibly pending until evidence or an approved disposition is available.

### 6.7 Assurance promotion

Promotion between assurance levels MUST be based on evidence and review.

The normal promotion sequence is:

`L0 -> L1 -> L2 -> L3`

An IP MAY be assessed directly against a higher level if the evidence package demonstrates that all applicable lower-level and target-level criteria are satisfied.

Such a direct assessment MUST NOT waive lower-level criteria implicitly.

The assessment record MUST identify the criteria reviewed, evidence accepted, criteria not applicable, unresolved gaps, and approval decision.

### 6.8 Assurance regression

An IP's declared assurance level MUST be reassessed when a material change invalidates previously accepted evidence.

Examples include:

- RTL changes affecting functional behavior.
- Interface changes.
- Parameter changes outside the previously verified configuration.
- Changes to reset or clock assumptions.
- Changes to dependencies or wrappers.
- Changes to verification environment or test semantics.
- Changes to synthesis or implementation constraints that affect the qualification scope.
- Discovery of a defect that invalidates a prior acceptance result.
- A change in upstream source that materially affects the adopted IP.

The owner MUST determine which evidence is invalidated and whether a lower assurance level should be declared temporarily.

The previous assessment MUST remain in the historical record.

## 7. Lifecycle state transitions

### 7.1 Transition model

The normal lifecycle progression is:

`proposed -> adopted -> active -> deprecated -> replaced -> retired`

This is a conceptual progression, not a requirement that every IP must pass through every state.

Permitted transitions depend on the IP's actual use and governance needs.

### 7.2 Transition matrix

| Current state | Target state | Permitted | Conditions |
|---|---|---|---|
| proposed | adopted | Yes | Adoption review and approval completed |
| proposed | retired | Yes | Candidate rejected or evaluation discontinued |
| adopted | active | Yes | Active-use entry criteria satisfied |
| adopted | deprecated | Yes | Adoption withdrawn or scope no longer recommended |
| adopted | retired | Yes | Controlled-use approval withdrawn and no continuing use |
| active | deprecated | Yes | Deprecation decision approved |
| active | replaced | Yes | Replacement decision approved and relationship recorded |
| active | retired | Yes, restricted | Retirement decision and consumer impact assessment completed |
| deprecated | active | Yes, restricted | Reinstatement review and approval completed |
| deprecated | replaced | Yes | Replacement decision approved |
| deprecated | retired | Yes | Retirement criteria satisfied |
| replaced | deprecated | Yes, restricted | Legacy support continues but replacement relationship remains |
| replaced | retired | Yes | Retirement criteria satisfied |
| retired | any non-retired state | No, by default | Reinstatement requires a new lifecycle record or explicit exceptional decision |

A lifecycle owner MUST NOT create an unlisted transition by silently changing the state field.

An exceptional transition MUST be documented with its rationale, impact, approval, and traceability.

### 7.3 Proposed to adopted

The transition from `proposed` to `adopted` MUST require:

1. A completed adoption evaluation appropriate to the intended scope.
2. Identified source revision or development baseline.
3. Provenance and licence review where applicable.
4. Initial technical evaluation.
5. Documented limitations and known risks.
6. An adoption recommendation.
7. An approval decision by the designated adoption authority.

The adoption record MUST state whether use is limited to evaluation, development, or a named integration scope.

### 7.4 Adopted to active

The transition from `adopted` to `active` MUST require:

1. A controlled source baseline.
2. An assigned lifecycle owner.
3. A declared assurance level.
4. Evidence appropriate to the approved active-use scope.
5. A documented maintenance approach.
6. A defined issue and change-management approach.
7. A review of open defects and residual risks.
8. Approval by the designated technical authority.

The transition MUST NOT be used to bypass required L2 or L3 criteria when the intended use requires those levels.

The approval record MUST identify the permitted use scope and any restrictions.

### 7.5 Active to deprecated

The transition from `active` to `deprecated` MUST require:

1. A documented reason.
2. An impact assessment covering known consumers.
3. A statement of whether new adoption is prohibited.
4. A statement of whether existing use may continue.
5. A migration or replacement recommendation, if available.
6. A maintenance and support position.
7. An effective date.
8. Approval by the designated lifecycle authority.

Deprecation SHOULD provide a reasonable migration period where existing users or integrations are affected.

The migration period MUST be recorded when applicable.

### 7.6 Active or deprecated to replaced

The transition to `replaced` MUST require:

1. An identified replacement IP or a documented replacement programme.
2. A comparison of relevant functionality and interfaces.
3. An assessment of compatibility and migration impact.
4. A review of assurance differences between the old and replacement IP.
5. A documented consumer migration plan or exception process.
6. An explicit replacement relationship in the lifecycle records.
7. Approval by the designated lifecycle authority.

The replacement decision MUST distinguish:

- Replacement selected but not yet adopted.
- Replacement adopted but not yet active.
- Replacement active for the intended scope.
- Replacement qualified for the intended scope.

These conditions MUST NOT be conflated.

### 7.7 Transition to retired

A transition to `retired` MUST require:

1. A documented retirement rationale.
2. A consumer and integration impact assessment.
3. A disposition for known dependencies.
4. A record of migration status.
5. A final source revision or archive reference.
6. Retention of applicable evidence and provenance records.
7. A statement of residual risks or known limitations.
8. Approval by the designated lifecycle authority.

If an IP has active consumers, retirement MUST include a documented decision on how those consumers are handled.

An IP MUST NOT be marked retired merely because active development has stopped.

### 7.8 Reinstatement

Reinstatement of a retired IP is exceptional.

A retired IP MUST NOT be moved back to active by changing its state without a new review.

The owner MUST:

1. Create or reopen a controlled lifecycle review record.
2. Confirm source provenance and integrity.
3. Reassess current requirements and supported use.
4. Reassess dependencies and compatibility.
5. Reassess verification evidence and invalidated results.
6. Establish the assurance level applicable to the proposed use.
7. Obtain explicit approval.

The record MUST preserve the previous retirement decision and explain why reinstatement is justified.

Where the source has materially changed or the historical baseline cannot be reproduced, a new IP registration SHOULD be considered.

## 8. Lifecycle approval governance

### 8.1 Approval principles

Lifecycle approvals MUST be explicit, attributable, and traceable.

The person performing implementation or verification MUST NOT be assumed to have approval authority solely because they completed the work.

The lifecycle record MUST distinguish:

- Owner.
- Implementer, where applicable.
- Verification contributor, where applicable.
- Reviewer.
- Approver.
- Release authority, where applicable.

One person MAY perform multiple roles where organizational governance permits, but the record MUST make those roles explicit.

### 8.2 Approval authority

The following authority model is the default policy model. The actual authorized roles and delegation rules MUST be confirmed and recorded by KRITVA governance.

| Decision | Required approval authority |
|---|---|
| Initial IP registration | IP owner or delegated registry maintainer |
| Proposed to adopted | Designated IP adoption authority |
| Assurance promotion L0 to L1 | Technical reviewer or delegated authority |
| Assurance promotion L1 to L2 | Verification/technical reviewer and designated approver |
| Assurance promotion L2 to L3 | Technical qualification reviewer and release authority |
| Adopted to active | Designated technical authority |
| Active to deprecated | Lifecycle authority |
| Active or deprecated to replaced | Lifecycle authority |
| Transition to retired | Lifecycle authority |
| Reinstatement from retired | Lifecycle authority and technical authority |
| Exception to lifecycle requirements | Authorized exception approver |

The designated authority for each role MUST be identifiable.

Until the authority model is formally approved, the approval authority for an affected decision MUST be explicitly recorded rather than inferred.

### 8.3 Approval record

Every lifecycle transition approval MUST record:

- Decision identifier.
- IP identifier.
- Previous state.
- Target state.
- Previous assurance level.
- Target assurance level, if changed.
- Source revision.
- Decision date.
- Decision owner.
- Reviewer.
- Approver.
- Evidence references.
- Conditions and restrictions.
- Open issues and accepted risks.
- Approval status.
- Approval rationale.

Approval status MUST use a controlled value, such as:

- `PROPOSED`
- `UNDER_REVIEW`
- `APPROVED`
- `REJECTED`
- `SUPERSEDED`
- `WITHDRAWN`

Only `APPROVED` decisions authorize the corresponding transition.

### 8.4 Approval integrity

Approval records SHOULD be append-only.

Where a decision is corrected, superseded, or withdrawn, the correction MUST preserve the historical record and reference the affected decision.

A mutable status summary MAY be generated from the decision history, but MUST NOT replace the authoritative decision record.

Where the programme uses a commit-bound approval ledger, lifecycle decisions that fall within its scope MUST reference the corresponding programme approval record rather than creating a conflicting approval mechanism.

### 8.5 Interim sole-owner operating mode (proposed)

Status: PROPOSED 2026-11-13. This section takes effect only when the Owner
approves it (LCP-OI-021). Until then, section 8.2 applies and approval
authority MUST be explicitly recorded.

While the Owner is the only designated reviewer and approver, the following
interim rules apply:

1. The Owner MAY hold the owner, reviewer, approver and release-authority
   roles for the same decision.
2. The record MUST name each role explicitly and set `approval_basis` to
   `SOLE_OWNER_INTERIM`. A decision approved on this basis MUST NOT be
   described as independently reviewed.
3. Self-approval MUST NOT be implicit. The approval rationale MUST be recorded
   and the evidence references MUST be present before the status becomes
   `APPROVED`.
4. For promotion to L3, for exceptions or waivers that deviate from a MUST
   requirement, and for any decision rated high risk, the Owner MUST record
   that independent review was unavailable, and SHOULD obtain independent human
   review where a qualified reviewer is reasonably available.
5. Reviews performed with automated or AI-assisted tools MAY be recorded as
   review inputs (tool, date, scope and findings). They are not reviewer or
   approver roles and do not constitute independent review.
6. The interim mode ends when a second qualified reviewer or approver is
   designated and recorded. Decisions approved under `SOLE_OWNER_INTERIM` that
   are at L3, or that are active with an unexpired exception, SHOULD then be
   re-reviewed by the independent reviewer within a period defined by the
   Owner (LCP-OI-021).
7. Interim approvals remain valid records. They are marked, not rewritten.

## 9. Lifecycle evidence and KVRF records

### 9.1 Evidence principles

Evidence MUST be linked to:

- The IP identifier.
- The source revision.
- The relevant configuration.
- The verification or analysis environment.
- The applicable requirement or acceptance criterion.
- The execution result.
- The evidence artifact or immutable reference.

Evidence MUST be sufficient to support the lifecycle or assurance decision being made.

### 9.2 KVRF-schema evidence

KVRF-schema evidence is the default evidence interchange format for new KRITVA-developed IP at L2 and above.

The lifecycle policy is outcome/evidence based. It does not mandate that all IP use one simulator, testbench, or verification implementation.

An equivalent verification flow MAY be accepted if it produces evidence records conforming to the applicable KVRF evidence schema.

The evidence record SHOULD identify:

- IP identifier.
- Source revision.
- Configuration identifier.
- Test or suite identifier.
- Test result.
- Execution timestamp.
- Tool and tool version.
- Environment identifier.
- Log and report references.
- Relevant requirement or acceptance criterion.
- Evidence producer.
- Evidence integrity information where available.

The exact schema version and mandatory fields are governed by the applicable KVRF specification.

### 9.3 Evidence outcomes

Evidence outcomes MUST distinguish at least:

- `PASS`
- `FAIL`
- `BLOCKED`
- `NOT_RUN`
- `NOT_APPLICABLE`
- `INCONCLUSIVE`

A result MUST NOT be marked `PASS` when the test or analysis did not execute successfully.

A result MUST NOT be marked `NOT_APPLICABLE` merely because evidence is unavailable.

An `INCONCLUSIVE` result MUST NOT be treated as a pass.

A lifecycle decision MAY accept a documented limitation or exception, but MUST NOT rewrite a failed or missing result as a pass.

### 9.4 Evidence acceptance

Evidence acceptance MUST consider:

1. Whether the evidence refers to the correct source revision.
2. Whether the configuration is within the declared scope.
3. Whether the test or analysis is relevant to the requirement.
4. Whether the execution completed successfully.
5. Whether the result is interpretable.
6. Whether required logs and artifacts are available.
7. Whether failures have been dispositioned.
8. Whether the evidence has been reviewed by an authorized reviewer.

Evidence acceptance MUST be recorded separately from evidence generation.

A passing CI job alone MUST NOT establish lifecycle approval unless the applicable acceptance and review rules are also satisfied.

### 9.5 Evidence invalidation

Evidence MUST be reassessed when its source, configuration, tool environment, or test semantics change in a way that could affect the result.

The owner MUST record whether evidence is:

- `VALID`
- `REQUIRES_REVIEW`
- `INVALIDATED`
- `SUPERSEDED`

Evidence MUST NOT be deleted merely because it is invalidated.

Historical evidence MUST remain identifiable for audit and reproducibility.

### 9.6 Tool versions

Tool versions used for lifecycle evidence MUST be recorded when available.

Tool versions that have not been verified MUST be marked `UNVERIFIED`.

A tool version MUST NOT be invented or inferred from a tool name, operating system, CI image label, or approximate release date.

Where a tool version is unknown, the evidence record MUST make that limitation visible.

The applicable verification plan MAY define tool-version pinning requirements for a particular assurance level or release scope.

## 10. Lifecycle records

### 10.1 Required records

Each managed IP MUST have a lifecycle record containing at least:

1. IP identity.
2. IP name and description.
3. IP category.
4. Origin and provenance.
5. Current lifecycle state.
6. Current assurance level.
7. Source repository and revision.
8. Owner.
9. Intended use and approved scope.
10. Dependencies.
11. Applicable requirements and standards.
12. Verification and evidence references.
13. Known issues and risks.
14. Current maintenance position.
15. Lifecycle decision history.
16. Replacement or dependency relationships, where applicable.

The record MAY be maintained as YAML, JSON, or another controlled machine-readable format.

The canonical format MUST be declared by the owning repository or governing registry.

### 10.2 Suggested lifecycle record schema

The following example is illustrative. It does not establish a mandatory repository path or finalized machine-readable schema.

~~~yaml
schema_version: "0.1.0"

ip:
  id: "KIP-IP-EXAMPLE-001"
  name: "Example IP"
  category: "peripheral"
  description: "Illustrative IP lifecycle record"

  origin:
    type: "kritva_developed"
    upstream_project: null
    upstream_revision: null
    licence: "TBD"

  source:
    repository: "TBD"
    revision: "TBD"
    release_tag: null

  lifecycle:
    state: "proposed"
    assurance_level: "L0"
    effective_date: null
    decision_id: null

  ownership:
    owner: "Dinesh Annayya"
    technical_reviewer: "TBD"
    approver: "TBD"

  intended_use:
    scope: "TBD"
    permitted_use: "evaluation_only"
    restrictions: []

  requirements:
    standard_references: []
    requirement_ids: []

  verification:
    framework: "TBD"
    evidence_format: "KVRF-schema"
    evidence_schema_version: "TBD"
    tool_versions:
      simulator: "UNVERIFIED"
      lint: "UNVERIFIED"
      synthesis: "UNVERIFIED"
    evidence_references: []

  dependencies: []

  risks:
    open_issues: []
    accepted_risks: []

  relationships:
    replaces: []
    replaced_by: []
    depends_on: []

  maintenance:
    support_status: "TBD"
    maintenance_owner: "Dinesh Annayya"
    last_review_date: null
    next_review_date: null

  decisions: []
~~~

### 10.3 Lifecycle decision records

Each lifecycle decision SHOULD be stored as a separate immutable or append-only record.

Suggested structure:

~~~yaml
decision:
  id: "LCP-DEC-001"
  ip_id: "KIP-IP-EXAMPLE-001"
  decision_type: "INITIAL_ADOPTION"

  from_state: "proposed"
  to_state: "adopted"

  from_assurance_level: "L0"
  to_assurance_level: "L1"

  source_revision: "TBD"
  evidence_references: []

  rationale: "TBD"
  restrictions: []
  open_issues: []

  owner: "Dinesh Annayya"
  reviewer: "TBD"
  approver: "TBD"

  status: "PROPOSED"
  decision_date: null
~~~

The example is a proposed decision only. It MUST NOT be interpreted as an actual approval.

The `decision_type` value MUST be one of the following controlled values:

| decision_type | Use |
|---|---|
| `INITIAL_REGISTRATION` | First registration of an IP (no previous state; typically `proposed` at L0) |
| `INITIAL_ADOPTION` | The adoption decision from `proposed` to `adopted`, normally produced by the adoption process |
| `STATE_TRANSITION` | Any other change of lifecycle state, including activation, deprecation, replacement and retirement |
| `ASSURANCE_CHANGE` | A change of assurance level with no lifecycle state change |
| `CUSTOMIZATION` | A decision arising from a customization record |
| `UPSTREAM_UPDATE` | A decision arising from an upstream update or maintenance event |
| `EXCEPTION` | A decision that records or ends an approved exception or waiver |
| `REINSTATEMENT` | Reinstatement of a retired IP |

If a decision changes both state and assurance level, it uses the value that
matches the state change. Policy documents and templates MUST use only these
values. Adding a value requires a revision of this policy and of
`ip-lifecycle.schema.json`.

### 10.4 Record ownership

The IP repository owner is responsible for maintaining IP-specific lifecycle records.

The lifecycle owner MUST ensure that records remain synchronized with the actual source baseline and accepted evidence.

The programme governance repository remains authoritative for programme-level status, milestones, dependencies, and approvals within its defined scope.

The IP lifecycle record SHOULD reference relevant programme records where necessary rather than duplicating them.

### 10.5 Record history

Lifecycle records MUST preserve:

- Previous lifecycle states.
- Previous assurance levels.
- Previous source baselines.
- Approval decisions.
- Evidence references.
- Superseded decisions.
- Exceptions and waivers.
- Deprecation, replacement, and retirement history.

A current-state summary MAY be generated from historical records.

The generated summary MUST be distinguishable from the underlying authoritative records.

### 10.6 Record identifier conventions

| Record | Identifier form | Scope and notes |
|---|---|---|
| IP | `KIP-IP-<NAME>-NNN` | Global; assigned once |
| Lifecycle decision | `LCP-DEC-NNN` | Unique within one IP's lifecycle record; referenced globally as `<ip_id>/<decision id>` |
| Exception or waiver | `KIP-WVR-NNN` | Global |
| Requirement mapping | `KIP-MAP-NNN` | Global (public template; populated mappings are private) |
| Upstream watch register | `KIP-UPW-NNN` | Global |
| KVRF plan, suite, test, run | `KVRF-PLAN-`, `KVRF-SUITE-`, `KVRF-TST-`, `KVRF-RUN-` | Defined by the KVRF Specification |
| Policy requirement | `<DOC>-<CAT>-NNN` | For example `ADP-PR-001`; owned by that document |
| Open item | `<DOC>-OI-NNN` | Owned by that document |

Identifiers MUST NOT be reused or renumbered. The `NNN` values in templates
and examples (for example `LCP-DEC-001`) are placeholders and do not reserve
identifiers.

## 11. Relationship to IP adoption and customization

### 11.1 Adoption process

The IP Adoption Process defines how a candidate is evaluated and approved for adoption.

This lifecycle policy defines the state and assurance status resulting from that process.

An adoption process completion MUST NOT automatically imply that the IP is active or L3.

The adoption decision MUST specify the initial lifecycle state and assurance level.

### 11.2 Customization

Customization MAY affect lifecycle status and assurance level.

Examples include:

- Parameter configuration.
- Wrapper or adapter development.
- Source patching.
- Forking.
- Generated or derived implementation.

A customized IP MUST have traceability to its upstream or original source.

The owner MUST determine whether the customization invalidates existing evidence or requires a new assurance assessment.

Where customization creates a materially distinct IP deliverable, a separate lifecycle identity SHOULD be assigned.

### 11.3 Upstream maintenance

For upstream IP, lifecycle decisions MUST consider:

- Upstream support status.
- Security advisories.
- Licence changes.
- Source revision changes.
- Known defects.
- Project maintenance activity.
- Availability of replacement or migration options.

The IP Upstream Maintenance Policy defines the detailed monitoring and update process.

An upstream project becoming inactive does not automatically retire the adopted IP. The KRITVA lifecycle owner MUST assess the impact and record the maintenance decision.

## 12. Deprecation, replacement, and retirement controls

### 12.1 Deprecation notice

A deprecation notice MUST be available to affected consumers.

The notice SHOULD identify:

- IP name and identifier.
- Current lifecycle state.
- Deprecation reason.
- Effective date.
- Affected configurations or interfaces.
- Whether existing deployments may continue.
- Migration recommendation.
- Replacement status.
- Contact or owner.

The notice MAY be published in the IP repository, release notes, or an applicable integration registry.

### 12.2 Migration planning

Where an IP is replaced, the migration plan SHOULD consider:

- Interface compatibility.
- Functional equivalence.
- Parameter and configuration differences.
- Reset and clock behavior.
- Verification differences.
- Performance and implementation impact.
- Dependency changes.
- Licence and provenance implications.
- Required changes in consumer repositories.
- Evidence required to accept the migration.

Migration completion MUST be evidenced where the replacement decision requires it.

### 12.3 Legacy support

A deprecated or replaced IP MAY remain supported for existing deployments.

The lifecycle record MUST define:

- Supported legacy configurations.
- Whether defect fixes are accepted.
- Whether security fixes are accepted.
- Whether interface changes are prohibited.
- Expected support duration or review date.
- Conditions that would trigger retirement.

Legacy support MUST NOT be interpreted as approval for new integration.

### 12.4 Retirement and archival

Retired IP source and evidence SHOULD be retained in a controlled archive.

The archive SHOULD preserve:

- Final source revision.
- Release and configuration manifests.
- Licence and provenance records.
- Verification evidence.
- Lifecycle decisions.
- Known limitations.
- Replacement or migration records.
- Relevant integration references.

Archive retention MUST comply with applicable licence, security, legal, and organizational requirements.

The retired state MUST remain visible in the lifecycle registry even if the source repository is archived or made read-only.

## 13. Exceptions and waivers

### 13.1 General requirements

An exception to this policy MUST be explicit.

Each exception MUST include:

- Exception identifier.
- Affected IP identifier.
- Requirement or policy clause.
- Reason for exception.
- Technical and operational impact.
- Risk assessment.
- Compensating controls, where applicable.
- Scope and validity period.
- Owner.
- Reviewer.
- Approver.
- Review or expiry date.

### 13.2 Exception restrictions

An exception MUST NOT:

- Convert failed evidence into passing evidence.
- Imply that an assurance criterion has been satisfied.
- Hide a known lifecycle restriction.
- Authorize use outside its stated scope.
- Override third-party licence obligations.
- Remove required provenance information.

### 13.3 Expiry and review

Exceptions SHOULD have an expiry date or explicit review trigger.

Expired exceptions MUST NOT be treated as current approval.

An exception that remains necessary MUST be reviewed and renewed through a new or updated recorded decision.

### 13.4 Waiver types, validity and approval

The `waiver_type` of an exception or waiver record MUST be one of:

| waiver_type | Applies to |
|---|---|
| `LIFECYCLE_EXCEPTION` | An exception to a lifecycle, assurance or transition criterion in this policy |
| `VERIFICATION_WAIVER` | A required verification activity or evidence item not performed or not accepted |
| `COVERAGE_EXCLUSION` | A coverage item excluded from the closure target (KVRF section 11.8) |
| `ACTIVE_HIGH_RESET` | Use of an active-high reset (KIP-STD-CLKRST-009) |
| `RTL_STANDARD_DEVIATION` | A deviation from another RTL or interface requirement of the common standard or a profile |
| `OTHER_STANDARD_EXCEPTION` | Any other approved deviation; the clause MUST be identified |

Rules for all waiver types:

1. A waiver is effective only when its status is `APPROVED` and the current
   date is before `expiry_date`.
2. `expiry_date` MUST be set before approval. It MUST NOT exceed 12 months
   from `approval_date` unless the approver records a longer period and the
   reason (LCP-OI-022).
3. Renewal requires a new or updated recorded decision and a reassessment of
   risk; it MUST NOT happen automatically.
4. A waiver MUST name the affected IP, revision and configuration, and the
   exact requirement or clause waived.
5. Approval authority follows section 8.2 (exception approver), or section 8.5
   while the interim sole-owner mode is in effect.
6. A waiver never changes an evidence outcome. Failed or missing evidence
   remains `FAIL`, `BLOCKED`, `NOT_RUN` or `INCONCLUSIVE` under the KVRF
   evidence schema.
7. `WAIVED` is a requirement-level compliance status used in adoption and
   customization assessments. It is not a KVRF test outcome.

## 14. Lifecycle monitoring and review

### 14.1 Periodic review

Every active, deprecated, and replaced IP MUST have a defined review cadence or review trigger.

The review SHOULD consider:

- Source changes.
- Open defects.
- Verification evidence freshness.
- Security advisories.
- Licence and provenance changes.
- Dependency changes.
- Consumer and integration status.
- Assurance-level validity.
- Replacement and retirement plans.

The review date and outcome MUST be recorded.

### 14.2 Event-driven review

A lifecycle review MUST be triggered when a material event affects the IP's approved use or evidence.

Examples include:

- A critical functional defect.
- A security vulnerability.
- A licence change.
- An upstream project discontinuation.
- An interface-breaking change.
- A material source customization.
- An invalidated verification result.
- A change in intended product or integration scope.
- A replacement decision.
- A significant change in maintenance ownership.

### 14.3 Lifecycle health

A lifecycle dashboard MAY report:

- Counts by lifecycle state.
- Counts by assurance level.
- IP items with overdue reviews.
- IP items with unresolved critical issues.
- IP items with invalidated evidence.
- Deprecated IP with active consumers.
- Replaced IP with incomplete migration.
- Retired IP still referenced by active integrations.
- IP with unverified tool versions.
- IP with missing owner or approval information.

A dashboard MUST NOT infer that an IP is compliant or qualified solely from its state or assurance-level label.

## 15. Security, licence, and provenance considerations

Lifecycle decisions MUST consider relevant security, licence, and provenance information.

For third-party and open-source IP:

1. The source origin MUST be recorded.
2. The applicable licence MUST be identified or explicitly marked unknown.
3. Required notices and attribution MUST be retained.
4. Material licence changes MUST trigger review.
5. Security advisories MUST be assessed for applicability.
6. Known vulnerabilities MUST be dispositioned.
7. Upstream revision changes MUST be traceable.
8. Forks and patches MUST be documented under the customization and upstream maintenance policies.

An IP MUST NOT be represented as approved for a use that is prohibited by its applicable licence or unresolved legal restriction.

Security or licence concerns MAY require a transition to deprecated or retired, depending on impact and approved disposition.

## 16. Interface and technology-boundary considerations

Lifecycle approval MUST consider applicable KRITVA IP Standard requirements.

The following common policy positions apply:

### 16.1 Control bus

APB is the primary control/register bus for KRITVA IP.

The APB revision and detailed profile remain subject to the applicable standard decision.

AXI4 MAY be used for data or high-bandwidth interfaces.

AXI4-Lite, AHB-Lite, and Wishbone MAY be used only through documented bridges where permitted by the applicable standard and integration profile.

Lifecycle approval MUST identify the interface actually supported by the IP.

### 16.2 Reset conventions

The default reset convention is active-low.

The common reset naming convention is:

`rst_<domain>_n_i`

An active-high reset requires an approved waiver with rationale.

Reset synchronizer implementation MUST follow the approved RTL library manifest and applicable common standards.

### 16.3 Technology-dependent RTL

The approved RTL library manifest is the sole technology boundary for technology-dependent RTL.

An IP MUST NOT introduce unapproved foundry-specific cells or technology-dependent implementation dependencies.

Lifecycle review MUST assess whether the IP complies with the approved library boundary for its declared scope.

### 16.4 Evidence and verification

New KRITVA-developed IP at L2 and above SHOULD use the KVRF reference flow with cocotb.

Equivalent flows are permitted when they produce evidence records conforming to the applicable KVRF evidence schema.

The assurance decision is based on accepted outcomes and evidence, not the brand or name of the simulator or verification tool.

## 17. Compliance

An IP lifecycle record is compliant with this policy when:

1. The IP has a unique identity.
2. Exactly one current lifecycle state is declared.
3. An assurance level is declared.
4. The owner and intended use scope are identified.
5. The current source baseline is traceable.
6. Required transition approvals are recorded.
7. Assurance claims are supported by accepted evidence.
8. Open risks and known limitations are visible.
9. Deprecation, replacement, and retirement relationships are explicit where applicable.
10. Historical decisions and evidence remain traceable.

A compliance review MUST distinguish:

- Compliant.
- Non-compliant.
- Partially compliant.
- Not assessed.
- Not applicable.

A `NOT ASSESSED` result MUST NOT be represented as compliant.

A lifecycle record with missing mandatory information MUST NOT be considered fully compliant.

## 18. Implementation guidance

### 18.1 Repository structure

An IP repository MAY use a structure similar to:

~~~
ip-repository/
├── README.md
├── LICENSE
├── rtl/
├── verification/
├── docs/
│   ├── IP_SPECIFICATION.md
│   ├── LIFECYCLE.md
│   ├── ACCEPTANCE_CRITERIA.md
│   └── RELEASE_NOTES.md
├── lifecycle/
│   ├── lifecycle.yaml
│   ├── decisions/
│   ├── reviews/
│   ├── exceptions/
│   └── evidence-index.yaml
└── scripts/
~~~

This is illustrative only. The policy does not mandate a repository layout.

The owning repository MUST declare the authoritative location of its lifecycle records.

### 18.2 Automation

Lifecycle validation MAY be automated.

Automation MAY check:

- Required lifecycle fields.
- Allowed state values.
- Allowed assurance-level values.
- Source revision presence.
- Decision record references.
- Evidence references.
- Owner and approver fields.
- Required deprecation or replacement metadata.
- Review dates.
- Schema validity.

Automation MUST NOT infer approval from a field that is merely populated.

Automation MUST NOT promote an IP to a lifecycle state or assurance level unless the governing approval process explicitly authorizes that action.

### 18.3 Generated reports

Reports MAY be generated from lifecycle records.

Generated reports SHOULD identify:

- Generation timestamp.
- Source revision.
- Schema version.
- Report generator version.
- Data completeness limitations.

Generated reports MUST NOT replace authoritative lifecycle records or approval evidence.

## 19. Open items

The following items remain open for policy finalization. Each item is owned by Dinesh Annayya.

| ID | Open item | Required decision |
|---|---|---|
| LCP-OI-001 | Lifecycle registry ownership | Confirm the authoritative lifecycle registry and its relationship to IP repositories. |
| LCP-OI-002 | Lifecycle record schema | Approve the canonical YAML or JSON schema and versioning approach. |
| LCP-OI-003 | Approval authority matrix | Confirm designated adoption, technical, lifecycle, and release authorities. |
| LCP-OI-004 | Delegation rules | Define permitted approval delegation and role separation. |
| LCP-OI-005 | L0-L3 acceptance criteria | Approve detailed, category-specific acceptance criteria and evidence expectations. |
| LCP-OI-006 | L2 verification minimums | Define the minimum required functional, structural, and integration verification by IP category. |
| LCP-OI-007 | L3 qualification scope | Define when product, technology, implementation, or silicon-specific qualification is required. |
| LCP-OI-008 | KVRF evidence schema | Confirm the applicable schema version and mandatory lifecycle evidence fields. |
| LCP-OI-009 | Evidence retention | Define minimum retention periods and archive ownership. |
| LCP-OI-010 | Evidence integrity | Define required hashes, signatures, or other integrity controls for evidence artifacts. |
| LCP-OI-011 | Tool-version policy | Define version pinning and acceptable tool-version changes by assurance level. |
| LCP-OI-012 | Lifecycle review cadence | Approve periodic review intervals for active and legacy IP. |
| LCP-OI-013 | Deprecation notice period | Define minimum notice periods where existing consumers are affected. |
| LCP-OI-014 | Legacy support duration | Define the expected support policy for deprecated and replaced IP. |
| LCP-OI-015 | Replacement acceptance | Define minimum evidence required to declare migration complete. |
| LCP-OI-016 | Retirement approval | Confirm the authority and conditions for retirement when active consumers remain. |
| LCP-OI-017 | Reinstatement rules | Confirm whether retired IP can be reinstated under the same identity or requires a new identity. |
| LCP-OI-018 | Exception validity | Define maximum exception duration and renewal requirements. |
| LCP-OI-019 | Lifecycle automation | Decide which lifecycle checks are mandatory CI gates and which remain advisory. |
| LCP-OI-020 | Lifecycle dashboard | Decide whether a consolidated lifecycle dashboard is required and where it is maintained. |
| LCP-OI-021 | Interim sole-owner operating mode | Approve, revise or reject section 8.5, including the re-review period after the interim mode ends. |
| LCP-OI-022 | Waiver validity period | Confirm the 12-month default maximum and the conditions for a longer period (section 13.4). |

No open item is considered approved by its inclusion in this table.

An open item MUST be closed through an explicit owner decision and, where required, a revision to this policy or its supporting schema.

## 20. Change control

Changes to this policy MUST be reviewed and approved by the designated policy owner or authorized delegate.

Changes MUST preserve:

- Existing lifecycle decision history.
- Existing IP identifiers.
- Existing requirement identifiers.
- Historical assurance assessments.
- Evidence traceability.
- Explicit replacement and retirement relationships.

A policy revision MUST identify material changes and their impact on existing IP lifecycle records.

A policy change MUST NOT silently invalidate previously approved lifecycle decisions.

Where a policy change requires reassessment, the affected IP items and reassessment criteria MUST be identified.

### 20.1 Versioning

The policy uses semantic versioning:

- MAJOR: incompatible changes to lifecycle states, assurance-level semantics, or mandatory governance requirements.
- MINOR: new requirements or capabilities that remain compatible with existing records.
- PATCH: editorial corrections, clarifications, and non-semantic changes.

The initial version is `0.1.0`, with status `DRAFT`.

### 20.2 Review and approval history

| Version | Date | Author | Status | Description |
|---|---|---|---|---|
| 0.1.0 | TBD | Dinesh Annayya | DRAFT | Initial KRITVA IP Lifecycle Policy. |

## 21. References

The following documents are relevant to this policy:

1. KRITVA IP Standard.
2. KRITVA Open Source IP Policy.
3. KRITVA IP Adoption Process.
4. KRITVA IP Customization Policy.
5. KRITVA IP Upstream Maintenance Policy.
6. Applicable KRITVA verification requirements and KVRF evidence schema.
7. Applicable approved RTL library manifest.
8. Applicable IP-specific specifications, requirements, and acceptance criteria.
9. Applicable SoC integration profiles and product-specific requirements.

The authoritative revision of each referenced document MUST be identified when used for a lifecycle approval.

External standards and tools MUST be referenced by their applicable revision or version when that information is verified. Unverified versions MUST be identified as `UNVERIFIED`.

---

**End of Document**
