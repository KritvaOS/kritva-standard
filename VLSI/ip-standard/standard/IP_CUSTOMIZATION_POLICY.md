# KRITVA IP Customization Policy

| Field | Value |
|---|---|
| Document ID | KSTD-IPCUST-001 |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | Public |
| Owner | Dinesh Annayya |
| Applies to | KRITVA-developed and adopted third-party IP |
| Related standard | `KRITVA_IP_STANDARD.md` |
| Related policy | `OPEN_SOURCE_IP_POLICY.md` |
| Related process | `IP_ADOPTION_PROCESS.md` |
| Related SoC profile | `KNX-RTL-STD-001` |
| Last updated | 2026-11-13 |

---

## 1. Purpose

This document defines the policy for customizing IP used within the KRITVA ecosystem.

Customization may be required to adapt an IP component to KRITVA interfaces, configuration requirements, verification methodology, integration constraints, or product requirements.

Customization introduces risks to:

- Upstream provenance and traceability.
- License compliance.
- Functional correctness.
- Verification completeness.
- Maintainability.
- Future upstream updates.
- Reproducibility.
- Separation between upstream and KRITVA-owned material.

This policy establishes a controlled approach to selecting, recording, reviewing, verifying, and maintaining customizations.

The primary objectives are to:

1. Prefer integration techniques that preserve upstream source.
2. Minimize modifications to third-party IP.
3. Preserve a clear distinction between upstream and KRITVA-owned content.
4. Ensure every customization has a documented technical rationale.
5. Maintain traceability from a customized component to its upstream revision.
6. Require re-verification after customization.
7. Define controlled procedures for upstream updates and rebasing.
8. Ensure deviations and waivers are explicit and approved.
9. Maintain customization records that support independent review and future maintenance.

This document is a public policy baseline. It does not approve any particular IP customization, implementation, or SoC integration.

## 2. Scope

This policy applies to customization of:

- KRITVA-developed RTL IP.
- Adopted third-party RTL IP.
- Verification components and testbenches.
- Firmware and software associated with IP.
- IP integration wrappers and adapters.
- Generated IP source and collateral.
- Supporting scripts and build infrastructure.
- Documentation and interface definitions.
- IP configuration and parameter sets.

It applies to customizations made during initial adoption, integration, maintenance, defect correction, performance optimization, and upstream update activities.

This policy applies whether customization is maintained in:

- The original KRITVA IP repository.
- A controlled fork.
- A separate integration repository.
- A patch series.
- A wrapper or adapter repository.
- Another approved source-control location.

The exact repository organization is not prescribed by this document.

## 3. Relationship to Other KRITVA Documents

This policy supplements the following documents:

| Document | Responsibility |
|---|---|
| `KRITVA_IP_STANDARD.md` | Common IP design, interface, clock/reset, technology, verification, and integration baseline. |
| `OPEN_SOURCE_IP_POLICY.md` | Third-party source classification, license assessment, provenance, notices, adoption, and redistribution. |
| `IP_ADOPTION_PROCESS.md` | Discovery, evaluation, intake, assessment, adoption decisions, integration readiness, and adoption records. |
| `KNX-RTL-STD-001` | Nexus-specific RTL design profile. |

This policy does not replace the adoption process or the applicable design standard.

A customization MUST comply with the applicable KRITVA IP requirements and the applicable SoC profile.

Where two applicable requirements address the same subject, the stricter requirement governs within its scope.

## 4. Normative Language

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are normative terms.

The common KRITVA standards use RFC 2119 `MUST` terminology.

The `SHALL` terminology used by `KNX-RTL-STD-001` is equivalent in normative force to `MUST`.

A requirement expressed as MUST remains mandatory regardless of its enforcement class.

A deviation from a mandatory requirement requires an explicit approved waiver where a waiver is legally and technically permissible.

## 5. Customization Principles

| ID | Principle | Policy |
|---|---|---|
| CUST-PR-001 | Preserve upstream | Prefer customization methods that avoid changing upstream source. |
| CUST-PR-002 | Minimal modification | Make the smallest change necessary to satisfy the documented requirement. |
| CUST-PR-003 | Traceability | Every customization MUST be traceable to its source revision and rationale. |
| CUST-PR-004 | Separation | Upstream source and KRITVA-owned changes MUST remain distinguishable. |
| CUST-PR-005 | License compliance | Customization MUST comply with applicable license and contractual obligations. |
| CUST-PR-006 | Evidence | Customizations MUST be re-verified with evidence appropriate to the change. |
| CUST-PR-007 | Reproducibility | The customized result MUST be reproducible from recorded source and modification information. |
| CUST-PR-008 | Maintainability | Customizations SHOULD minimize long-term maintenance and upstream merge conflicts. |
| CUST-PR-009 | Controlled deviation | Deviations from applicable standards MUST be explicitly assessed and dispositioned. |
| CUST-PR-010 | Controlled update | Upstream updates MUST be reviewed and integrated through a controlled rebase or equivalent process. |
| CUST-PR-011 | Technology boundary | Technology-dependent RTL MUST use only the approved RTL library manifest as its technology boundary. |
| CUST-PR-012 | Verification compatibility | Verification evidence MUST follow the KVRF evidence requirements or an approved equivalent flow producing KVRF-schema records. |

## 6. Customization Categories

Every customization MUST be assigned one or more categories.

The category describes the nature of the change, not its approval status.

### 6.1 Category C1 — Wrapper or Adapter

A wrapper or adapter provides an integration layer around an existing IP component without directly changing its upstream implementation.

Examples include:

- Interface adaptation.
- Control/register interface bridging.
- Signal naming adaptation.
- Clock and reset interface adaptation.
- Parameter exposure or configuration mapping.
- Protocol conversion.
- Integration-level error or status mapping.
- Verification access and observation interfaces.

A wrapper SHOULD be preferred when the required behavior can be achieved without modifying the underlying IP.

A wrapper MUST NOT conceal an incompatibility that should instead be resolved through an explicit technical decision or waiver.

### 6.2 Category C2 — Patch

A patch modifies a limited portion of upstream source while preserving the upstream project structure and most of its implementation.

Examples include:

- Correcting an identified functional defect.
- Fixing a portability issue.
- Correcting a reset or interface inconsistency.
- Applying a narrowly scoped coding-standard adaptation.
- Correcting a parameter-handling defect.
- Applying a required compatibility change.

A patch MUST have:

- A clear technical rationale.
- A reference to the affected upstream revision.
- A description of the changed files.
- A reproducible patch or equivalent change record.
- Verification evidence.
- A plan for future upstream update handling.

