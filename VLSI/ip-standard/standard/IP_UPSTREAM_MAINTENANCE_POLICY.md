# KRITVA IP Upstream Maintenance Policy

| Field | Value |
|---|---|
| Document ID | KSTD-IPUPM-001 |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | Public |
| Owner | Dinesh Annayya |
| Applies to | KRITVA-developed and adopted third-party IP with upstream dependencies |
| Related standard | `KRITVA_IP_STANDARD.md` |
| Related policy | `OPEN_SOURCE_IP_POLICY.md` |
| Related processes | `IP_ADOPTION_PROCESS.md`, `IP_CUSTOMIZATION_POLICY.md` |
| Related SoC profile | `KNX-RTL-STD-001` |
| Last updated | 2026-11-13 |

---

## 1. Purpose

This document defines the policy and operating process for monitoring, maintaining, updating, and retiring upstream IP dependencies used within the KRITVA ecosystem.

Upstream IP is subject to change. A project may publish new releases, modify its source code, change its license, disclose vulnerabilities, lose maintainers, become archived, or discontinue support.

Such changes can affect:

- Functional correctness.
- Security and supply-chain integrity.
- License compatibility.
- Redistribution rights.
- Technical compatibility.
- Verification results.
- KRITVA customizations.
- Integration assumptions.
- Long-term maintainability.
- Product and release readiness.

This policy establishes a controlled upstream maintenance process to ensure that adopted components remain traceable, supportable, and suitable for their approved use.

The objectives are to:

1. Establish a repeatable upstream monitoring process.
2. Track upstream changes against immutable source revisions.
3. Identify security, license, technical, and project-health risks.
4. Classify and triage upstream events consistently.
5. Evaluate updates before adoption.
6. Preserve KRITVA customization and verification history.
7. Define controlled responses to license changes and security advisories.
8. Manage abandoned, archived, and discontinued upstream projects.
9. Define deprecation and replacement procedures.
10. Maintain auditable upstream watch and maintenance records.

This document is a public maintenance policy baseline. It does not disclose unreleased SoC implementation details or approve any specific upstream dependency.

## 2. Scope

This policy applies to upstream projects and external dependencies used by KRITVA, including:

- Third-party RTL IP.
- Verification IP and testbench components.
- Reference implementations.
- Firmware and software dependencies.
- Build and development tools.
- Generated source dependencies.
- Scripts and automation components.
- Documentation and specification dependencies.
- Libraries and packages used by IP repositories.
- Vendor-provided components with an identifiable upstream release process.
- KRITVA-maintained forks of upstream projects.

It applies to dependencies used for development, evaluation, integration, verification, distribution, and maintenance.

It covers both direct dependencies and material transitive dependencies where their source, license, security, or maintenance status affects KRITVA.

A dependency may be monitored even when it is not approved for production adoption. Monitoring status MUST NOT be interpreted as adoption approval.

## 3. Relationship to Other KRITVA Documents

This policy supplements the following documents:

| Document | Responsibility |
|---|---|
| `KRITVA_IP_STANDARD.md` | Defines the common IP design and integration baseline. |
| `OPEN_SOURCE_IP_POLICY.md` | Defines third-party source classification, licensing, provenance, notices, and adoption controls. |
| `IP_ADOPTION_PROCESS.md` | Defines discovery, evaluation, intake, adoption decisions, and integration readiness. |
| `IP_CUSTOMIZATION_POLICY.md` | Defines customization categories, source modifications, re-verification, and upstream rebase handling. |
| `KNX-RTL-STD-001` | Defines the applicable Nexus-specific RTL design profile. |

This policy governs the continuing monitoring and maintenance of upstream dependencies after initial discovery or adoption.

It does not replace the initial adoption process.

An upstream update that changes the adopted source revision, intended use, license, or integration scope MUST be evaluated through the applicable adoption and customization reassessment requirements.

## 4. Normative Language

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are normative terms.

The common KRITVA standards use RFC 2119 `MUST` terminology.

The `SHALL` terminology used by `KNX-RTL-STD-001` is equivalent in normative force to `MUST`.

Where applicable requirements conflict, the stricter requirement governs within its scope.

A monitoring result, security advisory, upstream release, or automated scan result does not itself authorize an update or change to an approved KRITVA baseline.

## 5. Upstream Maintenance Principles

| ID | Principle | Policy |
|---|---|---|
| UPM-PR-001 | Immutable traceability | Every monitored upstream baseline MUST be tied to an immutable commit or equivalent source revision. |
| UPM-PR-002 | Continuous awareness | Material upstream changes SHOULD be monitored throughout the dependency lifecycle. |
| UPM-PR-003 | Controlled updates | An upstream release MUST NOT be adopted automatically. |
| UPM-PR-004 | Risk-based response | Monitoring and response priority MUST reflect technical, security, license, and project-health risk. |
| UPM-PR-005 | Provenance preservation | Previous and proposed upstream revisions MUST remain traceable. |
| UPM-PR-006 | License compliance | License changes MUST be evaluated before further adoption or redistribution. |
| UPM-PR-007 | Customization preservation | KRITVA patches, wrappers, configurations, and forks MUST remain identifiable during updates. |
| UPM-PR-008 | Re-verification | Material source or configuration changes MUST trigger appropriate re-verification. |
| UPM-PR-009 | Controlled retirement | Abandoned or unsuitable upstream projects MUST be handled through an explicit maintenance or retirement decision. |
| UPM-PR-010 | Evidence | Monitoring, triage, update, and retirement decisions MUST have traceable records. |
| UPM-PR-011 | Technology boundary | Technology-dependent RTL MUST remain within the approved RTL library manifest as the sole technology boundary. |
| UPM-PR-012 | Public/private separation | Public maintenance records MUST NOT disclose restricted information or unreleased implementation details. |

## 6. Upstream Dependency Classification

### 6.1 Dependency identity

Every upstream dependency under active maintenance MUST have a stable component identifier.

The identifier MUST be associated with:

- Component name.
- Upstream project.
- Upstream organization or maintainer.
- Authoritative upstream location.
- Source category.
- License.
- Approved or monitored revision.
- KRITVA consuming repository or component.
- Maintenance owner.
- Current maintenance status.

A component identifier MUST remain stable while the logical dependency remains the same.

A materially different replacement component MUST receive a separate identifier.

The identifier MUST NOT be confused with:

- A KRITVA standard requirement ID.
- A Nexus RTL requirement ID.
- An upstream issue or pull request number.
- An upstream commit hash.
- A customization identifier.
- A verification test identifier.

### 6.2 Dependency categories

| Category ID | Category | Description |
|---|---|---|
| UPM-CAT-001 | Third-party open-source IP | Public IP or source project under an identifiable open-source license. |
| UPM-CAT-002 | Vendor-provided IP | IP or collateral supplied under vendor terms. |
| UPM-CAT-003 | Verification dependency | Verification libraries, testbenches, reference models, and related components. |
| UPM-CAT-004 | Development tool dependency | Tools and utilities used for development, build, or verification. |
| UPM-CAT-005 | Generated-source dependency | Generator, template, schema, or source used to produce IP collateral. |
| UPM-CAT-006 | KRITVA-maintained fork | A KRITVA-controlled fork of an upstream project. |
| UPM-CAT-007 | Documentation or specification dependency | External specifications, reference documents, or schemas used by an IP component. |
| UPM-CAT-008 | Transitive dependency | A dependency introduced through another adopted component. |

A dependency MAY have more than one category when the source provides multiple types of material.

### 6.3 Dependency relationship

The maintenance record SHOULD identify the relationship between the dependency and its KRITVA consumer.

Examples include:

- Direct source dependency.
- Wrapper or adapter dependency.
- Verification-only dependency.
- Build-time dependency.
- Generated-source dependency.
- Toolchain dependency.
- Documentation reference.
- Transitive dependency.

The relationship MUST be sufficiently clear to identify the impact of an upstream event.

### 6.4 Classification requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-CLS-001 | Every actively monitored dependency MUST have a stable component identifier. | R |
| UPM-CLS-002 | Every dependency MUST have a source category. | R |
| UPM-CLS-003 | The upstream source and consuming KRITVA component MUST be identifiable. | R |
| UPM-CLS-004 | Direct and transitive dependencies SHOULD be distinguished. | R |
| UPM-CLS-005 | The dependency relationship MUST be recorded sufficiently to assess impact. | R |
| UPM-CLS-006 | Monitoring status MUST NOT imply adoption approval. | R |

## 7. Upstream Monitoring

### 7.1 Monitoring objectives

Upstream monitoring identifies material changes that may affect the suitability of an adopted or evaluated dependency.

Monitoring MUST consider, where applicable:

1. New releases and release candidates.
2. New commits and changes to the default branch.
3. Security advisories and vulnerability disclosures.
4. License changes and additional licensing terms.
5. Project maintenance and health.
6. Upstream issue and defect activity.
7. Changes to interfaces, parameters, and configuration.
8. Changes to build and verification requirements.
9. Changes to dependencies.
10. Changes to documentation and specifications.
11. Project archival or abandonment.
12. Changes to redistribution or source availability.

Monitoring depth SHOULD be proportional to dependency criticality and risk.

### 7.2 Release monitoring

The maintainer SHOULD monitor:

- Official upstream releases.
- Release notes.
- Release tags.
- Release candidate announcements.
- Changes to supported versions.
- Deprecated interfaces or features.
- Changes to build instructions.
- Changes to license files.
- Release integrity information, where available.

A release tag MUST NOT be treated as an immutable source reference without resolving it to an immutable commit or equivalent revision where the upstream system supports it.

A new release is a candidate for evaluation, not an automatic update.

### 7.3 Commit monitoring

Commit monitoring SHOULD identify changes that may affect:

- RTL functionality.
- Interfaces and parameters.
- Clock and reset behavior.
- Verification infrastructure.
- Build and configuration scripts.
- Security-sensitive code.
- License and attribution information.
- Generated source.
- Dependencies.
- Documentation describing supported behavior.

The maintainer SHOULD distinguish routine changes from changes that materially affect the adopted KRITVA use case.

A commit notification alone does not require an update. Its relevance MUST be assessed.

### 7.4 Security advisory monitoring

Security monitoring SHOULD use authoritative and relevant sources, including:

- Upstream security advisories.
- Official project announcements.
- Maintainer security notifications.
- Public vulnerability databases.
- Relevant vendor security notices.
- Security mailing lists or coordinated disclosure notices.
- Verified reports from recognized security researchers.

A security report MUST be evaluated for applicability to the adopted component and its actual use.

A vulnerability affecting an unused feature or configuration may have a different impact from a vulnerability affecting an enabled feature or exposed interface.

The assessment MUST document the applicability rationale.

### 7.5 License monitoring

License monitoring MUST identify material changes to:

- Repository-level license declarations.
- File-level license headers.
- License text.
- License exceptions.
- Copyright ownership statements.
- Patent terms.
- Redistribution conditions.
- Additional commercial or vendor restrictions.
- Contributor licensing terms, where relevant.

A change in license MUST trigger a license reassessment before adopting the changed source revision or distributing affected material.

The existence of an older approved license record does not establish that a later upstream revision has the same licensing conditions.

### 7.6 Project-health monitoring

Project health SHOULD be assessed using relevant evidence such as:

- Maintainer activity.
- Release frequency.
- Issue response and resolution.
- Pull request review activity.
- Security response activity.
- Documentation maintenance.
- Contributor continuity.
- Availability of build and verification infrastructure.
- Dependency maintenance.
- Public project status.
- Explicit maintenance or archival announcements.

No single activity metric MUST be treated as conclusive evidence of project health.

A low commit rate does not automatically mean a project is abandoned. A high commit rate does not automatically mean it is well maintained.

The assessment MUST consider the component's actual maintenance needs and risk.

### 7.7 Monitoring requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-MON-001 | Active upstream dependencies MUST have a monitoring record. | R |
| UPM-MON-002 | Monitoring MUST identify the immutable upstream baseline. | R |
| UPM-MON-003 | Release changes SHOULD be monitored for dependencies with active upstream releases. | R |
| UPM-MON-004 | Material commit changes SHOULD be reviewed for impact on the adopted component. | R |
| UPM-MON-005 | Security advisories MUST be assessed for applicability and impact. | R |
| UPM-MON-006 | License changes MUST trigger license reassessment. | R |
| UPM-MON-007 | Project-health risks SHOULD be assessed for maintained dependencies. | R |
| UPM-MON-008 | Monitoring frequency MUST be appropriate to dependency criticality and risk. | R |
| UPM-MON-009 | Monitoring results MUST be recorded or linked to the relevant watch record. | R |
| UPM-MON-010 | Automated notifications MUST NOT be treated as completed technical or license assessment. | R |

## 8. Monitoring Frequency and Triggers

### 8.1 Risk-based monitoring

Monitoring frequency SHOULD reflect:

- Component criticality.
- Exposure to external interfaces.
- Security sensitivity.
- License complexity.
- Update frequency.
- Upstream maintenance activity.
- Customization complexity.
- Availability of security and release notifications.
- Consequences of an undiscovered upstream change.

The maintenance owner MUST record the selected monitoring approach.

This policy does not impose a universal monitoring interval. Required monitoring intervals remain an owner decision.

### 8.2 Event-driven monitoring

The following events SHOULD trigger immediate or prioritized review:

- A security advisory affecting the component.
- An upstream license change.
- A critical defect disclosure.
- A release that removes or changes supported interfaces.
- An upstream project archival announcement.
- A maintainer announcement that support has ended.
- A dependency compromise or source integrity concern.
- A significant change to the upstream repository.
- A change to the approved source distribution location.
- A material change to the KRITVA use case.

### 8.3 Monitoring schedule record

A monitoring schedule SHOULD identify:

| Field | Description |
|---|---|
| Monitoring owner | Person responsible for the dependency. |
| Monitoring method | Manual review, notification, automated scan, or combination. |
| Monitoring frequency | Selected review interval or event-driven method. |
| Monitored sources | Authoritative upstream and security sources. |
| Last reviewed | Date of the last completed review. |
| Next review | Planned review date or condition. |
| Escalation contact | Responsible owner or authorized reviewer. |
| Criticality | Dependency criticality classification. |

### 8.4 Frequency requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-FRQ-001 | Every actively maintained dependency MUST have an identified monitoring owner. | R |
| UPM-FRQ-002 | The monitoring method MUST be recorded. | R |
| UPM-FRQ-003 | Monitoring frequency SHOULD reflect dependency risk and criticality. | R |
| UPM-FRQ-004 | Event-driven monitoring MUST be supported for material security and license events. | R |
| UPM-FRQ-005 | A missed or overdue monitoring review SHOULD be recorded and assessed. | R |

## 9. Upstream Watch Records

### 9.1 Watch record purpose

An upstream watch record tracks the current monitored baseline and material upstream events.

It MUST link the upstream project to the KRITVA component that consumes or evaluates it.

The watch record is not an adoption approval record.

A dependency MAY have a watch record while its adoption disposition remains REVIEW or DENY.

### 9.2 Immutable baseline

Every watch record MUST identify the upstream revision used as the comparison baseline.

The record SHOULD include:

- Immutable commit hash.
- Release identifier.
- Source repository location.
- Source snapshot checksum, where available.
- Date the revision was observed.
- KRITVA consuming component.
- Current adopted or evaluated revision.

A mutable branch name MAY be recorded as a monitoring reference but MUST NOT replace the immutable baseline.

### 9.3 Watch event record

Every material event SHOULD have an event record containing:

- Event identifier.
- Component identifier.
- Event type.
- Upstream event date.
- Date detected.
- Source reference.
- Affected upstream revision.
- Current KRITVA baseline.
- Initial impact assessment.
- Severity.
- Triage outcome.
- Assigned owner.
- Required action.
- Decision reference.
- Closure evidence.

### 9.4 Event immutability

Watch records SHOULD preserve the history of observed events.

A record MUST NOT be rewritten to make an earlier source revision appear to have been the current baseline at the time of an earlier decision.

Corrections MUST be recorded with a reason and sufficient history to reconstruct the original observation.

### 9.5 Watch record requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-WAT-001 | Every actively monitored dependency MUST have a watch record. | R |
| UPM-WAT-002 | A watch record MUST identify an immutable upstream baseline. | R |
| UPM-WAT-003 | Material upstream events MUST have traceable event references. | R |
| UPM-WAT-004 | Watch records MUST identify the affected KRITVA component or consumer. | R |
| UPM-WAT-005 | Event records MUST distinguish upstream event dates from KRITVA detection dates. | R |
| UPM-WAT-006 | Watch history MUST preserve previous baselines and material decisions. | R |
| UPM-WAT-007 | A mutable branch name MUST NOT be the sole baseline reference. | R |

## 10. Triage and Severity Classification

### 10.1 Triage objectives

Triage determines:

- Whether an upstream event is relevant.
- Which KRITVA components are affected.
- Whether the event introduces a security, license, technical, or maintenance risk.
- Whether immediate containment is required.
- Whether a source update or other action is necessary.
- Whether owner escalation is required.

Triage MUST be recorded even when the event is determined to have no impact.

### 10.2 Severity classes

The following severity classes define the default maintenance response priority.

