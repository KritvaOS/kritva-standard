# KRITVA IP Standard

| Field | Value |
|---|---|
| Document ID | KSTD-IPSTD-001 |
| Document | KRITVA IP Standard |
| Repository | `KritvaOS/kritva-standard` |
| Version | 0.1.0 |
| Status | DRAFT |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Approver | Dinesh Annayya (`dineshannayya`) |
| Last Updated | 2026-11-13 |

> **Status notice:** This document defines the proposed normative engineering
> contract for KRITVA semiconductor IP. It is DRAFT and is not an approved
> KRITVA engineering baseline until explicitly approved by Dinesh Annayya.
>
> Decisions marked PROPOSED or TBD are not approved design decisions.
> Requirements that depend on unresolved owner decisions must not be
> interpreted as evidence that the corresponding architecture has been
> selected.

---

## 1. Purpose

The KRITVA IP Standard defines a common engineering contract for
semiconductor IP developed, adopted, customized, verified, qualified and
integrated within the KRITVA project.

It establishes consistent requirements for:

- IP identity and classification.
- Functional and feature specifications.
- Interface and protocol definitions.
- Clock, reset and clock-domain crossing management.
- Parameterization and RTL conventions.
- Register specification and generation.
- Technology independence and implementation portability.
- Design-for-test, low-power, debug and security hooks.
- Supported hardware description languages.
- Lint and static analysis.
- Verification and evidence.
- Quality assessment.
- Packaging and release management.
- Public information and publication safety.
- SoC integration profiles.

The standard applies to three IP source categories:

1. Internal KRITVA IP.
2. Open-source IP.
3. Commercial or licensed third-party IP.

Requirements apply according to their defined applicability and the
compliance level claimed by an IP.

## 2. Scope

### 2.1 In scope

This standard covers the reusable engineering contract between an IP
provider and its consumers.

It defines what an IP package must specify, expose, document, verify and
deliver.

It also defines the minimum information required to assess whether an
IP is suitable for reuse and integration into a KRITVA SoC.

### 2.2 Out of scope

The following are addressed by separate standards or project-specific
engineering processes:

- Complete SoC architecture and microarchitecture.
- Detailed physical-design methodology.
- Static timing analysis and timing signoff methodology.
- DFT implementation and ATPG signoff methodology.
- Foundry-specific implementation rules.
- Commercial EDA licensing and tool procurement.
- SoC-specific address maps and final integration topology.
- Programme planning, milestones, task status and programme approvals.

These areas may impose additional requirements on an IP or its integration
profile.

### 2.3 Applicability

This standard applies to:

- New KRITVA-developed IP.
- Adopted open-source IP.
- Customized downstream IP.
- Commercial and licensed third-party IP where contractually and
  technically applicable.
- Reusable IP intended for one or more KRITVA SoC consumers.

For third-party IP, requirements that cannot be assessed because the
implementation is inaccessible must be marked NOT_ASSESSABLE or
NOT_APPLICABLE with justification and supporting evidence. They must not
be silently treated as passed.

---

## 3. Normative terminology and requirement conventions

### 3.1 RFC 2119 terminology

The keywords below are interpreted as normative requirement levels:

| Keyword | Meaning |
|---|---|
| MUST | Mandatory requirement |
| MUST NOT | Prohibited behavior |
| SHOULD | Recommended requirement; deviations require documented justification |
| SHOULD NOT | Discouraged behavior; exceptions require documented justification |
| MAY | Optional capability or behavior |

These keywords are used in uppercase when expressing normative
requirements.

MUST is the preferred normative keyword in common KRITVA standards.
Where an approved SoC-specific profile (for example `KNX-RTL-STD-001`)
uses SHALL or SHALL NOT, those terms have the same normative force as
MUST and MUST NOT. The normative force of a requirement is independent of
its enforcement class.

### 3.2 Requirement identifiers

Every normative requirement must have a stable identifier.

The identifier format is:

`KIP-STD-<AREA>-<NNN>`

Where:

- `KIP-STD` identifies the KRITVA IP Standard.
- `<AREA>` identifies the requirement area.
- `<NNN>` is a zero-padded sequential number within that area.

Examples:

- `KIP-STD-IDENTITY-001`
- `KIP-STD-INTERFACE-001`
- `KIP-STD-CLKRST-001`
- `KIP-STD-REGS-001`

Requirement identifiers MUST NOT be reused for unrelated requirements.

A retired requirement ID must remain identifiable in the standard's
change history.

#### 3.2.1 Identifier namespaces

KRITVA maintains separate, namespaced requirement identifier schemes:

| Namespace | Scope |
|---|---|
| `KIP-STD-<AREA>-NNN` | Common cross-SoC KRITVA IP standards |
| `KNX-RTL-<CAT>-NNN` | Nexus-specific RTL design profile (`KNX-RTL-STD-001`) |
| Edge scheme (TBD) | A separate scheme to be defined when the Edge profile is created |

Identifiers MUST NOT be renumbered to align the schemes. A cross-reference
table maps profile rules to common requirements using the relationship
values `EQUIVALENT`, `STRICTER` and `NEXUS_ONLY` (see Section 20).

When a profile rule is promoted into the common standard, the common
standard MUST assign a new `KIP-STD` identifier and retain a
`derived-from` reference to the originating profile rule. The originating
profile identifier remains unchanged in its own repository.

### 3.3 Requirement attributes

Each requirement has the following attributes:

| Attribute | Description |
|---|---|
| ID | Stable requirement identifier |
| Requirement | Normative statement |
| Level | MUST, SHOULD or MAY |
| Compliance applicability | Minimum compliance level at which it applies |
| Enforcement | A, T or R assessment class |
| Assessment method | How compliance is demonstrated |
| Evidence | Expected record, report, test or inspection result |

Enforcement classes:

| Class | Meaning |
|---|---|
| A | Automated — checked by an automated script, CI check or machine-readable validation |
| T | Tool-assisted — checked using a tool, with engineering interpretation or review of its output |
| R | Review only — assessed through documented engineering inspection or review |

The enforcement class describes the expected assessment approach. It
does not replace the assessment method or evidence requirement.

A requirement may use more than one assessment method. Where multiple
methods are required, the enforcement class should identify the principal
method and the assessment record should identify any additional methods.

### 3.4 Compliance applicability

Compliance levels are cumulative.

| Level | Name | Meaning |
|---|---|---|
| L0 | Registered | IP identity and source provenance are registered |
| L1 | Evaluated | IP has been technically evaluated: functionality, interfaces, source baseline and applicable requirements are documented, and an adoption or continuation decision is recorded |
| L2 | Verified | Required verification activities have passed and evidence is accepted |
| L3 | Release-qualified | IP has passed applicable release, quality and integration qualification gates |

An IP claiming a higher level must satisfy all applicable requirements
at lower levels.

The L0 to L3 definitions in this table are aligned with the assurance levels
in the IP Lifecycle Policy (LCP section 6) and the KVRF Specification. L1 is
"Evaluated", not "Specified" (alignment proposed 2026-11-13; see
IPSTD-OI-014). A complete specification package and an approved verification
plan are expected by L2.

### 3.5 Compliance applicability values

- L0: requirement applies from Registered level.
- L1: requirement applies from Evaluated level.
- L2: requirement applies from Verified level.
- L3: requirement applies from Release-qualified level.

Requirements marked MAY describe optional capabilities. They do not
become mandatory merely because an IP claims a higher compliance level.

### 3.6 Requirement assessment states

Each requirement assessment must use one of the following states:

- NOT_ASSESSED
- PASS
- FAIL
- NOT_APPLICABLE
- DEVIATION_APPROVED

NOT_APPLICABLE requires a technical justification and approval where
the requirement is mandatory at the claimed compliance level.

DEVIATION_APPROVED requires an approved deviation record. It must not
be represented as an unconditional PASS.

### 3.7 Compliance levels and release claims

A compliance claim must identify:

- IP identifier.
- IP release version or assessed source commit.
- Standard version.
- Claimed compliance level.
- Requirement assessment summary.
- Applicable deviations and waivers.
- Evidence references.
- Assessment date.
- Reviewer and approver.

---

## 4. IP identity and classification (IDENTITY)

### 4.1 IP identifiers

Every KRITVA-managed IP MUST have a stable unique identifier.

Identifier format:

`KIP-<CAT>-<NNN>`

Examples:

| Category | Example ID | Description |
|---|---|---|
| CPU | KIP-CPU-001 | Processor IP |
| Memory | KIP-MEM-001 | Memory controller or memory subsystem IP |
| Peripheral | KIP-PER-001 | UART or other peripheral |
| Interrupt | KIP-INT-001 | Interrupt controller |
| DMA | KIP-DMA-001 | DMA controller |
| Interconnect | KIP-ICN-001 | Bus or interconnect IP |
| Network | KIP-NET-001 | Networking IP |
| Industrial | KIP-IND-001 | Industrial communication IP |
| Control | KIP-CTL-001 | Control-related IP |
| Accelerator | KIP-ACC-001 | Hardware accelerator |
| Security | KIP-SEC-001 | Security IP |

The category list may be extended through a reviewed change.

