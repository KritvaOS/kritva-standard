# KRITVA VLSI Engineering Standards

| Field | Value |
|---|---|
| Document ID | KSTD-VLSI-001 |
| Document | VLSI Domain Index |
| Repository | `KritvaOS/kritva-standard` |
| Version | 0.1.0 |
| Status | DRAFT |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Last Updated | 2026-11-12 |

> **Status notice:** This document is DRAFT and defines the organization
> and intended scope of the KRITVA VLSI engineering standards domain.
> It becomes normative only after explicit approval by the authorized
> KRITVA owner.

---

## 1. Purpose

The VLSI domain defines common engineering standards and reusable
methodologies for specifying, developing, verifying, assessing, maintaining
and integrating semiconductor IP within the KRITVA project.

It establishes a common engineering framework for:

- KRITVA-developed internal IP.
- Adopted and customized open-source IP.
- Commercial and licensed third-party IP.

The standards are intended to support multiple KRITVA SoC consumers while
maintaining a consistent IP identity, specification, verification record,
quality assessment and release history.

The guiding principle is:

**One IP identity → One specification → One verification record → One
quality assessment → Multiple SoC integration profiles.**

The IP implementation and its SoC-specific integration configurations
remain in their respective engineering repositories.

## 2. VLSI domain organization

The VLSI domain is organized into three primary areas:

1. IP Standard.
2. IP Registry.
3. Verification Reference Flow (KVRF).

~~~text
VLSI/
├── README.md
│
├── ip-standard/
│   ├── README.md
│   ├── standard/
│   ├── schemas/
│   ├── templates/
│   ├── policies/
│   ├── examples/
│   └── tools/
│
├── ip-registry/
│   ├── README.md
│   ├── public-catalog/
│   ├── schemas/
│   ├── examples/
│   └── reports/
│
├── verification/
│   └── KVRF/
│       ├── README.md
│       ├── specification/
│       ├── toolchain/
│       ├── runners/
│       ├── coverage/
│       ├── evidence/
│       ├── quality/
│       ├── workflows/
│       ├── examples/
│       └── tests/
│
├── design/                 # Future domain - not yet defined
├── physical-design/        # Future domain - not yet defined
├── timing/                 # Future domain - not yet defined
└── DFT/                    # Future domain - not yet defined
~~~

This is the intended organization. A listed directory does not imply
that its standards, tools or workflows have been implemented or approved.

## 3. VLSI domain components

### 3.1 IP Standard

**Location:** `VLSI/ip-standard/`

Defines the common engineering contract for KRITVA semiconductor IP.

Its scope includes:

- IP identity and classification.
- Normative design requirements.
- Functional and feature specifications.
- Interface and protocol specifications.
- Clock, reset and CDC requirements.
- Parameterization and naming conventions.
- Register specification and management.
- Technology independence and portability.
- Interrupt, DFT and low-power integration hooks.
- Verification and quality requirements.
- IP packaging and release requirements.
- Open-source and commercial IP adoption policies.

The IP Standard is the authoritative reference for determining whether
an IP package complies with KRITVA engineering requirements.

### 3.2 IP Registry

**Location:** `VLSI/ip-registry/`

Maintains the public catalogue of approved and publishable KRITVA IP
metadata.

The registry is intended to provide:

- Stable IP identifiers.
- IP names and classifications.
- Source categories.
- Public repository references.
- Published IP versions.
- Applicable standard versions.
- Approved public verification and quality summaries.
- Approved public lifecycle information.
- Generic SoC applicability information.

The public registry must not contain confidential engineering records,
proprietary vendor information, unreleased architecture details or
restricted verification evidence.

Detailed internal engineering records remain in the relevant IP
repositories or controlled storage.

### 3.3 KRITVA Verification Reference Flow (KVRF)

**Location:** `VLSI/verification/KVRF/`

KVRF defines the reusable verification methodology and reference
toolchain for KRITVA semiconductor IP.

Its intended scope includes:

- RTL syntax and elaboration checks.
- Static analysis and lint.
- Simulation-based verification.
- Functional verification using Python and cocotb.
- Functional coverage.
- RTL code coverage.
- Assertions and formal verification.
- Register verification and consistency checks.
- Regression management.
- Evidence generation and validation.
- Quality assessment.
- Developer workstation and Linux CI execution.

KVRF provides common reusable infrastructure and policies.

Individual IP repositories retain their own:

- RTL source.
- Verification plans.
- Testbenches and test cases.
- Assertions and formal properties.
- Verification configurations.
- Detailed execution reports and evidence.

KVRF does not imply that every verification activity is applicable to
every IP. Applicability and required evidence are defined by the relevant
standard and verification policy.

## 4. IP source categories

KRITVA VLSI standards support three primary IP source categories.

### 4.1 Internal IP

IP developed and maintained by KRITVA.

Examples include:

- KRITVA-specific controllers.
- Custom interconnect components.
- Internal peripheral IP.
- Custom accelerators.
- Platform-specific system components.

The IP repository maintains implementation, specifications, verification,
quality records and release history.