| Severity | Name | Description | Default handling |
|---|---|---|---|
| S0 | Critical | Confirmed or strongly suspected issue with immediate unacceptable security, legal, integrity, or operational impact. | Immediate escalation and containment assessment. |
| S1 | High | Material vulnerability, license issue, functional defect, or upstream change that may compromise an approved use. | Priority investigation and owner decision. |
| S2 | Medium | Relevant issue or upstream change with a manageable impact or available workaround. | Planned remediation or controlled update. |
| S3 | Low | Minor issue, maintenance concern, non-blocking defect, or change with limited impact. | Track and address through normal maintenance. |
| S4 | Informational | No current impact; informational release, commit, project, or documentation event. | Record and monitor. |

Severity MUST be based on the impact on the KRITVA use case, not solely on an upstream severity label.

An upstream advisory marked critical may have reduced applicability if the affected functionality is not present or enabled. Such a conclusion MUST have a documented technical rationale.

A low upstream severity MUST NOT prevent KRITVA from assigning a higher severity when the actual use creates greater risk.

### 10.3 Event types

Each event SHOULD be assigned one or more event types.

| Event type | Description |
|---|---|
| RELEASE | New upstream release or release candidate. |
| COMMIT | Material source change. |
| SECURITY | Vulnerability disclosure or security advisory. |
| LICENSE | License or rights change. |
| DEFECT | Functional or technical defect report. |
| INTERFACE | Interface or parameter change. |
| DEPENDENCY | Change to an upstream dependency. |
| PROJECT_HEALTH | Maintenance or project continuity concern. |
| ARCHIVAL | Project marked archived or read-only. |
| ABANDONMENT | Evidence that upstream maintenance has ceased. |
| INTEGRITY | Source compromise, tampering, or provenance concern. |
| DOCUMENTATION | Material documentation or specification change. |
| DEPRECATION | Feature or component marked deprecated. |
| OTHER | Other relevant event requiring assessment. |

### 10.4 Triage outcome

A triage record MUST use one of the following outcomes:

| Outcome | Meaning |
|---|---|
| NO_IMPACT | Event does not affect the KRITVA use case. |
| MONITOR | Event is relevant but requires no immediate action. |
| INVESTIGATE | Additional technical, license, or security assessment is required. |
| UPDATE_REQUIRED | A source or configuration update is required. |
| CONTAINMENT_REQUIRED | Immediate containment or use restriction is required. |
| OWNER_DECISION | An owner decision is required before proceeding. |
| REJECT_UPDATE | Proposed upstream change is unsuitable. |
| CLOSE | Event has been resolved or dispositioned with evidence. |

A triage outcome MUST identify the reason and the evidence supporting it.

### 10.5 Severity assignment criteria

Severity assessment SHOULD consider:

- Actual exposure in the adopted configuration.
- Potential impact on functional correctness.
- Security impact and exploitability.
- License and redistribution implications.
- Integrity and provenance risk.
- Availability of a workaround.
- Availability of a fixed upstream revision.
- Complexity of applying a local correction.
- Impact on active KRITVA development or releases.
- Impact on downstream consumers.

### 10.6 Triage requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-TRI-001 | Every material upstream event MUST be triaged. | R |
| UPM-TRI-002 | Triage MUST identify affected KRITVA components. | R |
| UPM-TRI-003 | Severity MUST reflect the actual KRITVA use case and impact. | R |
| UPM-TRI-004 | Triage MUST record an explicit outcome. | R |
| UPM-TRI-005 | Events requiring owner action MUST be escalated. | R |
| UPM-TRI-006 | NO_IMPACT decisions MUST include a rationale. | R |
| UPM-TRI-007 | Severity and triage outcomes MUST be updated when material facts change. | R |

## 11. Security Response

### 11.1 Security response principles

A security advisory affecting an adopted component MUST be evaluated promptly.

The assessment MUST determine:

- Whether the affected source or functionality exists in the adopted revision.
- Whether the affected feature is enabled.
- Whether the affected interface is reachable in the intended use.
- Whether the vulnerability is exploitable under the KRITVA deployment assumptions.
- Whether a workaround exists.
- Whether a fixed upstream revision is available.
- Whether a local mitigation is appropriate.
- Whether public disclosure or release action is required.
- Whether downstream consumers must be notified.

Security response MUST distinguish confirmed findings from unverified reports.

### 11.2 Security severity

The upstream severity classification SHOULD be retained as source information.

KRITVA MUST independently assess the actual impact on its use case.

The assessment SHOULD include:

- Upstream advisory identifier.
- Upstream severity and scoring information, if available.
- Affected versions.
- Fixed versions.
- KRITVA affected revision.
- Applicability.
- Exposure.
- Mitigation.
- Residual risk.
- Response owner.
- Required action.
- Closure evidence.

### 11.3 Response actions

Possible actions include:

- Continue monitoring.
- Disable an affected feature.
- Restrict use of the affected component.
- Apply a documented mitigation.
- Apply a local patch.
- Adopt a fixed upstream revision.
- Revert to a previously approved revision.
- Temporarily suspend adoption.
- Revoke approval.
- Replace or retire the component.
- Notify affected downstream consumers.

A response action MUST be proportionate to the risk and must not violate applicable license or contractual obligations.

### 11.4 Security response timelines

Specific response and remediation time targets are owner decisions and are not established by this DRAFT.

The following placeholders define the timing categories that require approval.

| Severity | Initial triage target | Owner escalation target | Mitigation or disposition target | Status |
|---|---|---|---|---|
| S0 | TBD | TBD | TBD | OWNER DECISION |
| S1 | TBD | TBD | TBD | OWNER DECISION |
| S2 | TBD | TBD | TBD | OWNER DECISION |
| S3 | TBD | TBD | TBD | OWNER DECISION |
| S4 | TBD | TBD | TBD | OWNER DECISION |

These targets MUST be interpreted as response objectives after owner approval, not as currently established service levels.

An S0 event MUST be escalated for immediate owner attention even while the formal response timelines remain TBD.

### 11.5 Security response requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-SEC-001 | Security advisories MUST be assessed for applicability to the adopted revision and use case. | R |
| UPM-SEC-002 | KRITVA severity MUST reflect actual use and exposure. | R |
| UPM-SEC-003 | S0 events MUST be escalated for immediate owner attention. | R |
| UPM-SEC-004 | Security response actions MUST be recorded. | R |
| UPM-SEC-005 | Security mitigations MUST be evaluated for functional and integration impact. | R |
| UPM-SEC-006 | A security issue that makes the intended use unacceptable MUST prevent continued approved use until dispositioned. | R |
| UPM-SEC-007 | Security response timelines MUST remain marked TBD until approved by the owner. | R |
| UPM-SEC-008 | Security closure MUST include evidence of remediation, mitigation, or accepted disposition. | R |
| UPM-SEC-009 | Sensitive security details MUST follow the applicable disclosure and public/private controls. | R |

## 12. License Change Handling

### 12.1 License change triggers

A license reassessment MUST be initiated when any of the following occurs:

- Upstream repository changes its declared license.
- A new release changes licensing terms.
- File-level license headers change.
- A new license exception is introduced or removed.
- Copyright ownership information materially changes.
- Patent or redistribution terms change.
- New files are added under a different license.
- A dependency changes its license.
- A vendor changes usage or redistribution conditions.
- A previously missing license is newly identified.

### 12.2 License change assessment

The license reviewer MUST determine:

1. Which source revisions are affected.
2. Whether the current adopted revision is affected.
3. Whether the new license applies to existing files or only new changes.
4. Whether the new license is compatible with the approved use.
5. Whether modification obligations change.
6. Whether redistribution obligations change.
7. Whether source-disclosure obligations change.
8. Whether patent terms change.
9. Whether existing KRITVA modifications are affected.
10. Whether public or commercial distribution must be restricted.

The assessment MUST distinguish the license applying to the existing approved revision from the license applying to a proposed new revision.

A new upstream license does not automatically retroactively change the license of an earlier revision. The actual legal effect MUST be assessed rather than assumed.

### 12.3 License change outcomes

| Outcome | Meaning |
|---|---|
| RETAIN_EXISTING | Existing approved revision remains usable under its established license basis. |
| ALLOW_NEW_REVISION | New revision is approved after license reassessment. |
| REVIEW_NEW_REVISION | New revision is held pending license or legal review. |
| RESTRICT_DISTRIBUTION | Some distribution scopes are suspended or prohibited. |
| REJECT_NEW_REVISION | New revision is not adopted. |
| REVOKE_APPROVAL | Existing approval is withdrawn where continued use is not permitted or acceptable. |
| REPLACE_COMPONENT | A replacement is selected through a controlled adoption process. |