### 4.2 Identity requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-IDENTITY-001 | Every KRITVA-managed IP MUST have one stable unique IP identifier. | MUST | L0 | A | INSPECTION |
| KIP-STD-IDENTITY-002 | Every IP MUST declare its source category as INTERNAL, OPEN_SOURCE or COMMERCIAL. | MUST | L0 | A | INSPECTION |
| KIP-STD-IDENTITY-003 | Every IP MUST identify its owner or responsible maintainer. | MUST | L0 | A | INSPECTION |
| KIP-STD-IDENTITY-004 | Every IP MUST identify its repository or controlled source location. | MUST | L0 | A | INSPECTION |
| KIP-STD-IDENTITY-005 | Every IP MUST identify its upstream project and immutable source commit when derived from upstream IP. | MUST | L0 | A | INSPECTION, EVIDENCE |
| KIP-STD-IDENTITY-006 | Every IP release MUST have a version identifier. | MUST | L1 | A | INSPECTION |
| KIP-STD-IDENTITY-007 | An IP SHOULD identify applicable Nexus and Edge consumer profiles. | SHOULD | L1 | R | INSPECTION |
| KIP-STD-IDENTITY-008 | An IP MUST NOT change its stable identifier merely because its implementation or release version changes. | MUST | L0 | A | INSPECTION |

### 4.3 Source categories

**INTERNAL**

IP developed and controlled by KRITVA.

**OPEN_SOURCE**

IP derived from a publicly available upstream project under an applicable
open-source licence. Its upstream identity, licence, commit baseline and
customization history must be retained.

**COMMERCIAL**

IP provided under commercial, proprietary or other restricted licensing
terms. Its licence and permitted usage must be respected.

Source category and redistribution rights must be recorded independently.

### 4.4 Versioning

KRITVA IP releases SHOULD use semantic versioning:

- MAJOR: incompatible interface, behavior or specification changes.
- MINOR: backward-compatible functionality additions.
- PATCH: backward-compatible fixes.

An IP package may also identify independently versioned:

- IP specification.
- Register map.
- Verification plan.
- Integration profile.
- Upstream baseline.
- Toolchain configuration.

An upstream version and a KRITVA IP release version are distinct identities.

### 4.5 Version requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-IDENTITY-009 | An IP release MUST identify its version and source revision. | MUST | L1 | A | INSPECTION |
| KIP-STD-IDENTITY-010 | An open-source IP release MUST identify its upstream baseline separately from its KRITVA release version. | MUST | L0 | A | INSPECTION |
| KIP-STD-IDENTITY-011 | An IP release SHOULD identify backward-compatibility implications. | SHOULD | L1 | R | INSPECTION |
| KIP-STD-IDENTITY-012 | Released IP versions MUST be immutable; changes require a new release version. | MUST | L3 | A | EVIDENCE |

---

## 5. IP specification (SPEC)

### 5.1 Specification objectives

An IP specification defines the externally observable behavior and
integration contract of an IP.

The specification must be independent of implementation details unless
those details affect integration, performance, configuration or behavior.

### 5.2 Feature identification

Every functional feature must have a stable feature identifier.

Suggested format:

`<IP-ID>-F<NNN>`

Example:

`KIP-PER-001-F001`

Feature records should identify:

- Feature identifier.
- Feature name.
- Functional description.
- Inputs and outputs.
- Configuration dependencies.
- Expected behavior.
- Error and boundary behavior.
- Verification method.
- Applicable interfaces and registers.
- Feature status.

### 5.3 Required specification document set

At L1, the IP specification package must include the following documents
or equivalent structured content:

1. IP overview and purpose.
2. Functional specification.
3. Feature list and traceability.
4. Interface specification.
5. Clock and reset specification.
6. Parameter and configuration specification.
7. Register specification, where applicable.
8. Interrupt specification, where applicable.
9. Error and exception behavior.
10. Integration requirements.
11. Verification plan.
12. Limitations and known constraints.

### 5.4 Specification requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-SPEC-001 | An IP MUST have a functional specification describing its externally observable behavior. | MUST | L1 | R | INSPECTION |
| KIP-STD-SPEC-002 | Functional features MUST have stable feature identifiers. | MUST | L1 | A | INSPECTION |
| KIP-STD-SPEC-003 | The specification MUST identify supported operating modes and configurations. | MUST | L1 | R | INSPECTION |
| KIP-STD-SPEC-004 | The specification MUST describe error, boundary and exceptional behavior. | MUST | L1 | R | INSPECTION |
| KIP-STD-SPEC-005 | The specification MUST identify assumptions, limitations and dependencies. | MUST | L1 | R | INSPECTION |
| KIP-STD-SPEC-006 | Features SHOULD map to verification activities and evidence. | SHOULD | L1 | A | INSPECTION |
| KIP-STD-SPEC-007 | Specification changes MUST be traceable to the applicable IP release. | MUST | L3 | A | EVIDENCE |

---

## 6. Interface contract (INTERFACE)

### 6.1 General interface requirements

An IP must define all interfaces required for functional operation and
integration.

Interface specifications must identify:

- Interface name and purpose.
- Protocol and version.
- Signal names and widths.
- Signal direction.
- Clock association.
- Reset behavior.
- Timing requirements.
- Handshake and transaction behavior.
- Error and timeout behavior.
- Parameter-dependent behavior.
- Optional signals and features.

An interface must not rely on undocumented assumptions between the
IP provider and consumer.

### 6.2 Memory-mapped control and register bus

**OWNER DECISION (2026-11-12): APB is the primary control/register bus
for KRITVA IP.**

The APB revision and KRITVA-supported profile remain TBD and are tracked
as IPSTD-OI-001.

Permitted alternatives:

- AXI4 for data movement and high-bandwidth interfaces.
- AXI4-Lite through a documented bridge.
- AHB-Lite through a documented bridge.
- Wishbone through a documented bridge and constrained supported profile.

An IP may retain a native interface different from the primary KRITVA
control/register interface when required by its functionality or upstream
origin. The adaptation boundary and bridge must be documented.

This decision is consistent with a fabric-plus-APB-bridge integration
approach: a system fabric may connect to peripheral control/register
interfaces through documented APB bridges. It does not prescribe any
particular SoC topology.

This decision does not select a final system interconnect or define
a high-bandwidth data-fabric architecture.

### 6.3 Bus trade-off comparison

| Interface | Strengths | Considerations |
|---|---|---|
| APB | Simple peripheral interface, low complexity, suitable for control and register access | Lower throughput; generally requires bridging from a system fabric |
| AXI4 | High-bandwidth data interface, burst transactions and broad ecosystem support | Greater interface and integration complexity |
| AXI4-Lite | Memory-mapped control interface with independent channels | More signals and handshake complexity than APB; requires a documented bridge under this standard |
| AHB-Lite | Established AMBA interface, suitable for simpler system fabrics | Requires a documented bridge under this standard |
| Wishbone | Open specification and flexible implementation profiles | Supported features and bridge behavior must be constrained for interoperability |

**Rationale:** APB provides a simple and consistent peripheral
control/register interface. AXI4 remains an allowed interface for
high-bandwidth data movement. Other memory-mapped protocols may be
supported through explicit, documented and verified bridges.

The final choice must consider available IP, bridge cost, verification
effort, performance requirements and implementation complexity.

APB is the owner-approved primary control/register bus. No APB revision,
KRITVA interface profile or alternate-bus profile is approved by this
DRAFT document.

### 6.4 Interface profiles and bridges

The standard should eventually define a KRITVA-supported interface profile
for every accepted protocol.

A profile should define:

- Protocol revision.
- Supported features.
- Transfer size and data width rules.
- Address alignment.
- Byte-enable behavior.
- Wait-state behavior.
- Response and error handling.
- Reset behavior.
- Outstanding transaction constraints, where applicable.
- Clock-domain assumptions.
- Required protocol checks.

An IP using an alternate bus MUST document its native interface and
required bridge.

Bridge implementations must be independently identified and verified.

### 6.5 Interrupt interfaces

Interrupt behavior must be documented where applicable.

The specification must identify:

- Interrupt source and purpose.
- Level-sensitive or edge-sensitive behavior.
- Active polarity.
- Masking and enable behavior.
- Pending and clear behavior.
- Priority behavior, if implemented.
- Interrupt aggregation and routing assumptions.
- Reset state.
- Software-visible status.

### 6.6 Sideband interfaces

Sideband signals must be explicitly documented.

Examples include:

- Ready and busy status.
- Error and fault indications.
- Power-state requests and acknowledgements.
- Clock or reset status.
- Performance or activity indicators.
- Configuration straps.

Sideband behavior must not be left implicit.

### 6.7 Debug interfaces

Debug interfaces must identify:

- Debug capability.
- Access method.
- Privilege requirements.
- Reset and power behavior.
- Security restrictions.
- Whether the interface is present in production configuration.

### 6.8 Interface requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-INTERFACE-001 | An IP MUST document every externally visible interface. | MUST | L1 | R | INSPECTION |
| KIP-STD-INTERFACE-002 | Every interface MUST define signal names, widths, directions and clock associations. | MUST | L1 | R | INSPECTION |
| KIP-STD-INTERFACE-003 | Memory-mapped interfaces MUST identify the supported protocol and profile. | MUST | L1 | R | INSPECTION, TEST |
| KIP-STD-INTERFACE-004 | An IP MUST document protocol errors, response behavior and boundary conditions. | MUST | L1 | R | INSPECTION, TEST |
| KIP-STD-INTERFACE-005 | Interrupt interfaces MUST define polarity, trigger behavior and clearing semantics. | MUST | L1 | R | INSPECTION, TEST |
| KIP-STD-INTERFACE-006 | An alternate bus implementation MUST identify the bridge or adapter requirements. | MUST | L1 | R | INSPECTION |
| KIP-STD-INTERFACE-007 | Protocol implementations SHOULD be checked against the applicable protocol profile. | SHOULD | L2 | T | TEST, EVIDENCE |
| KIP-STD-INTERFACE-008 | Debug and sideband interfaces MUST have documented access and behavior. | MUST | L1 | R | INSPECTION |