A patch SHOULD be contributed upstream when appropriate and permitted, but upstream submission does not itself constitute acceptance or approval.

### 6.3 Category C3 — Parameter Configuration

Parameter configuration changes the behavior or implementation characteristics of an IP through its documented configuration interface without modifying its source code.

Examples include:

- Selecting supported feature parameters.
- Setting widths and depths.
- Selecting supported operating modes.
- Configuring interface options.
- Enabling or disabling documented capabilities.
- Selecting supported implementation variants.

Parameter configuration SHOULD use documented upstream parameters rather than source modification.

A configuration MUST identify the parameter values, supported ranges, dependencies, and verification evidence.

A parameter value outside the documented supported range MUST NOT be treated as a normal configuration.

### 6.4 Category C4 — Fork

A fork maintains a KRITVA-controlled copy or derivative of an upstream project with independently managed changes.

A fork may be required when:

- A substantial change cannot reasonably be maintained as a wrapper.
- Upstream maintenance is unavailable or unsuitable.
- A set of patches has become too extensive for reliable patch management.
- The upstream project is incompatible with the required integration model.
- A long-lived maintenance branch is required.
- A separate KRITVA development direction has been explicitly approved.

A fork introduces additional responsibilities:

- Maintaining upstream provenance.
- Tracking upstream changes.
- Maintaining license and notice obligations.
- Managing local patches.
- Re-verifying changes.
- Resolving upstream conflicts.
- Maintaining a clear change history.
- Assessing whether the fork remains justified.

A fork MUST NOT be created merely for convenience when a wrapper or limited patch is sufficient.

### 6.5 Category C5 — Generated or Derived Customization

Generated or derived customization covers source or collateral produced from:

- Configuration files.
- Register descriptions.
- Interface specifications.
- Code generators.
- Templates.
- Schema-driven tools.
- Other source-controlled inputs.

The record MUST identify the generator, inputs, relevant versions, and generation procedure where available.

Generated source MUST NOT be treated as upstream source unless its provenance establishes that relationship.

Generated output MUST be re-created and verified when relevant inputs or generators change.

### 6.6 Category assignment

A single customization may use more than one category.

For example, an integration may use a wrapper together with a small patch and a parameter configuration.

The customization register MUST identify all applicable categories and distinguish their individual changes.

### 6.7 Category requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-CAT-001 | Every customization MUST be assigned one or more customization categories. | R |
| CUST-CAT-002 | The customization category MUST describe the actual change method. | R |
| CUST-CAT-003 | A wrapper MUST be preferred when it satisfies the requirement without changing upstream source. | R |
| CUST-CAT-004 | A patch MUST be limited to the changes required for the approved purpose. | R |
| CUST-CAT-005 | Parameter configurations MUST use documented and supported parameters unless an explicit exception is approved. | R |
| CUST-CAT-006 | A fork MUST have a documented justification and maintenance owner. | R |
| CUST-CAT-007 | Generated customizations MUST identify their inputs and generation method. | R |
| CUST-CAT-008 | Multiple customization categories MUST be recorded separately where necessary for traceability. | R |

## 7. Preferred Customization Order

### 7.1 Default preference

The preferred customization order is:

1. Wrapper or adapter.
2. Patch.
3. Fork.

Parameter configuration SHOULD be used wherever documented configuration can satisfy the requirement without source modification.

For practical evaluation, the preferred decision sequence is:

1. Determine whether documented parameter configuration is sufficient.
2. If not, determine whether a wrapper or adapter is sufficient.
3. If not, determine whether a limited patch is sufficient.
4. If not, evaluate whether a controlled fork is justified.

The preference order is intended to minimize divergence from upstream source.

It does not mean that a wrapper is always technically superior or that a patch or fork is prohibited.

### 7.2 Decision criteria

| Criterion | Parameter configuration | Wrapper / adapter | Patch | Fork |
|---|---|---|---|---|
| Changes upstream source | No | No | Yes | Yes |
| Upstream divergence | None | None in wrapped source | Limited | Potentially substantial |
| Interface adaptation | Limited to supported options | Primary purpose | Possible | Possible |
| Defect correction | Only if configuration resolves defect | Only if defect can be safely contained externally | Suitable for narrow defects | Suitable for extensive changes |
| Upstream update complexity | Low | Usually low | Requires patch reapplication | Requires ongoing rebase or merge |
| Maintenance responsibility | Configuration and validation | Wrapper maintenance | Patch maintenance | Fork maintenance |
| Default preference | First when sufficient | First source-level adaptation choice | After wrapper assessment | Last resort |

### 7.3 Justification for a lower-preference category

When a patch is selected instead of a wrapper, the record SHOULD explain why a wrapper is insufficient.

When a fork is selected instead of a patch, the record MUST explain why a limited patch series is insufficient.

When multiple approaches are technically viable, the selection SHOULD consider:

- Functional correctness.
- Verification complexity.
- Upstream compatibility.
- Long-term maintenance.
- License implications.
- Performance impact.
- Integration complexity.
- Reproducibility.
- Security implications.

### 7.4 Preference requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-PREF-001 | Parameter configuration MUST be considered before source modification when documented parameters can satisfy the requirement. | R |
| CUST-PREF-002 | A wrapper or adapter MUST be considered before patching upstream source. | R |
| CUST-PREF-003 | A patch SHOULD be preferred over a fork when a limited patch is technically sufficient. | R |
| CUST-PREF-004 | A fork MUST include a documented justification. | R |
| CUST-PREF-005 | Deviations from the preferred customization order MUST have a recorded rationale. | R |

## 8. Customization Identification and Intake

### 8.1 Customization identity

Every approved customization MUST have a stable customization identifier.

The identifier MUST be unique within the applicable KRITVA record system.

The identifier MUST NOT be confused with:

- A common IP standard requirement ID.
- A Nexus RTL requirement ID.
- An upstream issue identifier.
- An upstream commit identifier.
- A verification test identifier.

A customization identifier MUST remain stable while the same logical customization is maintained.

A materially different customization MUST receive a separate identifier.

### 8.2 Customization intake

Before a source-level customization is implemented, an intake record SHOULD be created.

For urgent defect corrections, the record MAY be created during the correction process, but MUST be completed before the change is accepted into an approved baseline.

The intake record MUST identify:

- Affected IP component.
- Upstream or KRITVA source classification.
- Source revision.
- Intended customization category.
- Problem or requirement being addressed.
- Proposed implementation approach.
- Expected files and interfaces affected.
- Technical reviewer.
- Verification approach.
- License implications.
- Expected maintenance impact.
- Required waivers or owner decisions.