KRITVA owns or controls the rights to publish the implementation and
associated documentation according to the applicable contribution and
licensing arrangements.

### 4.2 Open-source IP

IP obtained from publicly available projects under applicable
open-source licences.

The adoption and maintenance process must preserve:

- Upstream project identity.
- Original repository reference.
- Licence and attribution.
- Immutable upstream commit baseline.
- Upstream release and change history.
- KRITVA-specific customization records.
- Verification and qualification evidence.

The upstream source and KRITVA-qualified release must have distinct
identities and version histories.

Upstream changes must be monitored and evaluated before adoption.
Automatic adoption into a qualified KRITVA release is not permitted.

The governing process is defined under:

`VLSI/ip-standard/standard/`

### 4.3 Commercial and licensed third-party IP

IP obtained through commercial licensing or other restricted agreements.

Examples may include:

- Processor IP.
- Memory controllers.
- PHYs.
- Security IP.
- Licensed interconnect components.
- Other proprietary semiconductor IP.

The adoption and integration process must respect:

- Licence scope.
- Permitted use.
- Redistribution restrictions.
- Vendor documentation restrictions.
- Verification and implementation access limitations.
- Confidentiality obligations.

Commercial IP may be evaluated against applicable KRITVA integration,
verification and quality requirements using authorized evidence.

The public repository must not contain proprietary source code,
restricted vendor documentation or confidential commercial reports.

## 5. KRITVA SoC consumer profiles

The KRITVA VLSI standards are intended to support multiple SoC consumers.

The initial consumer profiles are:

- KRITVA Nexus.
- KRITVA Edge.

These profiles provide a generic description of the intended IP consumer
classes. They do not define detailed SoC architectures, final IP selections
or implementation requirements.

### 5.1 KRITVA Nexus

**Consumer class:** High-performance robotics SoC.

**Generic workload profile:**

- Application-level computing.
- Operating-system execution.
- Robotics application processing.
- Data-intensive processing.
- Networking and system communication.
- Potential hardware acceleration.

The IP standard should support the evaluation and integration of IP
categories relevant to this class of workload.

Potential IP categories include:

- Application-class CPU.
- System interconnect and bridges.
- Memory controllers and memory interfaces.
- DMA engines.
- Interrupt controller.
- General-purpose and high-speed peripherals.
- AI, vision or other workload accelerators.
- Platform security components.

The exact CPU architecture, memory subsystem, interconnect, accelerators,
IP selections and performance requirements are not established by this
generic profile.

### 5.2 KRITVA Edge

**Consumer class:** Real-time robotics control SoC.

**Generic workload profile:**

- Deterministic control processing.
- Real-time peripheral management.
- Industrial communication.
- Actuator and sensor control.
- Time-sensitive data acquisition.
- Low-latency control operations.

Potential IP categories include:

- Real-time CPU.
- Low-latency system interconnect.
- Memory controllers and local memory interfaces as required.
- DMA engines.
- Prioritized interrupt controller.
- General-purpose and real-time peripherals.
- Industrial communication components.
- Motor-control and signal-processing support where required.
- Platform security components.

The exact CPU architecture, interconnect, memory configuration, peripheral
selection, control architecture and timing requirements are not established
by this generic profile.

### 5.3 Shared and SoC-specific IP

An IP may be applicable to both Nexus and Edge, or to only one consumer.

The IP Standard should define a common IP specification independently
of a particular SoC implementation.

Each SoC consumer should maintain its own integration profile, including
the applicable:

- IP release.
- Configuration and parameters.
- Interface connections.
- Address allocation.
- Clock and reset connections.
- Interrupt routing.
- Power and isolation requirements.
- Timing and CDC/RDC constraints.
- Integration verification evidence.

A common IP specification must not be interpreted as requiring identical
integration configurations across the two SoCs.

### 5.4 Public information boundary

The public VLSI standards may describe Nexus and Edge through generic
consumer attributes, including:

- SoC consumer classification.
- Broad intended workload.
- Generic IP capability categories.
- Generic integration and qualification methodology.

The following information must remain in controlled engineering
repositories unless explicitly approved for public release:

- Detailed SoC architecture and microarchitecture.
- Final IP selections and implementation topology.
- Bus topology and address maps.
- Memory organization and bandwidth targets.
- Detailed CPU and accelerator configurations.
- Performance, power and area targets.
- Process-specific implementation details.
- Security architecture and threat-sensitive information.
- Unreleased integration configurations.
- Detailed verification reports containing confidential information.

Public profile descriptions do not constitute release approval for
unreleased SoC architecture information.

### 5.5 Programme boundary

KRITVA Nexus and KRITVA Edge are SoCs in the KRITVA project and are
planned as part of the future `kritva-program` V3 plan.

This document establishes only the generic engineering-standard
applicability of the two SoC consumer profiles.

It does not:

- Establish a V3 programme baseline.
- Create V3 programme tasks or milestones.
- Record programme execution status.
- Establish programme credit.
- Approve a SoC architecture or implementation.
- Modify any existing programme baseline.