---

## 7. Clock and reset contract (CLKRST)

### 7.1 Clock naming

Clock signal names must be meaningful and consistent.

Suggested conventions:

- `clk_<domain>_i` for clock input ports.
- `clk_<domain>` for internal clock nets.
- `clk_<domain>_en` for clock enable signals.

Clock names must identify the intended domain where practical.

The standard must not assume that all IPs have a single clock domain.

### 7.2 Clock specification

Each clock domain must identify:

- Clock name.
- Clock source or source assumption.
- Frequency range or operating requirement, if known.
- Clock relationship to other domains.
- Clock enable or gating behavior.
- Clock stability assumptions.
- Reset association.
- Timing constraints required for integration.

Unspecified numerical values must be marked TBD rather than invented.

### 7.3 Reset naming and polarity

The default KRITVA reset convention is active-low.

The standard reset port naming convention is:

`rst_<domain>_n_i`

Active-high reset ports are not permitted by default. An active-high reset
requires an explicitly approved waiver with technical rationale and
identified scope.

Internal reset signals must also use consistent, documented names that
identify their domain and polarity.

### 7.4 Reset behavior

Reset documentation must identify:

- Polarity.
- Assertion behavior.
- Deassertion behavior.
- Synchronous or asynchronous behavior.
- Reset domain.
- Reset sequencing assumptions.
- Reset values of externally visible state.
- Recovery and removal considerations where applicable.

The reset architecture must use the approved KRITVA RTL library manifest
for reset synchronizer implementation.

An IP MUST NOT independently reimplement a reset synchronizer inside
its functional RTL when the approved library provides the required
reset synchronizer component.

### 7.5 Sequential logic

Sequential logic must use positive-edge-triggered clocking by default.

Negative-edge-triggered or other non-default sequential behavior requires
explicit justification and approval through the applicable design review
or waiver process.

### 7.6 CDC and RDC

Clock-domain crossing (CDC) and reset-domain crossing (RDC) behavior must
be explicitly considered.

The IP specification must identify:

- Independent clock domains.
- Data and control crossings.
- Approved synchronizer or crossing modules.
- Handshake or asynchronous FIFO usage.
- Reset interactions across domains.
- Reset release sequencing.
- Any assumptions requiring SoC-level constraints.

Asynchronous crossings must not be introduced through arbitrary
combinational paths.

Crossings must use declared and reviewed crossing structures from the
approved library or other explicitly approved integration components.

CDC/RDC tool support and qualification must be recorded. Where tools
are not qualified, review-only assessment must be explicitly identified;
tool-assisted or automated closure must not be claimed.

### 7.7 CLKRST requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-CLKRST-001 | An IP MUST identify every clock domain. | MUST | L1 | R | INSPECTION |
| KIP-STD-CLKRST-002 | An IP MUST document reset polarity and behavior for each reset domain. | MUST | L1 | R | INSPECTION |
| KIP-STD-CLKRST-003 | Active-low reset signals MUST use the `rst_<domain>_n_i` naming convention for reset input ports. | MUST | L1 | A | INSPECTION |
| KIP-STD-CLKRST-004 | Reset assertion and deassertion behavior MUST be specified. | MUST | L1 | R | INSPECTION, ANALYSIS |
| KIP-STD-CLKRST-005 | Every asynchronous clock-domain crossing MUST use an identified and approved crossing mechanism. | MUST | L2 | T | ANALYSIS, EVIDENCE |
| KIP-STD-CLKRST-006 | Every reset-domain crossing MUST be assessed for reset interaction and release safety. | MUST | L2 | T | ANALYSIS, EVIDENCE |
| KIP-STD-CLKRST-007 | CDC and RDC assumptions MUST be documented for integration. | MUST | L1 | R | INSPECTION |
| KIP-STD-CLKRST-008 | CDC/RDC findings MUST be dispositioned before release qualification. | MUST | L3 | T | EVIDENCE |
| KIP-STD-CLKRST-009 | Reset input ports MUST be active-low unless an active-high reset waiver is approved. | MUST | L1 | A | INSPECTION |
| KIP-STD-CLKRST-010 | Active-high reset usage MUST have an approved waiver with technical rationale and affected-scope identification. | MUST | L1 | R | EVIDENCE |
| KIP-STD-CLKRST-011 | Sequential logic SHOULD use positive-edge-triggered clocking. | SHOULD | L1 | A | INSPECTION |
| KIP-STD-CLKRST-012 | Reset synchronizers MUST be instantiated from the approved KRITVA RTL library manifest. | MUST | L1 | A | INSPECTION |
| KIP-STD-CLKRST-013 | An IP MUST NOT independently reimplement an approved-library reset synchronizer within its functional RTL. | MUST | L1 | A | INSPECTION |

### 7.8 Technology-specific implementation

Synchronizer cells, reset cells and clock-gating cells may be technology
specific.

The portable IP contract must define the required logical behavior.
Technology-specific implementations must be contained in approved
library components or implementation-specific wrappers.

---

## 8. Parameterization and naming (PARAM)

### 8.1 Parameterization

Parameters must be used for documented configuration choices.

Examples include:

- Data width.
- Address width.
- FIFO depth.
- Number of channels.
- Number of ports.
- Feature enablement.
- Optional interface selection.

Every public parameter must identify:

- Name.
- Type.
- Default value.
- Permitted range or enumeration.
- Functional impact.
- Dependency on other parameters.
- Elaboration-time constraints.
- Verification configurations.

### 8.2 Naming conventions

Names should be descriptive and consistent.

The detailed naming rules must be harmonized with the applicable SoC
RTL design profile.

The proposed common port suffix conventions are:

- `_i` for input ports.
- `_o` for output ports.
- `_io` for bidirectional ports.

The exact naming policy and its relationship to the Nexus RTL profile
remain subject to the owner decisions listed in Section 24.

### 8.3 Magic numbers

Unexplained constants and implementation-specific assumptions must not
be embedded in RTL.

Constants should be named and documented.

Parameter-dependent expressions must be written so that supported
configurations elaborate correctly.

### 8.4 Generate constructs

Generate blocks should be used for structural configuration and
parameter-dependent implementation.

Generate logic must not introduce undocumented interfaces or
configuration-dependent behavior.

### 8.5 PARAM requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-PARAM-001 | Every externally configurable parameter MUST be documented. | MUST | L1 | R | INSPECTION |
| KIP-STD-PARAM-002 | Parameters MUST define their type, default and supported values. | MUST | L1 | R | INSPECTION |
| KIP-STD-PARAM-003 | Invalid parameter combinations MUST be detected or explicitly prohibited. | MUST | L2 | A | TEST, ANALYSIS |
| KIP-STD-PARAM-004 | RTL SHOULD use named constants instead of unexplained numeric literals. | SHOULD | L1 | A | INSPECTION |
| KIP-STD-PARAM-005 | Parameter-dependent generate structures MUST elaborate for every supported configuration. | MUST | L2 | A | TEST |
| KIP-STD-PARAM-006 | Public configuration parameters MUST NOT change behavior without documented specification impact. | MUST | L1 | R | INSPECTION |
| KIP-STD-PARAM-007 | Input, output and bidirectional ports SHOULD use `_i`, `_o` and `_io` suffixes respectively. | SHOULD | L1 | A | INSPECTION |

---

## 9. Register specification (REGS)

### 9.1 Register source of truth

SystemRDL is the proposed canonical source for memory-mapped register
definitions.

**PROPOSED — TOOLCHAIN AND POLICY QUALIFICATION REQUIRED**

The intended methodology is:

SystemRDL source → validated register model → generated documentation,
software headers and verification models.

Generated outputs must not become competing manually maintained sources
of truth.

### 9.2 Required register information

Each register and field should define:

- Name.
- Offset.
- Width.
- Reset value.
- Access type.
- Field bit range.
- Software description.
- Hardware behavior.
- Side effects.
- Reserved-field behavior.
- Clock and reset association.
- Interrupt relationships.
- Parameter dependencies.
- Security or privilege restrictions, where applicable.

### 9.3 Access types

The register model must define the applicable access behavior.

Common access types include:

- RW: Read and write.
- RO: Read only.
- WO: Write only.
- W1C: Write one to clear.
- W1S: Write one to set.
- W0C: Write zero to clear.
- W0S: Write zero to set.
- RC: Read to clear.
- Reserved: No functional software access.

Additional access types must be explicitly defined when needed.

Access semantics must not be inferred from register names alone.

### 9.4 Reset values

Reset values must be specified for all architecturally visible register
fields unless the register is explicitly documented as undefined after
reset.

If reset values depend on parameters or modes, those dependencies must
be recorded.

### 9.5 Reserved fields

Reserved fields must have documented read and write behavior.