### 8.3 Customization requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-INT-001 | Every approved customization MUST have a stable identifier. | R |
| CUST-INT-002 | Every customization MUST identify the affected component and source revision. | R |
| CUST-INT-003 | The intended customization category MUST be recorded. | R |
| CUST-INT-004 | The technical reason for customization MUST be documented. | R |
| CUST-INT-005 | Expected source, interface, and verification impact MUST be assessed. | R |
| CUST-INT-006 | Required license and waiver reviews MUST be identified before approval. | R |
| CUST-INT-007 | A customization MUST NOT be accepted into an approved baseline without a completed record. | R |

## 9. Customization Records

### 9.1 Required records

Every customization MUST have a record set appropriate to its category.

The record set MUST identify:

1. Customization identity.
2. Affected IP component.
3. Original source classification.
4. Original upstream revision, where applicable.
5. Customization category.
6. Technical rationale.
7. Requirements addressed.
8. Files and interfaces affected.
9. Change description.
10. License and provenance impact.
11. Verification impact.
12. Verification evidence.
13. Deviations and waivers.
14. Review and approval.
15. Upstream update and maintenance strategy.

### 9.2 Patch records

A patch record MUST contain:

- Patch identifier.
- Affected component identifier.
- Base upstream commit.
- Patch commit or patch-series reference.
- Files changed.
- Summary of changes.
- Reason for each logical change.
- Applicable requirement references.
- Known side effects.
- Verification evidence.
- Upstream contribution status, if applicable.
- Rebase considerations.

A patch MUST be reproducible against the recorded base revision.

A patch series MUST preserve the intended application order where order matters.

### 9.3 Wrapper and adapter records

A wrapper or adapter record SHOULD contain:

- Wrapped component identifier.
- Wrapped component revision.
- Wrapper source revision.
- Interface mapping.
- Clock and reset mapping.
- Parameter mapping.
- Protocol conversion behavior.
- Error and status mapping.
- Any buffering or timing assumptions.
- Verification evidence.
- Known limitations.

A wrapper MUST NOT be documented as part of the upstream implementation when it is KRITVA-authored.

### 9.4 Parameter configuration records

A parameter configuration record MUST contain:

- Component identifier and source revision.
- Parameter names.
- Selected values.
- Documented supported ranges.
- Dependencies between parameters.
- Configuration source or file.
- Expected behavior.
- Configuration-specific verification evidence.
- Any parameter deviation or unsupported value.

A configuration MUST be traceable to the exact component revision to which it applies.

### 9.5 Fork records

A fork record MUST contain:

- Original upstream project.
- Original upstream repository location.
- Fork repository location, where public disclosure is permitted.
- Fork creation revision.
- Base upstream revision.
- Reason for the fork.
- Maintainer and ownership.
- Local patch inventory.
- Upstream update strategy.
- License and notice obligations.
- Verification status.
- Maintenance and retirement considerations.

The fork MUST retain a clear relationship to the original upstream project.

### 9.6 Record requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-REC-001 | Every customization MUST have a corresponding record. | R |
| CUST-REC-002 | Records MUST identify the exact base source revision. | R |
| CUST-REC-003 | Source modifications MUST be traceable to a change or patch record. | R |
| CUST-REC-004 | Wrapper behavior and interface adaptation MUST be documented. | R |
| CUST-REC-005 | Parameter configurations MUST be recorded with their component revision. | R |
| CUST-REC-006 | Forks MUST preserve upstream identity and revision history. | R |
| CUST-REC-007 | Customization records MUST reference relevant verification evidence. | R |
| CUST-REC-008 | Material changes to a customization MUST update its record. | R |

## 10. Upstream and KRITVA Separation

### 10.1 Separation principle

Upstream source and KRITVA-owned customization MUST remain distinguishable.

A customized component MUST NOT be presented as an unmodified upstream release.

The separation MUST be maintained in:

- Source-control history.
- Repository organization.
- Copyright and license notices.
- Patch records.
- Documentation.
- Verification evidence.
- Release materials.
- Provenance records.

### 10.2 Upstream records

Upstream records include:

- Original source files.
- Original copyright statements.
- Original license files.
- Upstream documentation.
- Upstream issue references.
- Upstream commit history.
- Upstream release identifiers.
- Upstream testbenches and verification material.

Upstream records MUST be preserved in accordance with their license and applicable distribution requirements.

### 10.3 KRITVA records

KRITVA records include:

- KRITVA-authored wrappers and adapters.
- KRITVA patches.
- KRITVA parameter configurations.
- KRITVA fork changes.
- KRITVA integration documentation.
- KRITVA verification tests and evidence.
- KRITVA customization decisions.
- KRITVA waiver records.
- KRITVA maintenance and rebase records.

KRITVA-authored files MUST use the approved KRITVA copyright holder wording:

**Kritva Robotics**

This wording applies to KRITVA-authored files. It MUST NOT replace, remove, or alter original upstream copyright and license notices.

### 10.4 Mixed-origin files

A file containing material from multiple origins MUST preserve the applicable copyright and license information.

Where practical, mixed-origin material SHOULD be separated into distinct files or modules.

If separation is not practical, the file MUST clearly identify the applicable origin and notices.

A KRITVA modification MUST NOT imply that KRITVA owns upstream material.

### 10.5 Separation requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-SEP-001 | Upstream source MUST remain distinguishable from KRITVA-authored customization. | R |
| CUST-SEP-002 | KRITVA modifications MUST NOT be represented as upstream-authored changes. | R |
| CUST-SEP-003 | Original upstream copyright and license notices MUST be preserved. | R |
| CUST-SEP-004 | KRITVA-authored files MUST use the copyright holder wording `Kritva Robotics`. | R |
| CUST-SEP-005 | KRITVA copyright wording MUST NOT replace upstream copyright notices. | R |
| CUST-SEP-006 | Mixed-origin material MUST retain applicable attribution and license information. | R |
| CUST-SEP-007 | Verification evidence MUST identify whether it applies to upstream source, customized source, or both. | R |

## 11. Customization Design Rules

### 11.1 Minimal change

A customization MUST implement only the behavior necessary to satisfy its documented purpose.

Unrelated cleanup, refactoring, formatting changes, and speculative enhancements SHOULD be avoided in the same patch.

When unrelated changes are necessary, they SHOULD be separated into independently reviewable changes.

### 11.2 Functional preservation

A customization MUST identify which upstream behaviors are:

- Preserved.
- Changed.
- Removed.
- Newly introduced.
- Not applicable.

Any change to externally observable behavior MUST be documented.