### 12.4 License-change requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-LIC-001 | Material license changes MUST trigger reassessment. | R |
| UPM-LIC-002 | The license of the current adopted revision MUST be distinguished from the proposed new revision. | R |
| UPM-LIC-003 | License obligations MUST be evaluated against each intended distribution scope. | R |
| UPM-LIC-004 | A new revision MUST NOT be adopted before its license assessment is completed. | R |
| UPM-LIC-005 | Redistribution MUST be restricted when required rights are unavailable or unresolved. | R |
| UPM-LIC-006 | License decisions MUST be recorded with evidence and reviewer references. | R |
| UPM-LIC-007 | Original upstream notices MUST be preserved during updates. | R |

## 13. Upstream Update Evaluation Workflow

### 13.1 Update evaluation principle

An upstream release or commit is a candidate change.

It MUST be evaluated before it replaces an approved KRITVA baseline.

The evaluation MUST consider the impact on:

- Provenance.
- Licensing.
- Technical behavior.
- Security.
- Project health.
- Customizations.
- Verification.
- Integration readiness.
- Release obligations.

### 13.2 Workflow overview

| Stage | Activity | Required result |
|---|---|---|
| UPM-ST-01 | Detect event | Upstream event identified and referenced. |
| UPM-ST-02 | Record event | Watch record updated with immutable source references. |
| UPM-ST-03 | Triage | Severity, impact, and outcome assigned. |
| UPM-ST-04 | Establish baseline | Current KRITVA and upstream revisions identified. |
| UPM-ST-05 | Compare revisions | Source and configuration differences assessed. |
| UPM-ST-06 | Reassess license and provenance | License and source rights reviewed. |
| UPM-ST-07 | Reassess security and health | Security and project-health impact reviewed. |
| UPM-ST-08 | Reassess customization | Wrappers, patches, forks, and configurations reviewed. |
| UPM-ST-09 | Reassess integration | Applicable KRITVA requirements checked. |
| UPM-ST-10 | Re-verify | Required verification evidence generated. |
| UPM-ST-11 | Decision | Update disposition recorded. |
| UPM-ST-12 | Controlled integration | Approved revision integrated and recorded. |
| UPM-ST-13 | Close event | Watch and maintenance records updated. |

A stage MAY be combined with another stage if the evidence and decision remain identifiable.

### 13.3 Baseline identification

The maintainer MUST identify:

- Current upstream immutable revision.
- Proposed upstream immutable revision.
- Current KRITVA customized revision.
- Current adopted release identifier, if applicable.
- Relevant source snapshot checksums, where available.
- Applicable customization records.
- Current adoption disposition.
- Current verification evidence.

The comparison MUST be reproducible from the recorded revisions.

### 13.4 Revision comparison

The update assessment SHOULD examine:

- Added files.
- Removed files.
- Modified files.
- Interface changes.
- Parameter changes.
- Reset and clock changes.
- Functional changes.
- Build changes.
- Verification changes.
- Dependency changes.
- License and notice changes.
- Security fixes.
- Deprecated functionality.
- Changes to supported configurations.

A source diff alone may not reveal all behavioral or licensing changes. Relevant release notes, advisories, documentation, and project announcements SHOULD also be reviewed.

### 13.5 Reuse of adoption reassessment outcomes

The update workflow MUST reuse the adoption and customization reassessment outcomes defined by the related KRITVA documents.

For adoption reassessment, the applicable outcomes are:

| Outcome | Meaning |
|---|---|
| RETAIN | Existing approval remains valid. |
| UPDATE | Approval is retained subject to the new source revision or revised conditions. |
| REVIEW | Adoption is under review pending further evidence or owner decision. |
| REVOKE | Existing adoption approval is withdrawn. |

For customization reassessment, the applicable outcomes are:

| Outcome | Meaning |
|---|---|
| RETAIN | Existing customization remains valid. |
| UPDATE | Customization is updated and re-verified against the new upstream baseline. |
| REVIEW | Customization is under review pending resolution. |
| REVOKE | Existing customization approval is withdrawn. |

The update event record MUST identify both outcomes when the dependency has a KRITVA customization.

### 13.6 Update decision

The final update decision MUST use one of the following:

| Decision | Meaning |
|---|---|
| ACCEPT_UPDATE | Proposed revision is accepted for the approved scope. |
| HOLD_UPDATE | Update is deferred pending additional information or action. |
| REJECT_UPDATE | Proposed revision is not accepted. |
| RETAIN_CURRENT | Existing approved revision remains in use. |
| REVOKE_CURRENT | Current approval is withdrawn. |
| REPLACE_COMPONENT | A replacement is initiated through the adoption process. |
| RETIRE_COMPONENT | Component is retired through the controlled retirement process. |

The decision MUST include:

- Decision date.
- Decision owner.
- Current and proposed revisions.
- Adoption reassessment outcome.
- Customization reassessment outcome, where applicable.
- License disposition.
- Security disposition.
- Verification result.
- Integration-readiness result.
- Known limitations.
- Required follow-up actions.

### 13.7 Update evaluation requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-UPD-001 | An upstream update MUST be evaluated before replacing the approved baseline. | R |
| UPM-UPD-002 | Current and proposed immutable revisions MUST be recorded. | R |
| UPM-UPD-003 | Relevant source and release changes MUST be assessed. | R |
| UPM-UPD-004 | License and provenance reassessment MUST be completed. | R |
| UPM-UPD-005 | Security and project-health impact MUST be assessed. | R |
| UPM-UPD-006 | Existing KRITVA customizations MUST be reassessed. | R |
| UPM-UPD-007 | Integration readiness MUST be reassessed for affected requirements. | R |
| UPM-UPD-008 | Required verification MUST be completed before update acceptance. | R |
| UPM-UPD-009 | Adoption and customization reassessment outcomes MUST be recorded. | R |
| UPM-UPD-010 | The update decision MUST be explicit and traceable. | R |
| UPM-UPD-011 | A new upstream revision MUST NOT automatically replace the current approved baseline. | R |
| UPM-UPD-012 | The previous approved baseline MUST remain identifiable after an update. | R |

## 14. Customization and Rebase Maintenance

### 14.1 Customization inventory

Before an upstream update is accepted, the maintainer MUST identify all customizations that apply to the current baseline.

The inventory SHOULD include:

- Wrappers and adapters.
- Patches and patch series.
- Parameter configurations.
- Fork-specific changes.
- Generated source changes.
- Verification wrappers.
- KRITVA-specific scripts.
- Documentation adaptations.
- Approved deviations and waivers.

Each customization MUST be associated with its recorded base revision.

### 14.2 Wrapper and adapter reassessment

A wrapper may remain unchanged at source level while becoming incompatible with an updated upstream component.

The maintainer MUST assess:

- Port changes.
- Interface protocol changes.
- Parameter changes.
- Clock and reset changes.
- Error and status behavior.
- Timing assumptions.
- Register and control interface behavior.
- Data interface behavior.
- Verification assumptions.

An unchanged wrapper MUST NOT be assumed compatible without assessment.

### 14.3 Patch reassessment

For patch-based customizations:

- The patch series MUST be compared against the new upstream revision.
- Patches MUST be reapplied or rebased in a controlled manner.
- Conflicts MUST be reviewed.
- A patch MUST NOT be silently dropped.
- Obsolete patches SHOULD be retired with rationale.
- Modified patch behavior MUST be re-verified.
- The resulting customized revision MUST be recorded.

A patch that applies without conflict is not necessarily semantically correct against the new upstream source.

### 14.4 Fork reassessment

A KRITVA-maintained fork MUST retain its upstream identity and synchronization history.

The maintainer MUST assess:

- Upstream changes since the previous synchronization.
- Local modifications.
- Merge or rebase conflicts.
- License changes.
- Security fixes.
- Functional differences.
- Dependency changes.
- Verification impact.
- Long-term maintenance cost.

A fork that cannot reasonably track upstream changes SHOULD be considered for replacement, retirement, or a documented long-term maintenance decision.

### 14.5 Parameter configuration reassessment

The maintainer MUST verify:

- Parameter existence.
- Parameter names and types.
- Supported ranges.
- Default values.
- Dependencies.
- Deprecated parameters.
- Removed parameters.
- Changes in parameter behavior.
- Configuration-specific verification.

A configuration MUST NOT silently depend on a parameter that has been removed or changed incompatibly.

### 14.6 Rebase requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-CUS-001 | Existing customizations MUST be inventoried before an upstream update. | R |
| UPM-CUS-002 | Wrapper compatibility MUST be reassessed when upstream interfaces or behavior change. | R |
| UPM-CUS-003 | Patch series MUST be reapplied or rebased in a controlled manner. | R |
| UPM-CUS-004 | Patch conflicts MUST be reviewed and recorded. | R |
| UPM-CUS-005 | Patches MUST NOT be silently dropped during rebase. | R |
| UPM-CUS-006 | Fork synchronization MUST preserve upstream identity and local change history. | R |
| UPM-CUS-007 | Parameter configurations MUST be validated against the new source revision. | R |
| UPM-CUS-008 | Customization changes resulting from an update MUST be re-verified. | R |
| UPM-CUS-009 | The customized revision and update outcome MUST be recorded. | R |