Software must not depend on unspecified reserved-field values.

Where reserved fields must read as zero or ignore writes, that behavior
must be explicit.

### 9.6 Generated artifacts

The register flow should support generation of:

- Register documentation.
- C headers.
- Machine-readable register descriptions.
- Python register models where appropriate.
- RTL register definitions or integration artifacts where supported.
- UVM-independent verification register models.

The standard does not require UVM.

A UVM-based register model MAY be provided where a project uses UVM,
but the common register specification and basic generated verification
artifacts must not require UVM.

### 9.7 Register consistency

The register source, RTL implementation, generated software headers,
documentation and verification models must remain consistent.

### 9.8 REGS requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-REGS-001 | A memory-mapped IP MUST define its register map. | MUST | L1 | R | INSPECTION |
| KIP-STD-REGS-002 | The register map MUST identify offsets, widths, fields and access behavior. | MUST | L1 | R | INSPECTION |
| KIP-STD-REGS-003 | Reset values MUST be specified for architecturally visible fields or explicitly identified as undefined. | MUST | L1 | R | INSPECTION |
| KIP-STD-REGS-004 | Reserved-field behavior MUST be documented. | MUST | L1 | R | INSPECTION, TEST |
| KIP-STD-REGS-005 | SystemRDL SHOULD be used as the canonical register source. | SHOULD | L1 | A | INSPECTION |
| KIP-STD-REGS-006 | Generated register artifacts MUST identify their source specification version. | MUST | L1 | A | INSPECTION |
| KIP-STD-REGS-007 | Register source and generated artifacts MUST be checked for consistency. | MUST | L2 | A | TEST, EVIDENCE |
| KIP-STD-REGS-008 | Register verification MUST cover applicable access, reset and side-effect behavior. | MUST | L2 | T | TEST, EVIDENCE |

---

## 10. Technology independence (TECH)

### 10.1 General principle

The common IP RTL should be technology independent wherever practical.

The same functional IP should be capable of being evaluated for different
implementation targets without requiring its functional specification
to be rewritten.

Supported implementation targets may include:

- ASIC.
- FPGA.
- Simulation and verification environments.

An IP may have target-specific limitations, but these must be documented.

### 10.2 Approved KRITVA RTL library manifest

The approved KRITVA RTL library manifest is the only permitted technology
boundary for common IP RTL.

It defines the approved reusable implementation components and their
interfaces.

The manifest is expected to identify approved components for:

- CDC synchronizers and crossing structures.
- Reset synchronizers.
- Clock-gating wrappers.
- FIFO implementations and wrappers.
- Memory wrappers.
- Other approved technology-dependent abstractions.

The manifest must identify the component, interface, source location,
version, supported configurations, implementation dependencies and
applicable verification evidence.

A component must not be treated as approved merely because it exists
in a repository.

Its approval status must be identifiable from the approved manifest.

The exact manifest path, schema, approval process and initial component
inventory are TBD.

### 10.3 Vendor primitives

Vendor-specific or foundry-specific cells MUST NOT be instantiated
directly in common functional IP RTL.

Technology-specific implementation must be contained within components
identified by the approved KRITVA RTL library manifest.

No foundry cell or vendor primitive may bypass the approved library
boundary.

### 10.4 Memory abstraction

Memory interfaces must separate the logical memory contract from
the physical memory implementation.

Memory implementations must use approved memory wrappers from the
KRITVA RTL library manifest.

A memory wrapper should define:

- Read and write behavior.
- Port count.
- Data and address width.
- Byte enables, where applicable.
- Read latency.
- Collision behavior.
- Reset and initialization assumptions.
- Target-specific implementation selection.

The threshold for requiring a dedicated memory wrapper, including the
criteria for small inferred memories versus wrapper-based memories,
is TBD and requires owner approval.

### 10.5 Clock-gating abstraction

Clock-gating functionality must use an approved library component or
wrapper.

The abstraction must preserve the intended clock-enable and power behavior.

Technology-specific clock-gating cells must not be instantiated directly
inside functional IP RTL.

### 10.6 Synchronizer abstraction

Synchronizer implementations must use approved components from the
KRITVA RTL library manifest.

The functional crossing contract and verification assumptions must
remain documented.

Reset synchronizers must be sourced from the approved library. An IP
must not create a parallel reset synchronizer implementation inside
its functional RTL.

### 10.7 ASIC and FPGA portability

The common IP contract should preserve ASIC and FPGA portability
where practical.

Target-specific implementations may differ, but they must preserve
the specified functional contract.

Target-specific source files, wrappers and build configurations must
be identifiable and documented.

### 10.8 TECH requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-TECH-001 | Portable functional core RTL MUST NOT directly instantiate vendor-specific or foundry-specific implementation primitives. | MUST | L1 | A | INSPECTION |
| KIP-STD-TECH-002 | Technology-dependent components MUST be selected through the approved KRITVA RTL library manifest. | MUST | L1 | A | INSPECTION |
| KIP-STD-TECH-003 | Memory implementation assumptions MUST be documented. | MUST | L1 | R | INSPECTION |
| KIP-STD-TECH-004 | Clock-gating and synchronizer implementation dependencies MUST be identified. | MUST | L1 | R | INSPECTION |
| KIP-STD-TECH-005 | An IP SHOULD support an ASIC-independent simulation and verification configuration. | SHOULD | L2 | T | TEST |
| KIP-STD-TECH-006 | An IP SHOULD document FPGA portability or explicitly state why an FPGA target is not applicable. | SHOULD | L1 | R | INSPECTION |
| KIP-STD-TECH-007 | Target-specific substitutions MUST preserve the specified functional contract. | MUST | L2 | T | TEST, ANALYSIS |
| KIP-STD-TECH-008 | The approved KRITVA RTL library manifest MUST identify approved component versions and interfaces. | MUST | L1 | A | INSPECTION |
| KIP-STD-TECH-009 | Reset synchronizer implementations MUST be sourced from the approved KRITVA RTL library manifest. | MUST | L1 | A | INSPECTION |
| KIP-STD-TECH-010 | An IP MUST NOT independently reimplement an approved-library component within its functional RTL where the approved component is required. | MUST | L1 | A | INSPECTION |
| KIP-STD-TECH-011 | Memory wrappers MUST follow the approved library manifest and applicable wrapper policy. | MUST | L1 | A | INSPECTION |
| KIP-STD-TECH-012 | Clock-gating implementations MUST use approved library components or wrappers. | MUST | L1 | A | INSPECTION |

---

## 11. Integration hooks (HOOKS)

### 11.1 General principle

An IP must expose or document integration hooks required for its
intended functionality and lifecycle.

Not every hook is mandatory for every IP.

Applicability must be determined from the IP's purpose, architecture,
security requirements and integration environment.

### 11.2 DFT hooks

Where applicable, an IP should provide documented provisions for:

- Scan insertion compatibility.
- Test-mode control.
- Test clock requirements.
- Test reset requirements.
- Memory test access.
- DFT isolation or bypass behavior.
- Test status and observability.

The detailed DFT methodology will be defined by a future KRITVA DFT
standard.

### 11.3 Low-power hooks

Where applicable, an IP should identify:

- Clock enable or gating controls.
- Power-state behavior.
- Isolation requirements.
- Retention requirements.
- Reset behavior across power transitions.
- Wake-up or power acknowledgement signals.

The IP specification must distinguish functional power controls from
technology-specific power implementation.

### 11.4 Debug hooks

Where applicable, debug support should define:

- Status visibility.
- Error capture.
- Trace or event visibility.
- Debug access restrictions.
- Debug behavior under reset and low-power conditions.

### 11.5 Security hooks

Where applicable, an IP should identify:

- Privilege or access controls.
- Secure and non-secure access behavior.
- Configuration protection.
- Debug access policy.
- Error and fault reporting.
- Sensitive-data handling.
- Security reset behavior.

Security requirements must not be inferred solely from the presence
of a security-related IP category.

### 11.6 HOOKS requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-HOOKS-001 | An IP MUST document applicable DFT, low-power, debug and security integration hooks. | MUST | L1 | R | INSPECTION |
| KIP-STD-HOOKS-002 | An IP MUST identify hooks that are NOT_APPLICABLE and provide justification where relevant. | MUST | L1 | R | INSPECTION |
| KIP-STD-HOOKS-003 | Test-mode behavior MUST be documented where test-mode interfaces exist. | MUST | L1 | R | INSPECTION, TEST |
| KIP-STD-HOOKS-004 | Power-state and isolation assumptions MUST be documented where applicable. | MUST | L1 | R | INSPECTION |
| KIP-STD-HOOKS-005 | Security-sensitive interfaces MUST define their access and protection assumptions. | MUST | L1 | R | INSPECTION, ANALYSIS |
| KIP-STD-HOOKS-006 | Optional debug functionality MAY be disabled in production configurations. | MAY | L1 | R | INSPECTION |

---

## 12. Hardware description languages (LANG)

### 12.1 Baseline language

SystemVerilog is the proposed baseline language for new KRITVA-developed
RTL.

The exact supported language subset, compiler compatibility requirements
and lint ruleset remain subject to owner approval.

The standard must prioritize portable, synthesizable RTL and avoid
unnecessary tool-specific language extensions.

### 12.2 Supported source languages

Open-source and commercial IP may originate in languages other than
SystemVerilog.