The customization MUST NOT silently change an upstream interface or supported configuration.

### 11.3 Interface compatibility

A customization affecting interfaces MUST document:

- Original interface.
- Customized interface.
- Mapping or adaptation.
- Timing assumptions.
- Reset behavior.
- Parameter dependencies.
- Compatibility limitations.
- Verification approach.

Interface changes MUST be assessed against the KRITVA IP Standard and applicable SoC profile.

### 11.4 Clock and reset

A customization affecting clock or reset behavior MUST be assessed for:

- Clock source and domain assumptions.
- Clock-domain crossings.
- Reset assertion and deassertion.
- Reset-domain crossings.
- Reset synchronization.
- Reset recovery and removal behavior.
- Interactions with interface protocols.

The common reset baseline is active-low.

Reset naming follows:

`rst_<domain>_n_i`

Active-high reset usage requires an approved waiver with documented rationale.

Reset synchronizers MUST be sourced from the approved RTL library manifest. A customization MUST NOT introduce an independent reset synchronizer implementation where the approved library provides the required implementation.

A wrapper MUST NOT bypass or undermine the reset behavior required by the applicable standard.

### 11.5 Control and register interfaces

The common KRITVA IP baseline identifies APB as the primary control/register interface.

The APB revision and profile remain TBD until approved by the owner.

A customization affecting control or register access MUST assess:

- APB compatibility.
- Register access behavior.
- Address and data mapping.
- Read and write behavior.
- Error response behavior.
- Reset values.
- Register side effects.
- Bridge requirements.
- Access timing assumptions.

AXI4 MAY be used for data or high-bandwidth interfaces where justified.

AXI4-Lite, AHB-Lite, and Wishbone MAY be used through documented bridges.

A customization MUST NOT silently introduce an alternative primary control/register interface.

### 11.6 Technology boundary

The approved RTL library manifest is the sole technology boundary for technology-dependent RTL dependencies.

A customization MUST NOT introduce:

- Unapproved technology-specific cells.
- Direct foundry-cell dependencies outside the approved manifest.
- Unapproved clock-gating implementations.
- Unapproved reset synchronizer implementations.
- Unapproved technology-dependent wrappers.
- Undocumented technology-specific assumptions.

A change to the approved technology boundary requires an explicit owner decision and the applicable standard update.

### 11.7 Port naming and sequential logic

Customized RTL MUST be assessed against the applicable common conventions:

- Input ports use `_i`.
- Output ports use `_o`.
- Bidirectional ports use `_io`.
- Sequential logic uses positive-edge triggering as required by the applicable standard.
- Reset naming follows the active-low convention.

Any deviation MUST be documented and dispositioned.

### 11.8 Design-rule requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-DES-001 | A customization MUST implement only its documented purpose. | R |
| CUST-DES-002 | Unrelated changes SHOULD be separated from functional customizations. | R |
| CUST-DES-003 | Changes to externally observable behavior MUST be documented. | R |
| CUST-DES-004 | Interface changes MUST be assessed against the KRITVA IP Standard. | R |
| CUST-DES-005 | Clock and reset changes MUST be assessed for domain and synchronization effects. | R |
| CUST-DES-006 | Reset conventions MUST follow the active-low baseline or have an approved waiver. | R |
| CUST-DES-007 | Reset synchronizers MUST use the approved RTL library manifest. | R |
| CUST-DES-008 | Control/register interface changes MUST be assessed against the APB-primary baseline. | R |
| CUST-DES-009 | Technology-dependent RTL MUST remain within the approved RTL library manifest. | R |
| CUST-DES-010 | Port naming and sequential logic conventions MUST be assessed. | R |
| CUST-DES-011 | A customization MUST NOT silently introduce an unapproved technology dependency. | R |

## 12. Deviation and Waiver Management

### 12.1 Deviation definition

A deviation is a difference between a customized component and an applicable requirement, standard, approved interface, or upstream behavior.

A deviation may be:

- A temporary integration limitation.
- A deliberate interface adaptation.
- A reset or clock convention difference.
- A technology dependency difference.
- A parameter limitation.
- A verification limitation.
- A functional behavior difference.
- A documentation or release-process difference.

A deviation is not automatically a waiver.

### 12.2 Deviation record

Every material deviation MUST be recorded with:

- Deviation ID.
- Customization ID.
- Affected component and source revision.
- Applicable requirement ID.
- Description of the deviation.
- Technical rationale.
- Functional impact.
- Verification impact.
- Security impact, where applicable.
- License impact, where applicable.
- Risk assessment.
- Proposed resolution.
- Required compensating controls.
- Owner and review status.

### 12.3 Waiver requirements

A deviation from a mandatory requirement MUST be handled through an explicit waiver process where a waiver is permitted.

A waiver request MUST include:

1. Requirement ID.
2. Customization and component identifiers.
3. Exact scope of the exception.
4. Technical rationale.
5. Risk assessment.
6. Verification evidence.
7. Compensating controls.
8. Expiry or reassessment condition.
9. Authorized approver.
10. Approval date.

A waiver MUST NOT override:

- Applicable law.
- Third-party license obligations.
- Contractual restrictions.
- Security or safety obligations that cannot legally or technically be waived.
- The requirement to preserve upstream notices.
- The requirement to maintain source provenance.

### 12.4 Waiver scope

A waiver applies only to its recorded component, revision, requirement, and scope.

A waiver MUST NOT automatically apply to:

- A different component.
- A different source revision.
- A different integration.
- A different SoC profile.
- A future upstream update.
- A public release with different distribution obligations.

### 12.5 Waiver status

| Status | Meaning |
|---|---|
| PROPOSED | Waiver request created but not approved. |
| UNDER_REVIEW | Review is in progress. |
| APPROVED | Authorized approval recorded. |
| REJECTED | Waiver request rejected. |
| EXPIRED | Approved waiver has reached its expiry or reassessment condition. |
| REVOKED | Previously approved waiver withdrawn. |

A PROPOSED or UNDER_REVIEW waiver MUST NOT be treated as approved.

### 12.6 Deviation and waiver requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-WVR-001 | Material deviations MUST be documented. | R |
| CUST-WVR-002 | A mandatory requirement deviation MUST have an explicit approved waiver where permitted. | R |
| CUST-WVR-003 | Waivers MUST identify the affected requirement and customization scope. | R |
| CUST-WVR-004 | Waivers MUST include rationale and risk assessment. | R |
| CUST-WVR-005 | Waivers MUST identify expiry or reassessment conditions. | R |
| CUST-WVR-006 | A proposed or pending waiver MUST NOT be treated as approved. | R |
| CUST-WVR-007 | A waiver MUST NOT override license or contractual obligations. | R |
| CUST-WVR-008 | Waivers MUST be reassessed when their assumptions or scope change. | R |

