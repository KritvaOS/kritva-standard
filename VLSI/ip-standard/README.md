# KRITVA VLSI IP Standardization

Copyright (c) Kritva Robotics.  
Version: 0.1.0  
Status: DRAFT  
Owner: Dinesh Annayya  
Classification: PUBLIC

## 1. Purpose and scope

This directory contains the public KRITVA VLSI IP standardization framework.

It defines common requirements, IP adoption and maintenance processes, customization controls, lifecycle governance, verification evidence expectations, and reusable record templates.

The framework is intended for:
- KRITVA-developed IP.
- Third-party and open-source IP considered for adoption.
- Customized or upstream-maintained IP.
- IP verification and evidence management using the KRITVA Verification Reference Flow (KVRF).
- Future SoC profiles that extend the common standard.

This repository defines standards and processes. It does not duplicate programme-level planning, milestone tracking, or project execution governance maintained in `kritva-program`.

## 2. Document authority and precedence

Use the documents according to their responsibilities:

1. **KRITVA IP Standard (IPSTD):** common normative requirements and standardization principles.
2. **Specialized policies:** define the processes for open-source IP, adoption, customization, and upstream maintenance.
3. **IP Lifecycle Policy (LCP):** defines lifecycle states, assurance levels, transitions, and decision records.
4. **KVRF Specification:** defines verification outcomes, evidence records, and verification quality expectations.
5. **Schemas and templates:** provide machine-readable validation structures and reusable record formats. They do not independently establish approval.

A SoC-specific profile may add requirements within its approved scope. It must not silently weaken applicable common requirements.

Where documents appear inconsistent, record the issue for Owner review. Do not resolve normative conflicts by silently changing requirements or records.

A waiver is effective only after the required approval. A waiver does not change the underlying requirement or convert failed or missing evidence into passing evidence.

## 3. Document and artifact index

All listed artifacts are version 0.1.0 DRAFT unless otherwise stated. DRAFT documents are not approvals.

| ID | Path | Purpose | Status |
|---|---|---|---|
| IPSTD | `VLSI/ip-standard/standard/KRITVA_IP_STANDARD.md` | Common KRITVA IP requirements and standardization framework | DRAFT |
| OSIP | `VLSI/ip-standard/standard/OPEN_SOURCE_IP_POLICY.md` | Open-source IP evaluation, licensing and adoption controls | DRAFT |
| ADP | `VLSI/ip-standard/standard/IP_ADOPTION_PROCESS.md` | IP candidate evaluation and adoption process | DRAFT |
| CUST | `VLSI/ip-standard/standard/IP_CUSTOMIZATION_POLICY.md` | Customization categories, upstream separation and re-verification | DRAFT |
| UPM | `VLSI/ip-standard/standard/IP_UPSTREAM_MAINTENANCE_POLICY.md` | Upstream monitoring, event triage and maintenance | DRAFT |
| LCP | `VLSI/ip-standard/standard/IP_LIFECYCLE_POLICY.md` | Lifecycle states, assurance levels and lifecycle decisions | DRAFT |
| KVRF | `VLSI/verification/KVRF/KVRF_SPECIFICATION.md` | Verification reference flow and evidence requirements | DRAFT |
| KVRF-SCHEMA | `VLSI/verification/KVRF/schemas/kvrf-evidence.schema.json` | Validation schema for KVRF evidence records | DRAFT |
| LCP-SCHEMA | `VLSI/ip-standard/schemas/ip-lifecycle.schema.json` | Validation schema for IP lifecycle records | DRAFT |
| RTL-MANIFEST-SCHEMA | `VLSI/ip-standard/schemas/rtl-library-manifest.schema.json` | Validation schema for approved RTL library manifests | DRAFT |
| TPL-LCP | `VLSI/ip-standard/templates/ip-lifecycle.template.yaml` | IP lifecycle record template | DRAFT |
| TPL-ADP | `VLSI/ip-standard/templates/ip-adoption-record.template.yaml` | IP adoption evaluation and recommendation record | DRAFT |
| TPL-CUST | `VLSI/ip-standard/templates/ip-customization-record.template.yaml` | IP customization and re-verification record | DRAFT |
| TPL-UPM | `VLSI/ip-standard/templates/upstream-watch-register.template.yaml` | Upstream dependency watch register and event record | DRAFT |
| TPL-KVRF | `VLSI/verification/KVRF/templates/verification-plan.template.yaml` | KVRF verification planning template | DRAFT |
| TPL-WVR | `VLSI/ip-standard/templates/waiver-exception-record.template.yaml` | Lifecycle, verification and standard waiver record | DRAFT |
| TPL-MAP | `VLSI/ip-standard/templates/requirement-id-mapping.template.yaml` | Public template for profile-to-common requirement mapping | DRAFT |
| INDEX | `VLSI/ip-standard/README.md` | Public navigation and framework index | DRAFT |

Templates are starting points, not completed records. Validate completed records against their applicable schemas where a schema is provided.

## 4. How the documents relate

The document set forms a connected IP governance flow:

- **IPSTD** establishes common technical requirements and standardization conventions.
- **OSIP** defines controls for evaluating and using externally sourced IP.
- **ADP** defines the candidate evaluation and adoption decision process.
- **CUST** governs parameterization, wrappers, patches, forks and generated customizations.
- **UPM** governs upstream monitoring, event triage, updates and maintenance.
- **LCP** records the IP's lifecycle state, assurance level and approved transitions.
- **KVRF** defines how verification results are produced, recorded and assessed.