The standard recognizes:

- Verilog-2001.
- SystemVerilog.
- VHDL.
- Chisel or other hardware construction languages that generate RTL.

The source language alone must not be grounds for rejecting otherwise
suitable third-party IP.

### 12.3 Non-SystemVerilog upstream IP

Non-SystemVerilog upstream IP may be accepted when:

1. Its original source language and toolchain are recorded.
2. Its source and build provenance are retained.
3. The generated or elaborated hardware is reproducible.
4. The IP boundary is documented.
5. A KRITVA-compatible integration wrapper is provided where required.
6. The wrapper and external interface satisfy the KRITVA interface contract.
7. Verification evidence covers the integration boundary and relevant
   functional behavior.

### 12.4 Verilog-2001

Verilog-2001 upstream IP may be retained in its original language.

A SystemVerilog wrapper may provide a standardized KRITVA integration
boundary.

The source should be validated using the qualified tools and language
support profile.

### 12.5 VHDL

VHDL upstream IP may be accepted with an appropriate simulator and
integration strategy.

Where GHDL or another VHDL tool is used, the tool version, source
configuration, build steps and generated artifacts must be recorded.

A wrapper or mixed-language integration boundary must be documented.

### 12.6 Chisel-generated IP

Chisel-generated IP must identify:

- Chisel source revision.
- Generator version.
- Scala and build environment versions where relevant.
- Generation commands and configuration.
- Generated RTL revision or checksum.
- Reproducibility requirements.
- Licence and provenance of generator and generated output.

Generated RTL must be treated as an identifiable build artifact.

### 12.7 Language requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-LANG-001 | New KRITVA-developed RTL SHOULD use SystemVerilog. | SHOULD | L1 | R | INSPECTION |
| KIP-STD-LANG-002 | Every IP MUST identify the source language or languages used. | MUST | L0 | A | INSPECTION |
| KIP-STD-LANG-003 | Non-SystemVerilog IP MUST document its integration boundary and language-specific build requirements. | MUST | L1 | R | INSPECTION |
| KIP-STD-LANG-004 | Generated RTL MUST identify its generator, source revision and reproducible build configuration. | MUST | L1 | A | INSPECTION, EVIDENCE |
| KIP-STD-LANG-005 | Language-specific wrappers MUST preserve the specified functional and interface contract. | MUST | L2 | T | TEST |
| KIP-STD-LANG-006 | The supported language subset and tool compatibility profile MUST be recorded for each qualified toolchain. | MUST | L2 | A | EVIDENCE |

---

## 13. Lint and static analysis (LINT)

### 13.1 Purpose

Lint and static analysis are required to identify RTL quality, portability,
structural and maintainability problems before verification and release.

The lint process should be reproducible and machine-readable.

### 13.2 Ruleset ownership

The KRITVA lint ruleset will be maintained as part of the VLSI standards
and KVRF toolchain.

The ruleset must identify:

- Tool and version.
- Rule identifiers.
- Severity.
- Enabled and disabled rules.
- Waiver policy.
- Baseline and configuration.
- Report format.
- Enforcement class.

The exact lint tool, rule set and severity mapping are TBD.

### 13.3 Waivers

Lint waivers must be explicit and traceable.

Each waiver should include:

- Rule identifier.
- Affected file and location.
- Technical reason.
- Risk assessment.
- Owner.
- Approval.
- Review or expiry condition.

Broad suppressions that hide unrelated violations should be avoided.

### 13.4 LINT requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-LINT-001 | RTL MUST be processed by the applicable qualified lint configuration before release qualification. | MUST | L3 | T | TEST, EVIDENCE |
| KIP-STD-LINT-002 | The lint tool and configuration MUST be identified in the evidence record. | MUST | L2 | A | EVIDENCE |
| KIP-STD-LINT-003 | Lint findings MUST be dispositioned according to their severity. | MUST | L2 | R | INSPECTION, EVIDENCE |
| KIP-STD-LINT-004 | Lint waivers MUST have documented justification and ownership. | MUST | L2 | R | INSPECTION |
| KIP-STD-LINT-005 | The lint ruleset SHOULD be centrally maintained and versioned. | SHOULD | L1 | R | INSPECTION |

---

## 14. Verification requirements (VERIF)

### 14.1 KVRF relationship

The KRITVA Verification Reference Flow (KVRF) defines the common
verification methodology, execution conventions, toolchain, evidence
formats and quality reporting.

This document defines what verification outcomes and evidence are
required for IP compliance.

It does not duplicate KVRF implementation details.

The authoritative verification methodology is maintained under:

`VLSI/verification/KVRF/`

### 14.2 Verification planning

Every IP claiming L1 or higher must have an IP-specific verification plan.

The plan must identify:

- Features and requirements under verification.
- Applicable verification activities.
- Test scenarios.
- Assertions or properties where applicable.
- Functional coverage objectives.
- Code coverage objectives where applicable.
- Regression configuration.
- Formal verification applicability.
- Exclusions and waivers.
- Evidence expected for release.

### 14.3 Verification activities

Applicable activities may include:

- RTL syntax and elaboration.
- Lint and structural analysis.
- Directed simulation.
- Randomized simulation.
- Functional coverage.
- RTL code coverage.
- Register verification.
- Protocol checking.
- Assertions.
- Formal verification.
- CDC/RDC analysis.
- Synthesis checks.
- Integration verification.

An activity may be marked NOT_APPLICABLE only with documented technical
justification and required review approval.

### 14.4 Evidence by compliance level

| Compliance level | Minimum expected evidence |
|---|---|
| L0 Registered | IP manifest, identity, source category, repository reference and provenance |
| L1 Evaluated | Documented functionality and major interfaces, source baseline, applicable requirement list, known limitations, basic functional, lint or structural evaluation results (or recorded pending status), provenance and licence assessment for third-party IP, adoption or continuation decision. A full specification package (feature list, interface definition, parameter description, register definition where applicable) and verification plan are expected by L2 |
| L2 Verified | Applicable verification results, regression summary, functional and code coverage reports where required, lint results, applicable assertions/formal/CDC/RDC results, traceable evidence |
| L3 Release-qualified | L2 evidence, approved deviations, quality assessment, release package, licence review, reproducible release source and applicable integration qualification evidence |

Evidence requirements may be more stringent for safety-critical,
security-sensitive or complex IP.

### 14.5 Commit-bound evidence

Verification evidence must identify the exact source revision assessed.

Where applicable, evidence must also identify:

- Testbench revision.
- Tool versions.
- Tool configuration.
- Parameter configuration.
- Test selection.
- Random seed.
- Execution environment.
- Run identifier.
- Execution date.
- Result.
- Report or artifact reference.
- Artifact checksum.
- Reviewer or approval reference.

A result produced against an earlier source commit must not be presented
as verification evidence for a different release without an impact
assessment and appropriate rerun.

### 14.6 Verification requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-VERIF-001 | An IP MUST have a verification plan before claiming L1 compliance. | MUST | L1 | R | INSPECTION |
| KIP-STD-VERIF-002 | Verification activities MUST be mapped to applicable features and requirements. | MUST | L2 | A | INSPECTION, EVIDENCE |
| KIP-STD-VERIF-003 | Required verification activities MUST pass before claiming L2 compliance. | MUST | L2 | A | TEST, EVIDENCE |
| KIP-STD-VERIF-004 | Verification evidence MUST identify the assessed source commit. | MUST | L2 | A | EVIDENCE |
| KIP-STD-VERIF-005 | Verification tools and configurations MUST be recorded. | MUST | L2 | A | EVIDENCE |
| KIP-STD-VERIF-006 | Functional and code coverage objectives MUST be defined where applicable. | MUST | L2 | R | INSPECTION, EVIDENCE |
| KIP-STD-VERIF-007 | Coverage exclusions MUST have documented justification. | MUST | L2 | R | INSPECTION |
| KIP-STD-VERIF-008 | Formal, CDC and RDC activities MUST be assessed for applicability. | MUST | L2 | R | ANALYSIS |
| KIP-STD-VERIF-009 | A verification result MUST NOT be reused for a changed source revision without an impact assessment. | MUST | L2 | R | EVIDENCE |
| KIP-STD-VERIF-010 | Release qualification MUST use evidence associated with the exact release candidate. | MUST | L3 | A | EVIDENCE |
| KIP-STD-VERIF-011 | New KRITVA-developed IP at L2 and above MUST use the KVRF reference flow (Python, cocotb, SystemVerilog) unless an equivalent flow is used under KIP-STD-VERIF-012. | MUST | L2 | T | INSPECTION, EVIDENCE |
| KIP-STD-VERIF-012 | An equivalent verification flow MUST produce evidence records conforming to the applicable KVRF evidence schema. | MUST | L2 | A | EVIDENCE |
| KIP-STD-VERIF-013 | Upstream or third-party IP MAY retain its native testbench; a wrapper-level KVRF test or equivalent evidence-producing integration test SHOULD be provided for KRITVA integration behavior. | SHOULD | L2 | R | INSPECTION |

### 14.7 Reference flow and equivalent flows

This standard is outcome and evidence based. KVRF with cocotb is the
default reference flow for new KRITVA-developed IP at L2 and above.
Equivalent flows (for example a Verilator-based or hardware-assisted flow
used by a SoC profile) are acceptable when they emit evidence records
conforming to the KVRF evidence schema.