## 13. Re-Verification After Customization

### 13.1 General requirement

Every functional customization MUST be re-verified.

The extent of re-verification MUST be appropriate to:

- The customization category.
- The files and logic affected.
- The functional behavior changed.
- The interface impact.
- Clock and reset impact.
- Parameter impact.
- Security impact.
- The component's intended integration level.

A source change MUST NOT inherit an upstream verification result as proof that the customized source is correct.

### 13.2 Verification scope

Re-verification SHOULD include the following where applicable:

| Verification area | Assessment objective |
|---|---|
| Source integrity | Confirm the expected base revision and customization are present. |
| Elaboration | Confirm source completeness and configuration validity. |
| Lint | Check coding and structural quality. |
| Functional simulation | Verify changed and affected behavior. |
| Regression | Check for unintended effects on preserved behavior. |
| Interface verification | Verify wrapper, adapter, and protocol behavior. |
| Clock/reset verification | Verify affected clock and reset assumptions. |
| Parameter verification | Verify the selected configuration and relevant boundaries. |
| Assertions | Check applicable protocol and functional properties. |
| Formal verification | Apply where appropriate to the change and component. |
| Coverage | Assess relevant functional and structural coverage. |
| Security checks | Reassess security impact where source or dependency changes warrant it. |
| Integration checks | Verify compatibility with the intended integration context. |

Not every verification area is mandatory for every change. The assessment record MUST explain which checks apply and why any relevant check is omitted.

### 13.3 KVRF evidence requirements

KVRF/cocotb is the default reference verification flow for new KRITVA-developed IP at L2+.

Equivalent verification flows MAY be used if they produce evidence records conforming to the KVRF schema.

Upstream IP MAY retain its native testbench and verification flow. Its KRITVA adoption and customization integration MUST include a wrapper-level KVRF test producing KVRF-schema evidence.

A customization MUST update or extend the relevant verification evidence to cover the changed behavior.

A wrapper-level KVRF test MUST exercise the customized integration boundary and the behavior relevant to the approved use.

### 13.4 Re-verification by category

| Category | Minimum re-verification expectation |
|---|---|
| Parameter configuration | Verify the selected configuration, supported parameter ranges, and affected behavior. |
| Wrapper or adapter | Verify interface mapping, protocol behavior, reset/clock mapping, and relevant integration behavior. |
| Patch | Verify changed functionality and regression-test affected preserved behavior. |
| Fork | Establish a verification baseline for the fork and verify the maintained changes and relevant upstream behavior. |
| Generated customization | Re-run generation as applicable and verify the generated result against the controlled inputs. |

These are minimum assessment expectations. Additional verification is required when the risk or change impact warrants it.

### 13.5 Evidence record

The re-verification record MUST identify:

- Customization ID.
- Component ID.
- Base upstream revision.
- Customized source revision.
- Verification methodology.
- Test identifiers.
- KVRF evidence record references, where applicable.
- Tool names and versions, where known.
- Configuration and parameters.
- Execution environment.
- Results.
- Logs and reports.
- Coverage or assertion evidence, where applicable.
- Known limitations.
- Reviewer and review date.

Tool versions that have not been independently established MUST be marked UNVERIFIED.

### 13.6 Verification status

| Status | Meaning |
|---|---|
| NOT_STARTED | Required verification has not started. |
| IN_PROGRESS | Verification is in progress. |
| PASS | Required verification completed successfully. |
| FAIL | One or more required checks failed. |
| INCONCLUSIVE | Results are insufficient to establish acceptance. |
| WAIVED | A valid approved waiver applies to the specific requirement. |

A customization MUST NOT be marked verification PASS when required checks are missing or inconclusive.

### 13.7 Re-verification requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-VER-001 | Functional customizations MUST be re-verified. | R |
| CUST-VER-002 | Verification MUST identify the customized source revision. | R |
| CUST-VER-003 | Verification scope MUST be based on change impact. | R |
| CUST-VER-004 | Changed functionality MUST have relevant verification evidence. | R |
| CUST-VER-005 | Regression impact MUST be assessed for modified upstream behavior. | R |
| CUST-VER-006 | KVRF-schema evidence MUST be produced according to the applicable verification policy. | R |
| CUST-VER-007 | Equivalent verification flows MUST produce KVRF-schema evidence records. | R |
| CUST-VER-008 | Upstream IP MUST retain its native testbench where applicable and have a wrapper-level KVRF test for KRITVA integration. | R |
| CUST-VER-009 | Tool versions MUST be marked UNVERIFIED when not independently established. | R |
| CUST-VER-010 | A failed or inconclusive mandatory verification result MUST prevent customization acceptance until resolved or validly waived. | R |

## 14. Upstream Update and Rebase Policy

### 14.1 Update principle

An upstream update is a new source revision requiring controlled evaluation.

A customized component MUST NOT be updated merely because a newer upstream release is available.

The update process MUST preserve:

- The previous upstream revision.
- The previous customized revision.
- The patch and modification history.
- The customization rationale.
- Existing waiver history.
- Verification evidence for the previous baseline.
- The new upstream revision and its assessment.
- The result of the rebase or merge.

### 14.2 Update preparation

Before updating a customized component, the maintainer MUST:

1. Identify the currently adopted upstream revision.
2. Identify the proposed upstream revision.
3. Record the current KRITVA customized revision.
4. Inventory all local customizations.
5. Review upstream changes since the current base.
6. Review changes to interfaces and parameters.
7. Reassess license and notice changes.
8. Review security advisories and known defects.
9. Identify potential conflicts.
10. Define the rebase or merge strategy.

### 14.3 Patch-based customization

For a patch-based customization:

- Patches MUST be associated with their original base revision.
- The new upstream revision MUST be recorded.
- Patches MUST be reapplied or rebased in a controlled manner.
- Patch conflicts MUST be reviewed rather than resolved mechanically without assessment.
- A patch MUST NOT be silently dropped because it fails to apply.
- A patch that is no longer required SHOULD be explicitly retired with rationale.
- Changes to patch behavior MUST trigger re-verification.

The resulting patch series MUST remain reproducible against the new upstream base.

### 14.4 Wrapper-based customization

A wrapper may not require source-level rebasing, but upstream interface changes can invalidate its assumptions.

For every upstream update, the maintainer MUST assess:

- Port and interface changes.
- Parameter changes.
- Clock and reset changes.
- Protocol behavior.
- Error handling.
- Timing assumptions.
- Configuration compatibility.
- Verification wrapper assumptions.