The schemas validate structured records. Templates help contributors create those records consistently.

Lifecycle records identify the IP and its lifecycle decisions. Adoption, customization and waiver records reference the same IP identifier and relevant lifecycle decision identifier where applicable.

KVRF evidence is associated with an IP revision, configuration and verification run. Lifecycle and adoption decisions may reference that evidence; they do not replace it.

## 5. Requirement and identifier conventions

### 5.1 Common standard

Common requirements use:

`KIP-STD-<AREA>-NNN`

A common requirement promoted from a profile receives a new KIP identifier and retains a derivation reference to its original profile requirement.

Existing identifiers must never be renumbered.

### 5.2 Nexus profile

The private Nexus profile uses:

`KNX-RTL-<CAT>-NNN`

The profile standard is `KNX-RTL-STD-001`.

Nexus uses SHALL with normative force equivalent to MUST in the common standard.

Nexus rule text and per-rule mappings are private. They must remain in the private `kritva-nexus` repository.

### 5.3 Edge profile

The Edge identifier scheme is TBD. The Edge profile has not started. Its identifier namespace and normative requirements require Owner decisions before publication.

### 5.4 Mapping relationships

The mapping methodology recognizes:

- `EQUIVALENT`
- `STRICTER`
- `NEXUS_ONLY`
- `PROMOTED`

The public mapping template defines the record structure only. It does not authorize publication of private profile identifiers or rule details.

Enforcement classes are:
- `A` — automated
- `T` — tool-assisted
- `R` — review only

Enforcement class does not change normative force.

## 6. Public and private boundary

This repository is PUBLIC.

The following restrictions apply:

- Do not include Nexus rule text, private implementation details, or unreleased Nexus architecture information.
- Do not publish the populated Nexus per-rule mapping here.
- Keep the Nexus profile and its populated per-rule mapping in the private `kritva-nexus` repository.
- Keep only common-standard requirements, public mapping methodology, and area-level mapping guidance in this repository.
- The Edge profile has not started; do not publish speculative Edge requirements as approved rules.
- Preserve upstream copyright and licence notices when incorporating third-party material.

The public mapping template is intentionally generic and contains placeholders rather than private Nexus rule content.

## 7. Owner decisions and open items

### 7.1 Decisions already made

The following framework decisions have been established by the Owner:

- RFC 2119 MUST terminology is used for common normative requirements.
- Nexus SHALL has equivalent normative force to common-standard MUST.
- Common and Nexus requirement namespaces are separate.
- Existing requirement identifiers are never renumbered.
- Enforcement classes A/T/R are adopted.
- KVRF with cocotb is the default reference flow for new KRITVA-developed IP at L2 and above.
- Equivalent verification flows are permitted when they produce evidence conforming to the KVRF evidence schema.
- Upstream IP may retain native testbenches with wrapper-level KVRF tests.
- APB is the primary control/register bus; its revision and profile remain TBD.
- AXI4 is permitted for data and high-bandwidth interfaces. Other control buses require documented bridges.
- Active-low reset is the default, using `rst_<domain>_n_i`.
- Active-high reset requires an approved waiver.
- The approved RTL library manifest is the sole technology boundary for technology-dependent RTL.
- KRITVA-authored files use `Kritva Robotics` as copyright holder.

### 7.2 Open items

Open items remain controlled by their respective documents and Owner decisions.

Examples include:

- APB revision and interface profile.
- Completion and approval of the RTL library manifest and its actual entries.
- Verification tool versions and environment baselines.
- Outstanding policy and lifecycle clarifications.
- Edge profile scope, requirements and identifier namespace.
- Any unresolved mapping or normative conflict.

Track open items using the identifiers and registers defined by the relevant document. Do not treat an open item as approved merely because a template or proposed record exists.

IPSTD-OI-010 / OI-006 includes the profile-to-common per-rule mapping work. The populated Nexus mapping belongs in the private Nexus repository; only public methodology and area-level guidance belong here.

## 8. Contribution and review guidance

Contributors should:

1. Identify the applicable standard, policy and requirement before proposing a change.
2. Preserve existing requirement, decision and evidence identifiers.
3. Use MUST for common normative requirements and maintain the established Nexus SHALL equivalence.
4. Keep common requirements separate from SoC-specific profile requirements.
5. Provide rationale, scope, impact and verification evidence for normative changes.
6. Update relevant schemas and templates when record structures change.
7. Keep public and private information within their approved repository boundaries.
8. Submit changes for Owner review before treating them as approved.
9. Record waivers explicitly; do not hide deviations in implementation notes.
10. Preserve upstream notices and document provenance for adopted IP.

Changes to normative requirements, identifier schemes, schema contracts, profile scope or approval policy require explicit Owner review.

The Owner is Dinesh Annayya. Reviewer and approver assignments for individual records must be populated as applicable.

## 9. Approval and applicability disclaimer

This repository documents a standardization framework and its proposed artifacts.

Nothing in this repository, including a standard, policy, schema, template, mapping record or example, by itself approves any IP, RTL library entry, tool, tool version, verification result, lifecycle transition or product integration.

Approval requires the applicable review, decision and evidence records under the relevant KRITVA policy.

Until such approval is recorded, treat the applicable item as DRAFT, PROPOSED, TBD or UNVERIFIED.