Upstream or third-party IP may keep its native testbench. Native evidence
and wrapper-level KVRF evidence must be distinguishable in the evidence
package.

Verification tool versions are UNVERIFIED unless independently established.
The authoritative definitions are in `VLSI/verification/KVRF/KVRF_SPECIFICATION.md`.

---

## 15. Quality assessment (QUALITY)

### 15.1 Quality dimensions

An IP quality assessment should consider the following dimensions.

| Dimension | Proposed weight |
|---|---:|
| Functional completeness | 20 |
| RTL/design quality | 15 |
| Verification quality | 20 |
| Documentation | 15 |
| Integration readiness | 15 |
| Synthesis/implementation readiness | 10 |
| Maintainability and reusability | 5 |
| **Total** | **100** |

These weights are PROPOSED and require owner approval.

### 15.2 Scoring

A proposed scoring scale is:

| Score | Meaning |
|---|---|
| 0 | Not implemented or unacceptable |
| 1 | Initial or substantially incomplete |
| 2 | Partially implemented |
| 3 | Meets basic documented expectations |
| 4 | Meets expectations with strong evidence |
| 5 | Fully meets expectations with complete evidence |

A missing assessment or missing evidence must be recorded as
NOT_ASSESSED, not automatically assigned a score of zero.

### 15.3 Quality gates

A high quality score cannot compensate for a failed mandatory release gate.

Release qualification requires all applicable hard gates to pass.

The quality policy and detailed scoring procedure will be maintained
with the KVRF quality specification and related IP policies.

### 15.4 QUALITY requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-QUALITY-001 | An IP claiming L3 compliance MUST have an approved quality assessment. | MUST | L3 | R | EVIDENCE |
| KIP-STD-QUALITY-002 | Quality dimensions and assessment results MUST be traceable to evidence. | MUST | L3 | R | INSPECTION, EVIDENCE |
| KIP-STD-QUALITY-003 | Missing evidence MUST NOT be represented as a successful assessment. | MUST | L3 | A | INSPECTION |
| KIP-STD-QUALITY-004 | Mandatory release gates MUST be evaluated independently of any aggregate quality score. | MUST | L3 | R | EVIDENCE |

---

## 16. Package and manifest requirements (PKG)

### 16.1 Package structure

An IP repository or release package should use a consistent structure.

The following is a reference layout. Additional directories may be added
according to the IP category.

~~~text
kritva-ip-<name>/
├── README.md
├── LICENSE
├── THIRD_PARTY_NOTICES
├── CHANGELOG.md
├── MANIFEST.yaml
│
├── documentation/
│   ├── IP_OVERVIEW.md
│   ├── FUNCTIONAL_SPEC.md
│   ├── INTERFACE_SPEC.md
│   ├── INTEGRATION_GUIDE.md
│   └── LIMITATIONS.md
│
├── rtl/
│   ├── src/
│   └── wrappers/
│
├── registers/
│   └── register_spec.rdl
│
├── verification/
│   ├── VERIFICATION_PLAN.md
│   ├── feature_traceability.yaml
│   ├── cocotb/
│   ├── formal/
│   ├── lint/
│   └── regression/
│
├── quality/
│
├── integration/
│   ├── nexus/
│   └── edge/
│
├── upstream/
│   └── UPSTREAM_MANIFEST.yaml
│
└── customization/
    └── CUSTOMIZATION_REGISTER.yaml
~~~

Directories that do not apply to an IP may be omitted with appropriate
documentation.

### 16.2 IP manifest

Every managed IP must have a machine-readable manifest.

The manifest must identify:

- Schema version.
- IP identifier and name.
- Category.
- Source category.
- Owner.
- Repository.
- Release version.
- Standard version.
- Specification version.
- Supported configurations.
- Source language.
- Licence and SPDX identifier.
- Upstream baseline where applicable.
- Verification and quality references.
- SoC applicability.
- Release status.

The exact manifest schema is maintained under:

`VLSI/ip-standard/schemas/`

### 16.3 Licence files

Every IP package must identify its applicable licence.

Internal IP must identify its approved licensing arrangement.

Open-source IP must preserve the upstream licence and required notices.

Commercial IP must identify the applicable controlled licence reference
without disclosing confidential contract details in public metadata.

Where third-party material is included, applicable notices must be
preserved in `THIRD_PARTY_NOTICES` or equivalent approved records.

SPDX identifiers SHOULD be used wherever an applicable SPDX identifier
exists.

### 16.4 PKG requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-PKG-001 | Every IP MUST have a machine-readable manifest. | MUST | L0 | A | INSPECTION |
| KIP-STD-PKG-002 | The manifest MUST identify the IP, source category, version and owner. | MUST | L0 | A | INSPECTION |
| KIP-STD-PKG-003 | Every IP package MUST identify its applicable licence. | MUST | L0 | A | INSPECTION |
| KIP-STD-PKG-004 | Third-party licence notices and attribution MUST be preserved. | MUST | L0 | R | INSPECTION |
| KIP-STD-PKG-005 | SPDX identifiers SHOULD be used where applicable. | SHOULD | L0 | A | INSPECTION |
| KIP-STD-PKG-006 | The release package MUST identify the applicable standard and schema versions. | MUST | L3 | A | INSPECTION |
| KIP-STD-PKG-007 | The package MUST include sufficient documentation to reproduce its declared build and verification process. | MUST | L3 | R | EVIDENCE |

---

## 17. Release qualification (RELEASE)

### 17.1 Release lifecycle

An IP release should follow the lifecycle:

- DRAFT
- UNDER_REVIEW
- APPROVED
- RELEASED
- DEPRECATED
- SUPERSEDED

The detailed lifecycle, release authority and transition rules are
defined in `IP_LIFECYCLE_POLICY.md`.

### 17.2 Mandatory release gates

An IP cannot claim L3 Release-qualified status unless all applicable
hard gates pass.

| Gate | Requirement |
|---|---|
| Identity | Stable IP identity and release version |
| Provenance | Source origin and revision identified |
| Licensing | Rights and redistribution obligations reviewed |
| Specification | Applicable specification approved |
| Interface | Interface contract documented and reviewed |
| Parameters | Supported configurations identified |
| Registers | Register source and generated artifacts consistent, where applicable |
| Lint | Required lint findings dispositioned |
| Verification | All required verification activities passed |
| CDC/RDC | Applicable crossings reviewed and findings dispositioned |
| Defects | No unresolved critical defects |
| Deviations | All deviations and waivers approved |
| Quality | Quality assessment approved |
| Packaging | Release package complete |
| Evidence | Evidence tied to the exact release candidate |
| Integration | Applicable integration profile assessed and approved |
| Approval | Authorized release approval recorded |

### 17.3 Release requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-RELEASE-001 | A released IP MUST have a unique immutable release identity. | MUST | L3 | A | INSPECTION |
| KIP-STD-RELEASE-002 | All mandatory release gates MUST pass before release qualification. | MUST | L3 | A | EVIDENCE |
| KIP-STD-RELEASE-003 | Release evidence MUST identify the exact source revision. | MUST | L3 | A | EVIDENCE |
| KIP-STD-RELEASE-004 | Release approval MUST identify the authorized approver and approval record. | MUST | L3 | R | EVIDENCE |
| KIP-STD-RELEASE-005 | A released IP MUST identify its known limitations and applicable integration restrictions. | MUST | L3 | R | INSPECTION |
| KIP-STD-RELEASE-006 | A released IP MUST NOT be modified in place. | MUST | L3 | A | INSPECTION |

---

## 18. Public information and security (SEC-PUB)

### 18.1 Public repository rule

`kritva-standard` is a public repository.

All content must be assessed for publication suitability before merging.

No unreleased Nexus or Edge architecture, implementation details,
configuration data, proprietary RTL, confidential vendor documentation
or internal engineering review comments may be published without explicit
authorization and applicable legal clearance.

### 18.2 Public-safe IP information

Information that may be published, subject to approval, includes:

- Generic IP identity and category.
- Approved IP descriptions.
- Public source references.
- Approved licence identifiers.
- Publicly distributable specification content.
- Approved verification and quality summaries.
- Generic SoC consumer applicability.
- Released IP versions and release notes.

### 18.3 Restricted information

The following must remain in controlled engineering repositories unless
explicitly approved for public release:

- Unreleased Nexus and Edge architecture.
- Detailed SoC topology and implementation choices.
- Internal address maps and configuration details.
- Confidential performance, power and area targets.
- Security architecture and restricted security findings.
- Proprietary vendor reports and licensed source.
- Internal verification logs and review comments.
- Confidential defects and incident records.
- Private CI artifacts and restricted evidence links.

### 18.4 Publication review

Public-content review must follow the repository governance policy.

The review includes:

- Confidentiality inspection.
- Licence and attribution inspection.
- Secret scanning.
- Architecture denylist checks.
- Private URL checks.
- Registry-field allowlist validation.
- Public link validation.
- Human publication review.

Passing automated checks does not constitute authorization to publish.

### 18.5 SEC-PUB requirements