A wrapper MUST be re-verified when the upstream update can affect its behavior or compatibility.

### 14.5 Parameter configuration

An upstream update may add, remove, rename, or change parameter behavior.

The maintainer MUST:

- Compare parameter definitions.
- Check supported ranges.
- Review default values.
- Review parameter dependencies.
- Identify deprecated or removed parameters.
- Validate the KRITVA configuration against the new revision.
- Re-run configuration-specific verification.

A configuration MUST NOT silently rely on a removed or changed parameter.

### 14.6 Fork maintenance

A fork MUST maintain an explicit relationship to upstream.

The fork maintainer SHOULD:

- Track upstream releases and significant changes.
- Maintain an upstream merge or rebase reference.
- Keep local changes reviewable.
- Separate upstream synchronization from unrelated local feature work.
- Record conflict resolutions.
- Review license and notice changes.
- Maintain a re-verification plan.

A fork MUST have an owner responsible for its maintenance and upstream update decisions.

### 14.7 Update decision

After the update assessment, the maintainer MUST record one of the following:

| Outcome | Meaning |
|---|---|
| ACCEPT_UPDATE | New upstream revision and customized result are accepted. |
| HOLD_UPDATE | Update is deferred pending resolution of identified issues. |
| REJECT_UPDATE | Proposed update is not accepted. |
| RETAIN_CURRENT | Existing adopted revision remains in use. |
| RETIRE_CUSTOMIZATION | Existing customization is no longer required and is retired through a controlled change. |

The update decision MUST include rationale and evidence references.

### 14.8 Rebase and update requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-UPD-001 | Upstream updates MUST be evaluated as new source revisions. | R |
| CUST-UPD-002 | The previous upstream and customized revisions MUST remain traceable. | R |
| CUST-UPD-003 | Local patches MUST be inventoried before a rebase or merge. | R |
| CUST-UPD-004 | Patch conflicts MUST be reviewed and documented. | R |
| CUST-UPD-005 | A patch MUST NOT be silently dropped during an update. | R |
| CUST-UPD-006 | Wrapper compatibility MUST be reassessed when upstream interfaces change. | R |
| CUST-UPD-007 | Parameter configurations MUST be reassessed when upstream parameter definitions change. | R |
| CUST-UPD-008 | Forks MUST preserve upstream identity and maintain a documented update strategy. | R |
| CUST-UPD-009 | License and notice changes MUST be reassessed before adopting an updated revision. | R |
| CUST-UPD-010 | Material changes resulting from an upstream update MUST be re-verified. | R |
| CUST-UPD-011 | The update decision MUST be recorded. | R |
| CUST-UPD-012 | A newer upstream release MUST NOT automatically replace the currently adopted revision. | R |

## 15. Customization Lifecycle and Status

### 15.1 Lifecycle

A customization follows the lifecycle below:

| Stage | Name | Description |
|---|---|---|
| CUST-ST-01 | PROPOSED | Customization need identified. |
| CUST-ST-02 | ASSESSED | Category, rationale, and impact assessed. |
| CUST-ST-03 | APPROVED_FOR_IMPLEMENTATION | Required implementation approval recorded. |
| CUST-ST-04 | IN_IMPLEMENTATION | Customization being implemented. |
| CUST-ST-05 | UNDER_REVIEW | Source changes and records under review. |
| CUST-ST-06 | VERIFICATION | Re-verification in progress. |
| CUST-ST-07 | ACCEPTED | Required review and verification completed. |
| CUST-ST-08 | MAINTENANCE | Accepted customization maintained against its source revision. |
| CUST-ST-09 | REASSESSMENT | Upstream update or material change under evaluation. |
| CUST-ST-10 | RETIRED | Customization no longer used and retirement recorded. |
| CUST-ST-11 | REJECTED | Customization proposal rejected. |

### 15.2 Status transition controls

A customization MUST NOT transition to ACCEPTED unless:

- Its implementation is complete.
- Required source and patch records are complete.
- Required technical review is complete.
- Applicable license obligations are addressed.
- Applicable deviations and waivers are dispositioned.
- Required verification evidence is available.
- The intended integration scope is documented.
- The acceptance decision is recorded.

A customization MUST NOT transition to RETIRED without a record of its replacement, removal, or reason for retirement.

### 15.3 Lifecycle requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-LCY-001 | Customization status MUST reflect the actual lifecycle state. | R |
| CUST-LCY-002 | A customization MUST NOT be ACCEPTED with unresolved mandatory blockers. | R |
| CUST-LCY-003 | Verification status MUST be recorded separately from implementation status. | R |
| CUST-LCY-004 | A rejected customization MUST retain its decision rationale. | R |
| CUST-LCY-005 | A retired customization MUST retain its historical records. | R |
| CUST-LCY-006 | Reassessment MUST preserve the previous accepted baseline and its evidence. | R |

## 16. Customization Register

### 16.1 Purpose

The customization register provides a consolidated inventory of customization activities.

It supports:

- Identification of customized components.
- Tracking of source revisions.
- Visibility of upstream divergence.
- Review of patch and fork maintenance.
- Verification status tracking.
- Waiver and deviation traceability.
- Upstream update planning.
- Customization retirement.

The register is an index and status record. It does not replace the detailed intake, patch, verification, waiver, or approval records.

### 16.2 Register schema

The following fields define the minimum customization register format.

| Field | Type | Required | Description |
|---|---|---|---|
| customization_id | string | Yes | Stable KRITVA customization identifier. |
| component_id | string | Yes | Stable IP component identifier. |
| component_name | string | Yes | Component name. |
| source_class | string | Yes | KRITVA-owned, third-party, vendor, or other approved source classification. |
| upstream_project | string | Conditional | Original upstream project or provider. |
| upstream_repository | string | Conditional | Authoritative upstream source location. |
| upstream_revision | string | Conditional | Immutable upstream commit or equivalent revision. |
| customized_revision | string | Yes | Revision identifying the customized result. |
| category | array | Yes | One or more customization categories. |
| rationale | string | Yes | Reason for customization. |
| requirement_refs | array | Yes | Applicable requirement and decision references. |
| changed_files | array | Yes | Files or logical source areas changed. |
| customization_status | string | Yes | Lifecycle status from Section 15. |
| technical_review | string | Yes | Technical review state or reference. |
| license_review | string | Yes | License review state or reference. |
| security_review | string | Yes | Security review state or reference. |
| verification_status | string | Yes | Verification status from Section 13. |
| kvrf_evidence_refs | array | Conditional | KVRF-schema evidence record references, where applicable. |
| waiver_refs | array | No | Approved waiver references. |
| deviation_refs | array | No | Deviation record references. |
| upstream_update_strategy | string | Yes | Wrapper compatibility, patch rebase, fork synchronization, or other strategy. |
| maintenance_owner | string | Yes | Responsible maintainer. |
| approval_reference | string | Conditional | Approval decision record reference. |
| approval_date | string | Conditional | Approval date. |
| last_review_date | string | No | Most recent review date. |
| next_review_condition | string | No | Event or condition requiring reassessment. |
| notes | string | No | Additional non-sensitive information. |