KRITVA Nexus remains outside `kritva-program` V2. Nothing in this
repository creates Nexus V2 status, task mapping or programme credit.

Programme planning and execution are governed by `kritva-program`.

## 6. Reading order

The following reading order is recommended for contributors and reviewers.

| Order | Document or area | Purpose |
|---|---|---|
| 1 | `README.md` | Repository scope and organization |
| 2 | `GOVERNANCE.md` | Ownership, approval and public-content controls |
| 3 | `VLSI/README.md` | VLSI domain organization and consumer profiles |
| 4 | `ip-standard/standard/KRITVA_IP_STANDARD.md` | Normative IP engineering contract |
| 5 | `ip-standard/standard/OPEN_SOURCE_IP_POLICY.md` | Open-source IP licensing and publication policy |
| 6 | `ip-standard/standard/IP_ADOPTION_PROCESS.md` | IP discovery and adoption |
| 7 | `ip-standard/standard/IP_CUSTOMIZATION_POLICY.md` | Customization and downstream maintenance |
| 8 | `ip-standard/standard/IP_UPSTREAM_MAINTENANCE_POLICY.md` | Upstream change monitoring |
| 9 | `ip-standard/standard/IP_LIFECYCLE_POLICY.md` | IP lifecycle and release requirements |
| 10 | `verification/KVRF/` specifications and policies | Verification methodology and evidence |
| 11 | Relevant schemas | Machine-readable metadata and evidence contracts |
| 12 | Relevant templates and examples | Practical application of the standards |

The reading order is an introduction to the intended document set.
It does not imply that documents not yet created or approved are available
or normative.

## 7. Relationship between VLSI standards and IP repositories

The VLSI standards repository defines reusable requirements and
methodologies.

Individual IP repositories own their implementation-specific engineering
content.

An IP repository should reference:

- Applicable KRITVA IP Standard version.
- Applicable KVRF version.
- IP manifest and schema versions.
- IP-specific specification and release version.
- Upstream source baseline where applicable.
- Verification and quality evidence.
- Applicable SoC integration profiles.

An IP release should remain traceable to the exact standards and schemas
used for its qualification.

A standards update does not automatically modify an existing IP release.

The impact of a standards change must be evaluated against affected
IP packages and their qualification records.

## 8. Future VLSI domains

The following engineering areas are recognized as potential future
extensions of the VLSI standards framework.

They are placeholders only and are not yet defined normative domains.

### 8.1 Design

**Proposed location:** `VLSI/design/`

Potential future scope:

- RTL design methodology.
- Coding conventions.
- Microarchitecture documentation.
- Design review methodology.
- Reusable RTL development practices.
- Design quality rules.

**Status:** NOT_DEFINED.

### 8.2 Physical Design

**Proposed location:** `VLSI/physical-design/`

Potential future scope:

- Synthesis and implementation methodology.
- Floorplanning and placement conventions.
- Clock-tree synthesis.
- Routing methodology.
- Physical verification.
- Power and implementation reporting.
- Technology-specific implementation guidance.

**Status:** NOT_DEFINED.

### 8.3 Timing

**Proposed location:** `VLSI/timing/`

Potential future scope:

- Timing constraint conventions.
- SDC management.
- Timing ownership.
- Static timing analysis.
- Clock-domain timing requirements.
- Timing closure methodology.
- Signoff evidence and reporting.

**Status:** NOT_DEFINED.

### 8.4 DFT

**Proposed location:** `VLSI/DFT/`

Potential future scope:

- Scan architecture.
- Testability requirements.
- ATPG methodology.
- Memory BIST.
- Logic BIST.
- Test access and debug interfaces.
- DFT verification and signoff evidence.

**Status:** NOT_DEFINED.

These areas must be developed through separately reviewed standards.
Their existence in this index does not create mandatory requirements or
imply that their methodologies have been selected.

## 9. Versioning and status

The VLSI domain follows the repository governance policy.

Each normative standard, specification, schema and reference-flow
definition must maintain its own version and status.

The following document statuses are recognized:

- DRAFT
- UNDER_REVIEW
- APPROVED
- DEPRECATED
- SUPERSEDED

The VLSI domain index does not independently approve standards.

Approval authority and document lifecycle transitions are governed by
the repository-level `GOVERNANCE.md`.

## 10. Document maintenance

This index should be updated when:

- A new VLSI standards area is introduced.
- A document is added, renamed or retired.
- The IP source categories change.
- A new SoC consumer profile is approved for public description.
- The reading order changes.
- The relationship between VLSI standards and IP repositories changes.

Changes must follow the repository governance and public-content
review requirements.

---

## 11. Approval record

| Field | Value |
|---|---|
| Document ID | KSTD-VLSI-001 |
| Version | 0.1.0 |
| Status | DRAFT |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Approver | Dinesh Annayya (`dineshannayya`) |
| Approval date | PENDING |
| Approval commit | PENDING |

**Approval statement:** This document is not an approved KRITVA VLSI
domain baseline until Dinesh Annayya explicitly approves version 0.1.0
and the approval is recorded against the applicable repository commit.

---

**End of document**