| Requirement ID | Requirement | Level | Applies from | Enforcement | Assessment |
|---|---|---|---|---|---|
| KIP-STD-SEC-PUB-001 | Public IP records MUST contain only approved public metadata. | MUST | L0 | A | INSPECTION |
| KIP-STD-SEC-PUB-002 | Unreleased Nexus or Edge architecture MUST NOT be published without explicit authorization. | MUST | L0 | R | INSPECTION |
| KIP-STD-SEC-PUB-003 | Proprietary or restricted vendor material MUST NOT be redistributed without applicable rights. | MUST | L0 | R | INSPECTION |
| KIP-STD-SEC-PUB-004 | Public evidence links MUST NOT expose private or restricted artifacts. | MUST | L2 | A | INSPECTION |
| KIP-STD-SEC-PUB-005 | Public-content review MUST be completed before merging a contribution. | MUST | L0 | R | EVIDENCE |
| KIP-STD-SEC-PUB-006 | Automated publication checks MUST NOT be treated as a substitute for human approval. | MUST | L0 | R | INSPECTION |

---

## 19. SoC consumer profiles

### 19.1 General principle

The common IP specification must be independent of a particular SoC.

An IP may be consumed by multiple SoCs using separate integration profiles.

The generic consumer-profile descriptions are maintained in:

`VLSI/README.md`, Section 5.

This document does not establish detailed SoC architecture or final IP
selection.

### 19.2 Nexus profile

KRITVA Nexus is an existing SoC engineering project with its own
repository and approved SoC-specific RTL design standard.

The Nexus integration profile must reference the applicable Nexus
repository documents and decision records.

The common KRITVA IP Standard does not replace the Nexus SoC-specific
design contract.

The Nexus-specific integration profile must identify, as applicable:

- Consumer SoC identity and profile version.
- IP identifier and selected IP release.
- Applicable common IP Standard version.
- Applicable Nexus RTL design standard version.
- Enabled features.
- Parameter overrides.
- Native and adapted interfaces.
- Bus connectivity.
- Address allocation.
- Clock connections and constraints.
- Reset connections and sequencing.
- Interrupt routing.
- DMA and peripheral connectivity.
- Memory and storage dependencies.
- Power and isolation requirements.
- DFT and debug configuration.
- Security and privilege configuration.
- CDC/RDC constraints.
- Timing requirements.
- Integration verification plan.
- Integration evidence and approval.

### 19.3 Edge profile

KRITVA Edge is a planned SoC consumer profile.

The `kritva-edge` SoC repository has not yet been started. Therefore,
the Edge profile in this standard is a placeholder and does not represent
an approved architecture, implementation or integration configuration.

When the Edge repository and its SoC-specific standards are established,
the Edge integration profile must identify, as applicable:

- Consumer SoC identity and profile version.
- IP identifier and selected IP release.
- Applicable common IP Standard version.
- Edge-specific design and integration standards.
- Enabled features.
- Parameter overrides.
- Native and adapted interfaces.
- Bus connectivity.
- Address allocation.
- Clock connections and constraints.
- Reset connections and sequencing.
- Interrupt routing.
- DMA and peripheral connectivity.
- Memory dependencies.
- Power and isolation requirements.
- DFT and debug configuration.
- Security configuration.
- CDC/RDC constraints.
- Timing requirements.
- Integration verification plan.
- Integration evidence and approval.

### 19.4 Shared and SoC-specific IP

An IP may be classified as:

- COMMON: potentially applicable to multiple KRITVA SoCs.
- NEXUS: intended for the Nexus consumer profile.
- EDGE: intended for the Edge consumer profile.
- CONDITIONAL: applicability depends on a defined configuration.
- NOT_APPLICABLE: not intended for the relevant consumer, with justification.

These classifications describe engineering applicability only.

They do not imply a completed SoC design, approved architecture, programme
baseline or programme execution status.

---

## 20. Relationship to KNX-RTL-STD-001

### 20.1 Purpose and authority

KRITVA IP Standard is the cross-SoC baseline for reusable semiconductor IP.

KRITVA Nexus maintains its own SoC-specific RTL Design Standard:

`KNX-RTL-STD-001`, version 1.0.1.

The Nexus standard is an approved Nexus-specific design profile.
It is not replaced by this common standard.

The common IP Standard defines reusable cross-SoC requirements.
The Nexus RTL Design Standard defines additional Nexus-specific
implementation requirements.

Where an applicable Nexus requirement is stricter than the common
KRITVA IP requirement, the stricter Nexus requirement prevails for
Nexus IP implementation and integration.

A common-standard requirement does not authorize an IP to violate
the applicable Nexus design profile.

This relationship does not automatically promote every Nexus-specific
rule into the cross-SoC standard.

### 20.2 Requirement language and enforcement

Owner decisions of 2026-11-12:

- Common KRITVA standards use RFC 2119 MUST. Where the Nexus standard uses
  SHALL, SHALL has the same normative force as MUST.
- Separate namespaced identifier schemes are retained: `KIP-STD-<AREA>-NNN`
  for common standards and `KNX-RTL-<CAT>-NNN` for the Nexus profile, with
  a separate Edge scheme to be defined later. Identifiers are never
  renumbered.
- The A/T/R enforcement classes (Automated, Tool-assisted, Review only) are
  adopted as-is across common standards and profiles.

Cross-reference rules:

- Existing Nexus rule identifiers must be retained in the Nexus repository.
- Common IP Standard requirement identifiers must remain stable.
- A cross-reference must not imply that two differently worded requirements
  are identical.
- A Nexus-specific rule remains applicable to Nexus according to the
  approved Nexus standard.
- A rule promoted into the common standard gets a new `KIP-STD` identifier
  with a `derived-from` reference.

The per-rule mapping between the schemes uses one of four relationship
values:

| Value | Meaning |
|---|---|
| EQUIVALENT | The profile rule and common requirement have the same intent and strength. |
| STRICTER | The profile rule is stricter; the stricter rule prevails for that SoC. |
| NEXUS_ONLY | The profile rule has no common counterpart and remains profile-specific. |
| PROMOTED | The profile rule has been promoted into the common standard under a new `KIP-STD` identifier that records the original profile rule ID as its `derived-from` reference. |

The detailed per-rule mapping table is maintained with the Nexus profile
in the private repository that owns that profile, and is tracked as
IPSTD-OI-010. This public standard describes only the mapping methodology and
area-level relationships; it does not publish profile rule IDs, per-rule
relationships, or private profile details. The public template
`../templates/requirement-id-mapping.template.yaml` (KIP-MAP-001) defines the
mapping record structure for use in that private repository.

### 20.3 Mapping by requirement area

The following is an area-level cross-reference only. It does not copy,
replace or reinterpret the normative text of KNX-RTL-STD-001.

| KRITVA IP Standard area | KNX-RTL-STD-001 category |
|---|---|
| SPEC | SPC |
| PARAM | NAM |
| PKG | FIL, LIB |
| PARAM | COD |
| CLKRST | RST |
| CLKRST | CLK |
| HOOKS | LPW |
| TECH | LIB, MEM |
| CLKRST | CDC |
| VERIF | VER |
| INTERFACE | INT |
| QUALITY | DOC |
| RELEASE | GOV |
| SEC-PUB | GOV |

This mapping is an initial cross-reference and requires owner review.
It is not a claim that the listed categories have identical scope or
requirement coverage.

Categories in the Nexus standard without an explicit common-standard
counterpart remain governed by the Nexus profile for Nexus implementation.

### 20.4 Nexus enforcement classification

The Nexus standard identifies enforcement classes:

- A: Automated.
- T: Tool-assisted.
- R: Review only.

This common IP Standard includes an Enforcement attribute in its
requirement tables to support alignment.

The enforcement class in this document is an assessment attribute.
It does not replace the Nexus rule's own enforcement definition or
automatically establish tool qualification.

### 20.5 Approved library boundary

The approved KRITVA RTL library manifest is the technology boundary
for reusable IP implementation.

Nexus-specific approved library components and their implementation
requirements must be respected by IP consumed by Nexus.

The common standard does not independently approve or redefine the
Nexus library manifest.

### 20.6 Change coordination

A change to this common standard that affects a Nexus integration
requirement must be assessed for compatibility with KNX-RTL-STD-001.

A change to KNX-RTL-STD-001 that affects common IP requirements should
be evaluated for possible promotion into the cross-SoC standard.

Neither change automatically modifies the other document.

---

## 21. Integration readiness

A proposed integration readiness scale is:

| Level | Meaning |
|---|---|
| IR0 | IP identified |
| IR1 | Interface specification available |
| IR2 | Consumer configuration defined |
| IR3 | Connectivity and elaboration validated |
| IR4 | Integration verification passed |
| IR5 | SoC integration approved |

The detailed integration readiness methodology remains subject to
development and approval.

An integration profile must identify the applicable IP release and
standard versions.

Integration readiness is separate from the IP's compliance level.
An IP may be verified independently but not yet integrated into a
particular SoC.

---

## 22. Compliance assessment and statement

### 22.1 Assessment process

An IP compliance assessment must:

1. Identify the IP and assessed revision.
2. Identify the applicable standard version.
3. Determine the claimed compliance level.
4. Identify applicable requirements.
5. Assess each requirement using its specified method.
6. Record the enforcement class and actual assessment evidence.
7. Record NOT_APPLICABLE decisions with justification.
8. Record deviations and waivers.
9. Calculate the achieved compliance level.
10. Obtain the required review and approval.

A compliance level may only be claimed when all mandatory applicable
requirements for that level and all lower levels have been satisfied.