A field marked Conditional MUST be present when applicable to the source category or customization type.

### 16.3 Example register record

The following example is illustrative and does not represent an actual adopted component.

~~~yaml
customization_id: CUST-EXAMPLE-001
component_id: IP-EXAMPLE-001
component_name: Example IP Component

source_class: THIRD_PARTY

upstream_project: Example Upstream Project
upstream_repository: TBD
upstream_revision: UNKNOWN
customized_revision: TBD

category:
  - WRAPPER_ADAPTER
  - PARAMETER_CONFIGURATION

rationale: >
  Illustrative interface adaptation and supported parameter configuration.

requirement_refs:
  - KRITVA_IP_STANDARD
  - APPLICABLE_INTEGRATION_REQUIREMENTS

changed_files:
  - integration/example_wrapper.sv
  - config/example_config.yaml

customization_status: PROPOSED

technical_review: NOT_STARTED
license_review: NOT_STARTED
security_review: NOT_STARTED

verification_status: NOT_STARTED
kvrf_evidence_refs: []

waiver_refs: []
deviation_refs: []

upstream_update_strategy: WRAPPER_COMPATIBILITY_REVIEW
maintenance_owner: TBD

approval_reference: null
approval_date: null

last_review_date: null
next_review_condition: UPSTREAM_REVISION_CHANGE

notes: >
  Illustrative record only. No adoption or customization approval is implied.
~~~

### 16.4 Register integrity

The customization register MUST:

- Use stable identifiers.
- Reference immutable source revisions where applicable.
- Distinguish upstream source from customized source.
- Reflect actual customization status.
- Reference the latest accepted verification evidence.
- Identify active waivers and deviations.
- Identify a maintenance owner.
- Preserve historical decisions.
- Avoid publishing confidential or restricted information.

A register entry MUST NOT imply approval solely because it exists.

### 16.5 Register requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-REG-001 | Every accepted customization MUST have a register entry. | R |
| CUST-REG-002 | The register MUST identify the affected component and source revision. | R |
| CUST-REG-003 | The register MUST identify the customization category. | R |
| CUST-REG-004 | The register MUST reference applicable verification evidence. | R |
| CUST-REG-005 | Active waivers and deviations MUST be referenced. | R |
| CUST-REG-006 | Every maintained customization MUST identify a maintenance owner. | R |
| CUST-REG-007 | Register status MUST be consistent with the detailed customization records. | R |
| CUST-REG-008 | Historical register entries MUST remain traceable after customization retirement. | R |

## 17. Review and Approval Responsibilities

### 17.1 Roles

| Role | Responsibility |
|---|---|
| Customization proposer | Identifies the requirement and proposes the customization. |
| Customization owner | Maintains the customization record and implementation. |
| Technical reviewer | Reviews technical rationale, source changes, and integration impact. |
| Verification reviewer | Reviews re-verification scope and evidence. |
| License reviewer | Reviews source rights, license obligations, and attribution implications. |
| Security reviewer | Reviews security impact and relevant dependencies. |
| Repository maintainer | Ensures controlled source integration and record consistency. |
| Owner / authorized approver | Approves customization acceptance and applicable exceptions. |

Dinesh Annayya is the owner for decisions and open items defined by this policy.

Review activities MAY be delegated to qualified reviewers.

Delegation of implementation or review work does not automatically delegate adoption or waiver approval authority.

### 17.2 Review checkpoints

The following checkpoints SHOULD be used:

| Checkpoint | Review objective |
|---|---|
| Proposal review | Confirm the need and proposed customization category. |
| Design review | Confirm the preferred approach and impact assessment. |
| Source review | Review actual implementation and change records. |
| License review | Confirm license and attribution compliance. |
| Integration review | Confirm compliance with the applicable KRITVA IP requirements. |
| Verification review | Confirm required tests and evidence. |
| Acceptance review | Confirm all mandatory conditions are satisfied. |
| Maintenance review | Reassess upstream compatibility and maintenance risk. |

### 17.3 Approval requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-APR-001 | A customization MUST have an identified owner. | R |
| CUST-APR-002 | Source changes MUST receive technical review before acceptance. | R |
| CUST-APR-003 | Required license and security reviews MUST be completed before acceptance. | R |
| CUST-APR-004 | Verification evidence MUST be reviewed before acceptance. | R |
| CUST-APR-005 | Waivers MUST be approved by the authorized owner or delegate. | R |
| CUST-APR-006 | Acceptance MUST be explicitly recorded. | R |
| CUST-APR-007 | Review completion MUST NOT be inferred from a successful CI run or merged change. | R |

## 18. Public and Private Boundary

### 18.1 Public records

Public KRITVA repositories MAY contain:

- Public upstream source references.
- Public immutable revision identifiers.
- Public license identifiers and notices.
- KRITVA-authored customization records approved for disclosure.
- Public patch descriptions.
- Public wrapper and adapter documentation.
- Public verification evidence.
- Public customization register entries.
- Public waiver summaries approved for disclosure.

### 18.2 Restricted information

The following MUST NOT be published without authorization:

- Proprietary or confidential source code.
- Restricted vendor collateral.
- Non-public commercial terms.
- Private supplier correspondence.
- Credentials and access tokens.
- Unreleased SoC architecture and implementation details.
- Private repository paths or internal review information that exposes unreleased implementation.
- Security-sensitive details not cleared for publication.
- Confidential verification or product information.

A public record MAY reference private evidence through a non-sensitive identifier.

This document does not disclose unreleased Nexus or Edge implementation details.

### 18.3 Copyright and attribution

KRITVA-authored files MUST use the copyright holder wording:

**Kritva Robotics**

Original upstream notices MUST remain intact.

Where customized source contains upstream material, applicable upstream copyright and license obligations MUST be preserved.

KRITVA copyright wording MUST NOT imply ownership of third-party source material.