## 15. Technical Integration Reassessment

### 15.1 Common IP requirements

An upstream update MUST be assessed against the applicable KRITVA IP Standard.

The assessment SHOULD focus on requirements affected by the upstream change.

A complete re-assessment MAY be required when the update changes the component's architecture, interfaces, reset behavior, or technology dependencies.

### 15.2 Control and register interface

The common KRITVA IP baseline identifies APB as the primary control/register interface.

The APB revision and profile remain TBD pending owner approval.

An upstream change affecting control or register access MUST be assessed for:

- APB compatibility.
- Register map changes.
- Read and write behavior.
- Address and data mapping.
- Error response behavior.
- Reset values.
- Register side effects.
- Interface timing.
- Bridge requirements.

AXI4 MAY be used for data or high-bandwidth interfaces where justified.

AXI4-Lite, AHB-Lite, and Wishbone MAY be used through documented bridges.

An upstream change MUST NOT silently introduce a different primary control/register interface.

### 15.3 Clock and reset

An upstream update affecting clocks or resets MUST be assessed for:

- Clock domain assumptions.
- Clock-domain crossing behavior.
- Reset domain behavior.
- Reset assertion and deassertion.
- Reset synchronization.
- Reset recovery and removal.
- Interactions between interfaces.

The common reset baseline is active-low.

Reset naming follows:

`rst_<domain>_n_i`

Active-high reset usage requires an approved waiver with documented rationale.

Reset synchronizers MUST be sourced from the approved RTL library manifest. An upstream update MUST NOT introduce an independent reset synchronizer implementation where the approved library provides the required implementation.

### 15.4 Technology boundary

The approved RTL library manifest is the sole technology boundary for technology-dependent RTL dependencies.

Every upstream update MUST be assessed for new or changed technology dependencies.

The assessment MUST identify:

- New cell or primitive dependencies.
- Changed technology-dependent modules.
- New clock-gating dependencies.
- New reset synchronizer dependencies.
- New memory or FIFO dependencies.
- Direct foundry-cell references.
- Vendor-specific implementation assumptions.

Unapproved technology-dependent RTL MUST NOT be adopted.

### 15.5 Verification and evidence

KVRF/cocotb is the default reference verification flow for new KRITVA-developed IP at L2+.

Equivalent flows MAY be used if they produce evidence records conforming to the KVRF schema.

Upstream IP MAY retain its native testbench and verification methodology, with a wrapper-level KVRF test for KRITVA integration.

An upstream update MUST trigger verification appropriate to its change impact.

### 15.6 Integration requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-INT-001 | Upstream updates MUST be assessed against applicable KRITVA IP requirements. | R |
| UPM-INT-002 | APB-primary control/register compatibility MUST be assessed when affected. | R |
| UPM-INT-003 | Active-low reset conventions and naming MUST be assessed when affected. | R |
| UPM-INT-004 | Reset synchronizer dependencies MUST comply with the approved RTL library manifest. | R |
| UPM-INT-005 | Technology dependencies MUST remain within the approved RTL library manifest. | R |
| UPM-INT-006 | Relevant port naming and sequential logic requirements MUST be reassessed. | R |
| UPM-INT-007 | Required KVRF-schema evidence MUST be produced for the updated integration. | R |
| UPM-INT-008 | UNKNOWN integration results MUST NOT be treated as PASS. | R |

## 16. Project Health and Abandoned Upstream Handling

### 16.1 Project-health indicators

Project health SHOULD be assessed using several indicators rather than a single activity measure.

Relevant indicators include:

- Recent upstream releases.
- Commit activity.
- Maintainer participation.
- Issue response.
- Pull request review.
- Security response.
- Documentation updates.
- Contributor continuity.
- Build and test infrastructure availability.
- Dependency health.
- Public maintenance announcements.
- Repository archival status.

The assessment SHOULD distinguish:

- Low activity with stable maintenance.
- Reduced maintenance capacity.
- Unclear project ownership.
- Explicitly discontinued development.
- Archived or read-only status.
- Abandoned or inaccessible source.

### 16.2 Maintenance status

The following statuses SHOULD be used in the upstream watch register.

| Status | Meaning |
|---|---|
| ACTIVE | Upstream project is maintained and no material continuity concern is identified. |
| REDUCED_ACTIVITY | Maintenance activity has decreased and requires monitoring. |
| MAINTENANCE_ONLY | Upstream project is primarily accepting maintenance and security changes. |
| UNCERTAIN | Project status or maintenance continuity cannot be established. |
| ARCHIVED | Upstream repository is explicitly archived or read-only. |
| ABANDONED | Evidence indicates upstream maintenance has ceased. |
| DISCONTINUED | Upstream project or component is explicitly discontinued. |
| REPLACED_UPSTREAM | Upstream project identifies a successor or replacement. |

The status MUST be supported by recorded evidence.

### 16.3 Reduced activity

Reduced activity does not automatically require replacement.

The maintainer SHOULD assess:

- Whether the current component remains functional.
- Whether the component has known unresolved defects.
- Whether security fixes are still available.
- Whether dependencies remain maintained.
- Whether KRITVA can maintain required fixes.
- Whether a replacement is available.
- Whether the component remains suitable for the intended lifecycle.

A REDUCED_ACTIVITY or UNCERTAIN status SHOULD trigger a documented maintenance-risk review.

### 16.4 Archived upstream

An archived project may remain technically usable under its existing license and source revision.

Archival MUST trigger a maintenance review.

The review MUST assess:

- Whether the archived source remains accessible.
- Whether the adopted revision is reproducible.
- Whether known defects remain.
- Whether security maintenance is available.
- Whether dependencies remain usable.
- Whether KRITVA can maintain a fork.
- Whether replacement is necessary.
- Whether continued use is acceptable for the intended scope.

An archived project MUST NOT be treated as actively maintained.

### 16.5 Abandoned upstream

When a project is assessed as abandoned:

1. Record the evidence supporting the assessment.
2. Identify affected KRITVA components.
3. Assess current functional and security risk.
4. Determine whether continued use is acceptable.
5. Assess the feasibility of KRITVA maintenance.
6. Identify alternative upstream projects, if available.
7. Consider a controlled fork.
8. Consider replacement or retirement.
9. Record the owner decision.
10. Define the maintenance plan and reassessment condition.

A decision to maintain an abandoned component MUST identify a responsible maintenance owner and the scope of that responsibility.

### 16.6 Fork decision

A KRITVA-maintained fork MAY be considered when:

- The component remains technically suitable.
- The source and license permit the required maintenance.
- A replacement is not justified or available.
- Required security and defect fixes can be maintained.
- The maintenance cost is acceptable.
- A qualified maintainer is available.
- The fork can preserve upstream provenance and notices.

A fork MUST NOT be treated as a continuation of upstream maintenance.

KRITVA MUST clearly distinguish its own maintenance status from that of the original upstream project.

### 16.7 Project-health requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-HLT-001 | Material project-health concerns MUST be recorded. | R |
| UPM-HLT-002 | An archived upstream project MUST trigger a maintenance review. | R |
| UPM-HLT-003 | An abandoned upstream project MUST have an explicit continued-use, fork, replacement, or retirement decision. | R |
| UPM-HLT-004 | A KRITVA-maintained fork MUST have an identified maintenance owner. | R |
| UPM-HLT-005 | A KRITVA fork MUST NOT be represented as actively maintained by the upstream project. | R |
| UPM-HLT-006 | Project-health status MUST be supported by evidence. | R |
| UPM-HLT-007 | Continued use of abandoned or archived IP MUST have a documented maintenance rationale. | R |

## 17. Deprecation and Replacement

### 17.1 Deprecation principles

Deprecation indicates that a component is no longer preferred for new adoption or is planned for eventual retirement.

Deprecation does not automatically mean that the component is unusable.

A deprecated component MUST have a documented reason and an identified maintenance disposition.

Possible reasons include:

- Upstream discontinuation.
- Unacceptable maintenance risk.
- Security concerns.
- License incompatibility.
- Functional limitations.
- Obsolete interfaces.
- Better-supported alternatives.
- Excessive customization burden.
- Integration incompatibility.
- Replacement by another component.

### 17.2 Deprecation statuses