### 22.2 Compliance statement template

~~~yaml
schema_version: "0.1.0"

compliance:
  ip_id: KIP-<CAT>-<NNN>
  ip_name: TBD
  ip_release: TBD
  source_commit: TBD

  standard:
    document_id: KSTD-IPSTD-001
    version: "0.1.0"
    status: DRAFT

  claimed_level: TBD
  achieved_level: TBD

  assessment:
    date: TBD
    assessor: TBD
    reviewer: TBD
    approver: TBD
    status: NOT_ASSESSED

  requirements:
    total_applicable: TBD
    pass: TBD
    fail: TBD
    not_applicable: TBD
    deviation_approved: TBD
    not_assessed: TBD

  enforcement:
    automated: TBD
    tool_assisted: TBD
    review_only: TBD

  evidence:
    index: TBD
    source_revision: TBD
    verification_report: TBD
    quality_report: TBD

  deviations:
    register: TBD

  approval:
    status: PENDING
    reference: TBD
    commit: TBD
~~~

This is an illustrative template. It is not a finalized machine-readable
schema. The authoritative schema will be maintained separately.

---

## 23. Deviation and waiver process

### 23.1 General policy

A deviation is a documented departure from a requirement.

A waiver is an explicitly approved exception for a defined scope and
period or release.

A deviation or waiver must not silently change the normative requirement.

### 23.2 Required deviation information

Each deviation must record:

- Deviation ID.
- Requirement ID.
- IP identifier.
- Affected release or source revision.
- Description of the deviation.
- Technical reason.
- Impact and risk assessment.
- Compensating controls.
- Verification impact.
- Requested duration or expiry.
- Owner.
- Reviewer.
- Approval record.

### 23.3 Approval

The owner or authorized approver must explicitly approve a deviation
before it is accepted for a compliance or release claim.

A waiver does not automatically establish compliance.

The compliance record must identify the deviation and its approval.

### 23.4 Prohibited waivers

A waiver must not be used to bypass:

- Legal licence restrictions.
- Public confidentiality requirements.
- Secret-handling requirements.
- Mandatory security controls where doing so would create unacceptable risk.
- A failed release gate without an approved risk disposition.

### 23.5 Reassessment

Deviations must be reviewed when:

- The IP release changes.
- The affected requirement changes.
- The implementation or integration context changes.
- New evidence changes the risk assessment.
- The waiver reaches its expiry date.

---

## 24. Open Items — owner decisions required

The following decisions are tracked here. Items marked DECIDED record owner
decisions of 2026-11-12 and are retained for traceability.

No item in this table should be treated as an approved architecture or
implementation decision.

| ID | Open decision | Current proposal or question | Owner | Status |
|---|---|---|---|---|
| IPSTD-OI-001 | Primary memory-mapped control/register bus | APB decided as primary bus (2026-11-12); APB revision and KRITVA profile remain to be confirmed | Dinesh Annayya | PARTIALLY DECIDED |
| IPSTD-OI-002 | Allowed alternate bus profiles and bridge policy | Confirm AXI4, AXI4-Lite, AHB-Lite and Wishbone support and bridge requirements | Dinesh Annayya | OPEN |
| IPSTD-OI-003 | SystemVerilog language subset | Define synthesizable and verification language subsets and harmonize with KNX-RTL-STD-001 | Dinesh Annayya | OPEN |
| IPSTD-OI-004 | Lint tool and ruleset | Select tools, rule ownership, severities and waiver policy; harmonize with KNX-RTL-STD-001 | Dinesh Annayya | OPEN |
| IPSTD-OI-005 | Requirement language harmonization | DECIDED (2026-11-12): common standards use RFC 2119 MUST; SHALL in profiles has equivalent force | Dinesh Annayya | DECIDED |
| IPSTD-OI-006 | Requirement identifier harmonization | DECIDED (2026-11-12): separate namespaced schemes retained (KIP-STD, KNX-RTL, future Edge); EQUIVALENT/STRICTER/NEXUS_ONLY mapping; no renumbering | Dinesh Annayya | DECIDED |
| IPSTD-OI-007 | Enforcement-class harmonization | DECIDED (2026-11-12): A/T/R enforcement classes adopted as-is | Dinesh Annayya | DECIDED |
| IPSTD-OI-008 | KVRF methodology relationship | DECIDED (2026-11-12): KVRF/cocotb is the default reference flow for new KRITVA-developed IP at L2+; equivalent flows (including a SoC profile's own flow) are allowed if they emit KVRF-schema evidence; upstream IP may keep native testbenches plus a wrapper-level KVRF test | Dinesh Annayya | DECIDED |
| IPSTD-OI-009 | Copyright holder wording | DECIDED (2026-11-12): copyright holder wording is `Kritva Robotics` for KRITVA-authored files; upstream notices are never replaced. Relationship to repository-level licensing remains to be documented | Dinesh Annayya | DECIDED |
| IPSTD-OI-010 | Promotion of Nexus RTL rules | PARTIALLY DECIDED (2026-11-13): populated per-rule mapping is kept in the private kritva-nexus repository; public template `requirement-id-mapping.template.yaml` added. Still open: identify which KNX-RTL-STD-001 rules should be promoted into the cross-SoC KRITVA IP Standard | Dinesh Annayya | OPEN |
| IPSTD-OI-011 | Approved RTL library manifest | Confirm manifest location, schema, ownership, approval process and initial component inventory | Dinesh Annayya | OPEN |
| IPSTD-OI-012 | Memory-wrapper threshold | Define when a memory implementation must use an approved library wrapper rather than inferred RTL | Dinesh Annayya | OPEN |
| IPSTD-OI-013 | Quality assessment weights | Review and approve or revise proposed quality dimensions and weights | Dinesh Annayya | OPEN |
| IPSTD-OI-014 | L1 definition alignment | PROPOSED (2026-11-13): L1 is "Evaluated / Basic evidence", matching LCP section 6.3 and the KVRF Specification; the specification package and verification plan move to L2 expectations. Owner approval required | Dinesh Annayya | OPEN |
| IPSTD-OI-014 | Compliance assessment authority | Confirm review and approval responsibilities for L0–L3 assessments | Dinesh Annayya | OPEN |
| IPSTD-OI-015 | Register source and generation toolchain | Confirm SystemRDL as canonical source and qualify generation tools | Dinesh Annayya | OPEN |
| IPSTD-OI-016 | ASIC and FPGA portability expectations | Define mandatory targets and acceptable implementation-specific exceptions | Dinesh Annayya | OPEN |
| IPSTD-OI-017 | DFT and low-power hooks | Define the minimum common interface and documentation expectations | Dinesh Annayya | OPEN |

Open items must be resolved through explicit owner decisions and recorded
in an approved revision or associated decision record.

SoC architecture decisions are tracked in the SoC repositories
(`kritva-nexus` decision records; `kritva-edge` repository not yet started).

---

## 25. Relationship to other standards

This document establishes the common IP engineering contract.
Detailed lifecycle and implementation procedures are maintained in
separate documents.

| Related document | Relationship to this standard |
|---|---|
| `OPEN_SOURCE_IP_POLICY.md` | Licensing, provenance and redistribution requirements for open-source IP |
| `IP_ADOPTION_PROCESS.md` | Discovery, evaluation and initial adoption of IP |
| `IP_CUSTOMIZATION_POLICY.md` | KRITVA modifications, wrappers, patches and deviation management |
| `IP_UPSTREAM_MAINTENANCE_POLICY.md` | Upstream release, commit, security and licence monitoring |
| `IP_LIFECYCLE_POLICY.md` | IP lifecycle states, approvals and release transitions |
| KVRF specification | Verification execution methodology and toolchain |
| KVRF verification policy | Verification activities and required outcomes |
| KVRF coverage policy | Functional and code coverage methodology |
| KVRF evidence policy | Evidence structure, traceability and reproducibility |
| KVRF quality policy | Quality assessment methodology |
| IP manifest schema | Machine-readable IP identity and metadata |
| Verification evidence schema | Machine-readable verification evidence |
| Quality result schema | Machine-readable quality assessment |

The related documents may add requirements within their defined scope.
They must not silently contradict this standard.

Conflicts must be resolved through a reviewed standards change.

---

## 26. Document maintenance

This standard must be reviewed when:

- A normative requirement changes.
- A new IP category is introduced.
- A new interface profile is approved.
- Language or toolchain requirements change.
- A compliance level or assessment method changes.
- A new SoC consumer profile is approved for public publication.
- A related standard introduces a conflicting requirement.
- A security, licensing or publication incident identifies a standards gap.
- The relationship with a SoC-specific RTL design standard changes.

Requirement identifiers must remain stable unless a requirement is
formally retired.

Changes must follow repository governance and semantic versioning.

---

## 27. Approval record

| Field | Value |
|---|---|
| Document ID | KSTD-IPSTD-001 |
| Version | 0.1.0 |
| Status | DRAFT |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Approver | Dinesh Annayya (`dineshannayya`) |
| Approval date | PENDING |
| Approval commit | PENDING |
| Open owner decisions | 12 (5 decided; IPSTD-OI-001 partially decided) |

**Approval statement:** This document is not an approved KRITVA IP
engineering baseline until Dinesh Annayya explicitly approves version
0.1.0 and the approval is recorded against the applicable repository
commit.

---

**End of document**