### 18.4 Public/private requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-PUB-001 | Public customization records MUST contain only information cleared for public disclosure. | R |
| CUST-PUB-002 | Confidential or restricted source MUST NOT be copied into public repositories without authorization. | R |
| CUST-PUB-003 | Public records MUST preserve applicable upstream license and attribution information. | R |
| CUST-PUB-004 | KRITVA-authored files MUST use the copyright holder wording `Kritva Robotics`. | R |
| CUST-PUB-005 | Public customization records MUST NOT disclose unreleased SoC implementation details. | R |
| CUST-PUB-006 | Private evidence MAY be referenced by a non-sensitive identifier. | R |

## 19. Enforcement and Assessment

### 19.1 Enforcement classes

This policy uses the enforcement classes aligned with `KRITVA_IP_STANDARD.md` and `KNX-RTL-STD-001`.

| Class | Name | Meaning |
|---|---|---|
| A | Automated | A requirement that can be checked by an automated script, tool, or CI process. |
| T | Tool-assisted | Tools provide evidence, but human interpretation or review remains necessary. |
| R | Review only | Human review, judgment, or explicit approval is required. |

The enforcement class describes the expected assessment method. It does not change the normative force of a requirement.

### 19.2 Assessment results

Customization assessment MUST use explicit outcomes appropriate to the check:

- PASS
- FAIL
- WAIVED
- NOT APPLICABLE
- UNKNOWN

UNKNOWN MUST NOT be treated as PASS.

A failed mandatory requirement MUST prevent acceptance unless an approved and permissible waiver applies.

### 19.3 Tool versions

Tools used for source comparison, patch management, build, verification, lint, and evidence generation SHOULD be recorded with their versions and relevant configuration.

**Tool versions for this document are UNVERIFIED.**

No specific tool version or toolchain configuration is approved by this document.

### 19.4 Enforcement requirements

| Requirement ID | Requirement | Enforcement |
|---|---|---|
| CUST-ENF-001 | Every mandatory customization requirement MUST have an identifiable assessment result. | R |
| CUST-ENF-002 | Enforcement classes MUST use A/T/R consistently with the KRITVA IP Standard. | R |
| CUST-ENF-003 | UNKNOWN MUST NOT be treated as PASS. | R |
| CUST-ENF-004 | Automated and tool-assisted results MUST retain sufficient evidence for review. | R |
| CUST-ENF-005 | Tool versions MUST be marked UNVERIFIED when not independently established. | R |
| CUST-ENF-006 | An assessment result MUST NOT replace an explicit customization acceptance decision. | R |

## 20. Document Maintenance

This document is maintained as a public KRITVA policy.

Changes MUST be reviewed for impact on:

- Customization categories.
- Preferred customization order.
- Source and record separation.
- License and provenance obligations.
- Deviation and waiver management.
- Verification and KVRF evidence requirements.
- Upstream update and rebase rules.
- Customization register fields.
- Public/private boundaries.
- Related KRITVA standards and policies.

A policy revision MUST NOT silently change the status or historical approval basis of existing customizations.

### 20.1 Versioning

| Version change | Meaning |
|---|---|
| Major | Incompatible changes to customization policy or mandatory controls. |
| Minor | New categories, requirements, or substantive additions that preserve the policy framework. |
| Patch | Editorial corrections, clarifications, and non-substantive changes. |

### 20.2 Approval status

The current document status is DRAFT.

Publication of this document does not constitute approval of any specific customization, patch, fork, wrapper, or waiver.

---

## 21. Open Items

The following items require explicit owner decisions. They are not approved assumptions.

Owner for all items: **Dinesh Annayya**.

| ID | Open item | Decision required | Owner | Status |
|---|---|---|---|---|
| CUST-OI-001 | Customization ID format | Approve a canonical customization identifier format and allocation authority. | Dinesh Annayya | OPEN |
| CUST-OI-002 | Customization register schema | Approve the canonical machine-readable customization register format. | Dinesh Annayya | OPEN |
| CUST-OI-003 | Register location | Decide whether customization registers are maintained per repository, centrally, or through a shared registry. | Dinesh Annayya | OPEN |
| CUST-OI-004 | Wrapper acceptance checklist | Approve a reusable wrapper and adapter acceptance checklist. | Dinesh Annayya | OPEN |
| CUST-OI-005 | Patch format | Select the preferred patch representation and patch-series management approach. | Dinesh Annayya | OPEN |
| CUST-OI-006 | Fork ownership | Define the approval authority and maintenance ownership requirements for long-lived forks. | Dinesh Annayya | OPEN |
| CUST-OI-007 | Rebase cadence | Define whether upstream reassessment should use a periodic cadence in addition to event-triggered review. | Dinesh Annayya | OPEN |
| CUST-OI-008 | Re-verification thresholds | Define common change-impact thresholds for selecting verification scope. | Dinesh Annayya | OPEN |
| CUST-OI-009 | KVRF evidence schema versioning | Define the version compatibility and migration policy for KVRF-schema evidence records. | Dinesh Annayya | OPEN |
| CUST-OI-010 | Waiver authority | Confirm approval authority and delegation rules for customization-related waivers. | Dinesh Annayya | OPEN |
| CUST-OI-011 | Generated source handling | Define additional requirements for generated source and generator reproducibility. | Dinesh Annayya | OPEN |
| CUST-OI-012 | Customization retirement | Define minimum retirement evidence and archival requirements. | Dinesh Annayya | OPEN |
| CUST-OI-013 | Toolchain baseline | Establish verified tool versions and configurations for customization and rebase activities. Current tool versions remain UNVERIFIED. | Dinesh Annayya | OPEN |
| CUST-OI-014 | APB revision and profile | Approve the APB revision and control/register interface profile for the common IP baseline. | Dinesh Annayya | OPEN |

## 22. References

1. `KRITVA_IP_STANDARD.md` — Common IP design and integration requirements.
2. `OPEN_SOURCE_IP_POLICY.md` — Third-party source, licensing, provenance, and redistribution policy.
3. `IP_ADOPTION_PROCESS.md` — IP discovery, evaluation, adoption, and integration process.
4. `KNX-RTL-STD-001` — Nexus SoC RTL design profile.
5. Applicable upstream project licenses and notices.
6. Applicable KVRF verification methodology and evidence schema.
7. Applicable KRITVA repository contribution and release procedures.

The references do not imply approval of any specific IP component, customization, tool version, or integration.

---

## 23. Change History

| Version | Date | Status | Description |
|---|---|---|---|
| 0.1.0 | 2026-11-12 | DRAFT | Initial customization policy covering customization categories, preferred approach, modification records, upstream separation, waivers, re-verification, upstream updates, and customization register requirements. |

---

**End of Document**