| Status | Meaning |
|---|---|
| NOT_DEPRECATED | No deprecation decision is active. |
| DEPRECATION_PROPOSED | Deprecation has been proposed but not approved. |
| DEPRECATED | Approved for deprecation; new adoption is restricted. |
| MIGRATION_IN_PROGRESS | Consumers are being migrated to a replacement. |
| RETIRED | Component is no longer approved for new or continuing use within the defined scope. |
| REPLACED | A replacement component has been adopted for the relevant scope. |

A DEPRECATION_PROPOSED status MUST NOT be represented as an approved deprecation decision.

### 17.3 Deprecation assessment

The assessment SHOULD identify:

- Reason for deprecation.
- Affected components and repositories.
- Existing consumers.
- Current adopted revision.
- Current customization status.
- Security and license status.
- Known defects.
- Replacement candidates.
- Migration complexity.
- Verification requirements.
- Required coexistence period.
- Retirement conditions.
- Owner and approval.

### 17.4 Replacement selection

A replacement MUST undergo the applicable adoption process.

The replacement assessment MUST consider:

- Functional equivalence.
- Interface compatibility.
- License compatibility.
- Security posture.
- Project health.
- Verification maturity.
- Customization requirements.
- Technology-boundary compliance.
- Integration effort.
- Maintenance sustainability.

A replacement MUST NOT be approved solely because the previous component has been deprecated.

### 17.5 Migration

Migration from a deprecated component MUST be controlled.

The migration record SHOULD identify:

- Source component.
- Replacement component.
- Existing consumers.
- Interface differences.
- Configuration differences.
- Customization changes.
- License and notice impact.
- Verification evidence.
- Release impact.
- Migration completion criteria.

Where both old and replacement components coexist, their approval scopes MUST be distinguishable.

### 17.6 Retirement

Retirement MUST include:

- A documented retirement decision.
- Affected consumers.
- Replacement or removal plan.
- Final approved source revision.
- Final customization and verification records.
- License and notice disposition.
- Archival location.
- Closure evidence.

Retired records MUST remain traceable.

Retirement MUST NOT erase historical provenance, adoption decisions, or verification evidence.

### 17.7 Deprecation and replacement requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-DEP-001 | Deprecation MUST have a documented rationale and owner decision. | R |
| UPM-DEP-002 | A deprecated component MUST have a defined adoption and maintenance restriction. | R |
| UPM-DEP-003 | A replacement MUST undergo the applicable adoption process. | R |
| UPM-DEP-004 | Replacement selection MUST assess license, security, technical, and maintenance suitability. | R |
| UPM-DEP-005 | Migration MUST be verified against the intended use. | R |
| UPM-DEP-006 | Retirement MUST preserve historical provenance and decision records. | R |
| UPM-DEP-007 | A retired component MUST NOT be used for new approved integration within its retired scope. | R |
| UPM-DEP-008 | Deprecation and retirement status MUST be reflected in the upstream watch register. | R |

## 18. Maintenance of KRITVA-Authored Components

### 18.1 Applicability

Some KRITVA components may be maintained in public repositories while depending on external projects, specifications, generators, or tools.

For KRITVA-authored components, upstream maintenance may relate to:

- External libraries.
- Reference implementations.
- Tool dependencies.
- Protocol specifications.
- Generated-source inputs.
- Verification frameworks.
- Vendor-provided collateral.

The same monitoring and update controls apply where an external dependency materially affects the component.

### 18.2 KRITVA-owned source

KRITVA-authored files MUST use the approved copyright holder wording:

**Kritva Robotics**

This wording applies only to KRITVA-authored material.

Original upstream copyright and license notices MUST be preserved in adopted or modified third-party material.

A KRITVA-maintained fork MUST retain the original upstream identity and required notices.

### 18.3 KRITVA maintenance requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-KRV-001 | External dependencies of KRITVA-authored components MUST be identified where they materially affect maintenance. | R |
| UPM-KRV-002 | KRITVA-authored changes MUST remain distinguishable from upstream source. | R |
| UPM-KRV-003 | KRITVA-authored files MUST use the copyright holder wording `Kritva Robotics`. | R |
| UPM-KRV-004 | Upstream copyright and license notices MUST remain intact. | R |
| UPM-KRV-005 | KRITVA-maintained forks MUST retain source provenance and maintenance records. | R |

## 19. Integration and Technology Boundary

### 19.1 Common IP integration baseline

Upstream changes MUST be assessed against the applicable KRITVA IP Standard and SoC profile.

The assessment MUST consider whether the update changes any established integration assumptions.

### 19.2 Control and register interface

The common KRITVA IP baseline identifies APB as the primary control/register interface.

The APB revision and profile remain TBD pending owner approval.

Upstream changes affecting control or register behavior MUST be assessed for compatibility with this baseline.

AXI4 MAY be used for data or high-bandwidth interfaces where justified.

AXI4-Lite, AHB-Lite, and Wishbone MAY be used through documented bridges.

### 19.3 Reset and clock conventions

The common reset baseline is active-low.

Reset naming follows:

`rst_<domain>_n_i`

Active-high reset usage requires an approved waiver with documented rationale.

Reset synchronizers MUST be sourced from the approved RTL library manifest.

Any upstream change to clock or reset behavior MUST be reviewed for compatibility with the applicable integration requirements.

### 19.4 Technology boundary

The approved RTL library manifest is the sole technology boundary for technology-dependent RTL dependencies.

Upstream changes MUST NOT introduce unapproved technology-specific cells, direct foundry-cell dependencies, or unsupported implementation primitives.

A technology-boundary change requires an explicit owner decision and applicable standard update.

### 19.5 Integration requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-TECH-001 | Upstream changes MUST be assessed against the applicable KRITVA IP integration baseline. | R |
| UPM-TECH-002 | APB-primary control/register compatibility MUST be assessed when affected. | R |
| UPM-TECH-003 | Active-low reset and reset naming conventions MUST be assessed when affected. | R |
| UPM-TECH-004 | Reset synchronizers MUST use the approved RTL library manifest. | R |
| UPM-TECH-005 | Technology-dependent RTL MUST remain within the approved RTL library manifest. | R |
| UPM-TECH-006 | Unapproved technology-specific dependencies MUST NOT be adopted. | R |
| UPM-TECH-007 | Relevant clock, reset, interface, and parameter changes MUST be recorded. | R |

## 20. Verification and Evidence

### 20.1 Verification policy

Upstream maintenance MUST preserve evidence that the currently adopted or proposed revision is suitable for its intended KRITVA use.

KVRF/cocotb is the default reference verification flow for new KRITVA-developed IP at L2+.

Equivalent verification flows MAY be used if they emit evidence records conforming to the KVRF schema.

Upstream IP MAY retain its native testbench and verification methodology. Its KRITVA integration MUST include a wrapper-level KVRF test producing KVRF-schema evidence.

An upstream update MUST trigger re-verification appropriate to the changes and their impact.

### 20.2 Verification scope

Re-verification SHOULD consider:

- Functional changes.
- Interface changes.
- Parameter changes.
- Reset and clock changes.
- Security fixes.
- Build and dependency changes.
- Wrapper and adapter compatibility.
- Patch and fork changes.
- Integration behavior.
- Relevant regression coverage.

A change that is documented as non-functional MAY require a reduced verification scope, but the rationale MUST be recorded.

### 20.3 Evidence requirements

Verification evidence SHOULD identify:

- Component ID.
- Upstream revision.
- Customized revision, if applicable.
- Proposed revision.
- Verification methodology.
- KVRF evidence record references.
- Test identifiers.
- Configuration and parameters.
- Tool names and versions.
- Execution environment.
- Results.
- Logs and reports.
- Known limitations.
- Reviewer and review date.

Tool versions that have not been independently established MUST be marked UNVERIFIED.

### 20.4 Verification requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-VER-001 | Material upstream changes MUST trigger impact-based re-verification. | R |
| UPM-VER-002 | Verification MUST identify the exact source revision under test. | R |
| UPM-VER-003 | KVRF-schema evidence MUST be produced according to the applicable verification policy. | R |
| UPM-VER-004 | Equivalent verification flows MUST produce KVRF-schema evidence records. | R |
| UPM-VER-005 | Upstream IP MAY retain its native testbench with a wrapper-level KVRF test for KRITVA integration. | R |
| UPM-VER-006 | Verification evidence MUST distinguish PASS, FAIL, and INCONCLUSIVE outcomes. | R |
| UPM-VER-007 | Tool versions MUST be marked UNVERIFIED when not independently established. | R |
| UPM-VER-008 | Verification evidence MUST be retained or referenced by the update record. | R |
| UPM-VER-009 | A failed mandatory verification result MUST prevent update acceptance until resolved or validly waived. | R |

## 21. Maintenance Register and Record Formats

### 21.1 Record model

The upstream maintenance record set consists of:

| Record | Purpose |
|---|---|
| Upstream watch register | Inventory of monitored upstream dependencies and current baselines. |
| Upstream event record | Evidence of a release, commit, advisory, license, or project-health event. |
| Triage record | Severity, applicability, impact, and initial disposition. |
| Security assessment | Vulnerability applicability and response. |
| License reassessment | License and redistribution impact. |
| Update evaluation | Comparison of current and proposed revisions. |
| Customization reassessment | Wrapper, patch, configuration, and fork impact. |
| Verification record | Re-verification results and evidence. |
| Adoption reassessment | RETAIN, UPDATE, REVIEW, or REVOKE outcome. |
| Customization reassessment | RETAIN, UPDATE, REVIEW, or REVOKE outcome. |
| Deprecation record | Deprecation rationale and scope. |
| Replacement record | Replacement assessment and migration. |
| Retirement record | Retirement decision and closure evidence. |

The watch register is an index. Detailed assessments MUST be maintained in their appropriate records.

### 21.2 Upstream watch register schema

The following fields define the minimum upstream watch register.

| Field | Type | Required | Description |
|---|---|---|---|
| component_id | string | Yes | Stable KRITVA component identifier. |
| component_name | string | Yes | Dependency name. |
| source_category | string | Yes | Source category. |
| upstream_project | string | Yes | Original upstream project or provider. |
| upstream_repository | string | Conditional | Authoritative upstream location. |
| upstream_release | string | No | Current upstream release identifier. |
| upstream_commit | string | Yes | Immutable monitored upstream revision. |
| upstream_branch | string | No | Mutable monitoring reference, if used. |
| source_checksum | string | No | Source snapshot integrity reference. |
| license | string | Yes | Current assessed license identifier or status. |
| license_status | string | Yes | Current license assessment state. |
| consuming_repositories | array | Yes | KRITVA repositories or components using the dependency. |
| dependency_type | string | Yes | Direct, transitive, build, verification, or other relationship. |
| adoption_status | string | Yes | Current adoption disposition. |
| maintenance_status | string | Yes | ACTIVE, REDUCED_ACTIVITY, MAINTENANCE_ONLY, UNCERTAIN, ARCHIVED, ABANDONED, DISCONTINUED, or REPLACED_UPSTREAM. |
| criticality | string | Yes | Owner-approved dependency criticality. |
| severity | string | Yes | Current highest unresolved event severity. |
| last_event_id | string | No | Latest material event reference. |
| last_review_date | string | Yes | Date of last completed review. |
| next_review | string | Yes | Next review date or trigger condition. |
| monitoring_method | string | Yes | Manual, automated, notification, or combined method. |
| maintenance_owner | string | Yes | Responsible maintainer. |
| customization_refs | array | No | Related customization identifiers. |
| current_kritva_revision | string | No | Current KRITVA customized revision. |
| last_update_decision | string | No | Latest update decision. |
| deprecation_status | string | Yes | Current deprecation state. |
| replacement_component_id | string | No | Approved or proposed replacement identifier. |
| evidence_refs | array | No | Assessment and evidence references. |
| notes | string | No | Additional non-sensitive information. |

Fields marked Conditional MUST be present where applicable.

Unknown values MUST be marked UNKNOWN or TBD rather than inferred.

### 21.3 Example upstream watch register

The following example is illustrative only. It does not identify an actual KRITVA dependency or indicate approval.

~~~yaml
schema_version: "0.1.0"
register_id: "UPM-WATCH-EXAMPLE"

owner: "Dinesh Annayya"
classification: "PUBLIC"

dependencies:
  - component_id: "IP-EXAMPLE-001"
    component_name: "Example Upstream IP"

    source_category: "THIRD_PARTY_OPEN_SOURCE"

    upstream_project: "Example Upstream Project"
    upstream_repository: "UNKNOWN"
    upstream_release: "UNKNOWN"
    upstream_commit: "UNKNOWN"
    upstream_branch: "main"
    source_checksum: "UNKNOWN"

    license: "UNKNOWN"
    license_status: "NOT_ASSESSED"

    consuming_repositories:
      - "EXAMPLE_KRITVA_REPOSITORY"

    dependency_type: "DIRECT"

    adoption_status: "REVIEW"

    maintenance_status: "UNCERTAIN"
    criticality: "TBD"
    severity: "S4"

    last_event_id: null
    last_review_date: "2026-11-12"
    next_review: "OWNER_DECISION"

    monitoring_method: "MANUAL"

    maintenance_owner: "TBD"

    customization_refs: []
    current_kritva_revision: "UNKNOWN"

    last_update_decision: null

    deprecation_status: "NOT_DEPRECATED"
    replacement_component_id: null

    evidence_refs: []

    notes: >
      Illustrative record only. Source provenance, license,
      maintenance status, and adoption are not verified.
~~~

### 21.4 Upstream event record schema

An upstream event record SHOULD contain:

| Field | Description |
|---|---|
| event_id | Stable event identifier. |
| component_id | Affected dependency. |
| event_type | RELEASE, COMMIT, SECURITY, LICENSE, DEFECT, PROJECT_HEALTH, or other type. |
| upstream_event_date | Date of the upstream event. |
| detected_date | Date KRITVA detected the event. |
| source_reference | Authoritative upstream or advisory reference. |
| affected_revision | Upstream revision affected by the event. |
| current_baseline | Current KRITVA upstream baseline. |
| proposed_revision | Proposed revision, where applicable. |
| severity | S0 through S4. |
| applicability | Assessment of relevance to the KRITVA use case. |
| triage_outcome | Recorded triage disposition. |
| assigned_owner | Responsible reviewer or maintainer. |
| required_action | Action required to resolve or disposition the event. |
| decision_reference | Related owner or adoption decision. |
| closure_date | Date the event was closed. |
| closure_evidence | Evidence supporting closure. |

### 21.5 Record integrity

All maintenance records MUST:

- Identify the affected component.
- Preserve immutable source references.
- Distinguish upstream observations from KRITVA decisions.
- Preserve historical event and decision information.
- Identify the responsible owner.
- Link to relevant assessment evidence.
- Avoid implying approval through record presence.
- Preserve public/private classification.

A correction to an event record MUST retain enough history to explain the correction.

## 22. Maintenance Status and Decision Reporting

### 22.1 Component maintenance status

Each monitored component SHOULD have an overall maintenance status.

| Status | Meaning |
|---|---|
| MONITORING | Dependency is being monitored and no active blocking issue is known. |
| UNDER_REVIEW | A material event or maintenance concern is under assessment. |
| UPDATE_PENDING | An update has been selected but not yet accepted. |
| REMEDIATION | Security, technical, or license remediation is in progress. |
| MAINTAINED | Current approved baseline and maintenance evidence are up to date. |
| DEPRECATED | Component is deprecated for the defined scope. |
| REPLACEMENT_IN_PROGRESS | A replacement is being adopted or migrated. |
| RETIRED | Component is retired within the defined scope. |
| BLOCKED | A material issue prevents continued approved use or update. |

The maintenance status is distinct from the adoption disposition.

For example, a component may have adoption status ALLOW while maintenance status is UNDER_REVIEW because a new upstream event is being evaluated.

### 22.2 Status reporting

Maintenance reporting SHOULD summarize:

- Number of monitored dependencies.
- Dependencies with overdue reviews.
- Open S0 and S1 events.
- Open license reassessments.
- Dependencies with uncertain or abandoned upstream status.
- Pending upstream updates.
- Pending customization rebases.
- Pending verification.
- Deprecated dependencies.
- Replacement activities.
- Retired dependencies.
- Open owner decisions.

Reports MUST distinguish actual measured status from estimates or incomplete records.

### 22.3 Status requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-STS-001 | Adoption status and maintenance status MUST remain distinct. | R |
| UPM-STS-002 | A component with a blocking event MUST reflect that condition in its maintenance status. | R |
| UPM-STS-003 | Status reports MUST distinguish verified results from unknown information. | R |
| UPM-STS-004 | Open critical events MUST remain visible until formally dispositioned. | R |
| UPM-STS-005 | Retired components MUST retain their historical maintenance status and records. | R |

## 23. Public and Private Boundary

### 23.1 Public maintenance information

Public KRITVA repositories MAY contain:

- Public upstream project names.
- Public repository locations.
- Public immutable revision identifiers.
- Public release references.
- Public license identifiers and notices.
- Public security advisory references.
- Public maintenance status.
- Publicly approved update decisions.
- Public verification evidence.
- Public deprecation and replacement records.
- Public customization references.

Public disclosure MUST comply with applicable licenses and security disclosure requirements.

### 23.2 Restricted information

The following information MUST NOT be published without authorization:

- Confidential vendor collateral.
- Proprietary source or restricted implementation details.
- Non-public commercial terms.
- Private supplier correspondence.
- Credentials and access tokens.
- Confidential security investigations.
- Unreleased SoC architecture and implementation details.
- Private repository paths or internal review artifacts exposing unreleased implementation.
- Non-public product or customer information.
- Restricted verification data.

Public records MAY refer to private evidence through a non-sensitive identifier.

### 23.3 Copyright and attribution

KRITVA-authored files MUST use the copyright holder wording:

**Kritva Robotics**

Original upstream copyright and license notices MUST be preserved.

A KRITVA-maintained fork MUST clearly distinguish KRITVA-authored modifications from upstream material.

KRITVA copyright wording MUST NOT replace or obscure third-party ownership and attribution.

### 23.4 Public/private requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-PUB-001 | Public maintenance records MUST contain only information cleared for public disclosure. | R |
| UPM-PUB-002 | Restricted vendor or proprietary material MUST NOT be copied into public records without authorization. | R |
| UPM-PUB-003 | Public source and revision references MUST NOT expose confidential credentials. | R |
| UPM-PUB-004 | Unreleased SoC implementation details MUST remain outside public maintenance records. | R |
| UPM-PUB-005 | KRITVA-authored files MUST use the copyright holder wording `Kritva Robotics`. | R |
| UPM-PUB-006 | Upstream copyright and license notices MUST remain intact. | R |
| UPM-PUB-007 | Private evidence MAY be referenced through a non-sensitive identifier. | R |

## 24. Enforcement and Assessment

### 24.1 Enforcement classes

This policy uses the enforcement classes aligned with `KRITVA_IP_STANDARD.md` and `KNX-RTL-STD-001`.

| Class | Name | Meaning |
|---|---|---|
| A | Automated | A requirement that can be checked by an automated script, tool, or CI process. |
| T | Tool-assisted | Tools provide evidence, but human interpretation or review remains necessary. |
| R | Review only | Human review, judgment, or explicit approval is required. |

The enforcement class describes the assessment method. It does not change the normative force of a requirement.

### 24.2 Assessment outcomes

Maintenance assessments MUST use explicit outcomes appropriate to the check:

- PASS
- FAIL
- WAIVED
- NOT APPLICABLE
- UNKNOWN

UNKNOWN MUST NOT be treated as PASS.

A failed mandatory requirement MUST prevent update acceptance or continued approved use where applicable, unless a valid and permissible waiver or disposition applies.

### 24.3 Tool versions

Tools used for upstream monitoring, source comparison, security scanning, license scanning, build, and verification SHOULD be recorded with their versions and relevant configuration.

**Tool versions for this document are UNVERIFIED.**

No specific tool version or toolchain configuration is approved by this document.

### 24.4 Enforcement requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| UPM-ENF-001 | Every material maintenance event MUST have an identifiable assessment outcome. | R |
| UPM-ENF-002 | Enforcement classes MUST use A/T/R consistently with the KRITVA IP Standard. | R |
| UPM-ENF-003 | UNKNOWN MUST NOT be treated as PASS. | R |
| UPM-ENF-004 | Automated and tool-assisted results MUST retain sufficient evidence for review. | R |
| UPM-ENF-005 | Tool versions MUST be marked UNVERIFIED when not independently established. | R |
| UPM-ENF-006 | Automated notifications MUST NOT replace an explicit maintenance decision. | R |

## 25. Document Maintenance

This document is maintained as a public KRITVA policy.

Changes MUST be reviewed for impact on:

- Upstream monitoring.
- Watch register and event records.
- Severity and triage.
- Security response.
- License reassessment.
- Update evaluation.
- Customization and rebase handling.
- Project-health and abandonment procedures.
- Deprecation and replacement.
- Verification evidence.
- Public/private boundaries.
- Related KRITVA standards and policies.

Changes MUST NOT silently invalidate historical maintenance or adoption decisions.

### 25.1 Versioning

| Version change | Meaning |
|---|---|
| Major | Incompatible changes to maintenance lifecycle, decision outcomes, or mandatory controls. |
| Minor | New monitoring categories, requirements, or substantive additions that preserve the policy framework. |
| Patch | Editorial corrections, clarifications, and non-substantive changes. |

### 25.2 Approval status

The current document status is DRAFT.

Publication of this document does not approve any specific upstream dependency, update, security response timeline, fork, deprecation, or replacement.

---

## 26. Open Items

The following items require explicit owner decisions. They are not approved assumptions.

Owner for all items: **Dinesh Annayya**.

| ID | Open item | Decision required | Owner | Status |
|---|---|---|---|---|
| UPM-OI-001 | Monitoring cadence | Define default monitoring intervals by dependency criticality and risk. | Dinesh Annayya | OPEN |
| UPM-OI-002 | Criticality classification | Approve the common dependency criticality levels and assignment criteria. | Dinesh Annayya | OPEN |
| UPM-OI-003 | Security response targets | Approve initial triage, escalation, mitigation, and disposition targets for S0-S4. | Dinesh Annayya | OPEN |
| UPM-OI-004 | Security escalation authority | Define the escalation path and approval authority for critical security events. | Dinesh Annayya | OPEN |
| UPM-OI-005 | Monitoring automation | Select approved sources and automation methods for upstream release and commit monitoring. | Dinesh Annayya | OPEN |
| UPM-OI-006 | Security advisory sources | Approve the authoritative security advisory sources for monitored dependencies. | Dinesh Annayya | OPEN |
| UPM-OI-007 | License monitoring method | Define the expected process for detecting and recording upstream license changes. | Dinesh Annayya | OPEN |
| UPM-OI-008 | Watch register schema | Approve the canonical machine-readable upstream watch register format. | Dinesh Annayya | OPEN |
| UPM-OI-009 | Watch register location | Decide whether watch records are maintained centrally, per repository, or through a shared registry. | Dinesh Annayya | OPEN |
| UPM-OI-010 | Event identifier format | Approve a stable identifier format for upstream watch events. | Dinesh Annayya | OPEN |
| UPM-OI-011 | Project-health thresholds | Define objective indicators and thresholds for REDUCED_ACTIVITY, ABANDONED, and related statuses. | Dinesh Annayya | OPEN |
| UPM-OI-012 | Fork maintenance authority | Define the approval and maintenance ownership requirements for KRITVA-maintained forks. | Dinesh Annayya | OPEN |
| UPM-OI-013 | Deprecation authority | Confirm the authority required to deprecate or retire an adopted component. | Dinesh Annayya | OPEN |
| UPM-OI-014 | Replacement evaluation | Approve minimum replacement evaluation criteria and coexistence expectations. | Dinesh Annayya | OPEN |
| UPM-OI-015 | Reassessment cadence | Define periodic reassessment requirements for adopted dependencies beyond event-driven review. | Dinesh Annayya | OPEN |
| UPM-OI-016 | Evidence retention | Define retention and archival requirements for upstream watch, security, and update evidence. | Dinesh Annayya | OPEN |
| UPM-OI-017 | Toolchain baseline | Establish verified versions and configurations for monitoring, scanning, source comparison, and verification. Current tool versions remain UNVERIFIED. | Dinesh Annayya | OPEN |
| UPM-OI-018 | KVRF evidence schema versioning | Define the compatibility and migration policy for KVRF-schema evidence records. | Dinesh Annayya | OPEN |
| UPM-OI-019 | Public security disclosure | Define the approval process for publishing security event details and remediation summaries. | Dinesh Annayya | OPEN |
| UPM-OI-020 | APB revision and profile | Approve the APB revision and control/register interface profile for the common IP baseline. | Dinesh Annayya | OPEN |

## 27. References

1. `KRITVA_IP_STANDARD.md` — Common IP design and integration requirements.
2. `OPEN_SOURCE_IP_POLICY.md` — Third-party source, license, provenance, and redistribution policy.
3. `IP_ADOPTION_PROCESS.md` — IP discovery, evaluation, adoption, and reassessment process.
4. `IP_CUSTOMIZATION_POLICY.md` — Customization, patch, fork, re-verification, and rebase policy.
5. `KNX-RTL-STD-001` — Nexus SoC RTL design profile.
6. Applicable upstream project release notes, commit history, security advisories, and license records.
7. Applicable KVRF verification methodology and evidence schema.
8. Applicable KRITVA repository contribution and release procedures.

The references do not imply approval of any specific upstream project, component, revision, tool version, or security response.

---

## 28. Change History

| Version | Date | Status | Description |
|---|---|---|---|
| 0.1.0 | 2026-11-12 | DRAFT | Initial upstream maintenance policy covering monitoring, immutable watch records, triage, security response, license changes, update evaluation, project health, abandonment, deprecation, replacement, and maintenance records. |

---

**End of Document**