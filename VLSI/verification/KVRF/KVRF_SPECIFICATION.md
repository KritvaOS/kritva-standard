
# KRITVA VERIFICATION REFERENCE FLOW (KVRF) SPECIFICATION

| Field | Value |
|---|---|
| Document ID | KVRF-SPEC-001 |
| Title | KRITVA Verification Reference Flow Specification |
| Version | 0.1.0 |
| Status | DRAFT |
| Classification | PUBLIC |
| Owner | Dinesh Annayya |
| Copyright Holder | Kritva Robotics |
| Effective Date | TBD |
| Review Cycle | Annual, or upon a material change to the verification framework |
| Normative Language | RFC 2119 |
| Applicable Scope | KRITVA-developed and adopted IP verification |
| Reference Languages | Python, SystemVerilog |
| Reference Test Framework | cocotb |
| Evidence Format | KVRF-schema |

Copyright (c) Kritva Robotics. All rights reserved, subject to the applicable repository licence and any third-party notices retained in the relevant files.

---

## 1. Purpose

The KRITVA Verification Reference Flow (KVRF) defines a common, evidence-oriented verification methodology for KRITVA intellectual property (IP).

KVRF establishes:

- A common verification architecture and execution model.
- A reference flow based on Python, cocotb, and SystemVerilog.
- A consistent approach to test and test-suite identification.
- A machine-readable evidence record format.
- Standardized test outcomes and evidence interpretation.
- Coverage and quality expectations aligned with IP assurance levels L0 through L3.
- Reproducibility and configuration traceability.
- CI integration and evidence publication requirements.
- A common verification boundary for upstream IP and customized IP.

KVRF is intended to make verification results portable, reviewable, traceable, and comparable across KRITVA IP repositories.

The primary objective is not to mandate one simulator or one testbench implementation. The objective is to establish a consistent evidence contract so that different verification implementations can produce evidence that can be reviewed and accepted under KRITVA standards.

## 2. Scope

### 2.1 In scope

KVRF applies to:

1. New KRITVA-developed RTL IP.
2. Third-party or open-source IP adopted for KRITVA use.
3. Customized, patched, wrapped, or forked IP.
4. IP-level functional verification.
5. Interface and protocol verification.
6. Parameter and configuration verification.
7. Reset and clock behavior verification.
8. Integration and interoperability testing.
9. Regression execution and evidence publication.
10. Verification evidence used for KRITVA IP assurance-level assessments.

### 2.2 Out of scope

KVRF does not define:

- A complete RTL coding standard.
- A specific SoC architecture.
- A particular simulator or commercial tool vendor.
- A mandatory implementation of every testbench component.
- Foundry-specific timing or physical-design signoff.
- A complete CDC/RDC methodology.
- A replacement for formal verification where formal analysis is required.
- Product-level safety certification.
- Silicon validation unless explicitly included in a separate verification scope.

KVRF evidence MAY reference results from tools or methodologies outside the reference flow, provided the evidence is traceable and conforms to the applicable KVRF schema.

### 2.3 Relationship to KRITVA standards and policies

| Document | Relationship |
|---|---|
| KRITVA IP Standard | Defines common IP design, interface, and verification expectations. |
| KRITVA IP Adoption Process | Defines how verification evidence is assessed during IP adoption. |
| KRITVA IP Lifecycle Policy | Defines L0-L3 assurance levels and lifecycle evidence requirements. |
| KRITVA IP Customization Policy | Defines verification obligations for modified or customized IP. |
| KRITVA IP Upstream Maintenance Policy | Defines upstream change and evidence reassessment requirements. |
| IP-specific specification | Defines the functional requirements and acceptance criteria to be verified. |
| SoC integration documentation | Defines product-specific integration and system-level verification requirements. |

KVRF defines verification evidence conventions. It does not replace the governing requirements or approval records maintained by the IP owner or KRITVA programme governance.

## 3. Normative language

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, and OPTIONAL are to be interpreted as normative requirement terms.

Common KRITVA standards use RFC 2119 terminology. MUST is the preferred normative keyword in this specification.

Where an applicable approved profile uses SHALL, SHALL has the same normative force as MUST.

### 3.1 Normative requirements

KVRF requirements use the following identifier scheme:

`KVRF-<AREA>-NNN`

Examples:

- `KVRF-ARCH-001`
- `KVRF-TEST-001`
- `KVRF-EVID-001`
- `KVRF-COV-001`
- `KVRF-CI-001`

These identifiers are local to the KVRF specification and do not replace common IP standard identifiers of the form:

`KIP-STD-<AREA>-NNN`

Where a KVRF requirement is promoted into a common KRITVA IP standard, the common standard MUST assign a new KIP identifier and retain a reference to the originating KVRF requirement.

Existing requirement identifiers MUST NOT be renumbered.

## 4. KVRF principles

### 4.1 Outcome and evidence based

KVRF is outcome/evidence based.

A verification flow is acceptable when it produces sufficient, traceable, reviewable evidence for the applicable requirements and assurance level.

The reference flow uses cocotb, Python, and SystemVerilog. Equivalent flows MAY be used.

An equivalent flow MUST:

1. Identify the IP and source revision.
2. Identify the verification configuration.
3. Identify tests and suites.
4. Record execution outcomes.
5. Produce evidence records conforming to the applicable KVRF schema.
6. Preserve relevant logs and reports.
7. Identify tool names and versions.
8. Support review of failures and unresolved results.
9. Provide sufficient reproducibility information.
10. Retain traceability to applicable requirements or acceptance criteria.

The use of a particular simulator, programming language, or testbench architecture does not by itself establish verification acceptance.

### 4.2 Evidence over tool branding

A result MUST be assessed on its validity and relevance, not on the commercial or open-source status of the tool that generated it.

Equivalent tools and execution environments MAY be used where their results are suitable for the verification objective.

Tool limitations MUST be documented where they affect confidence in the evidence.

### 4.3 Traceability

Every accepted verification result MUST be traceable to:

- An IP identifier.
- A source revision.
- A configuration.
- A test or suite identifier.
- An execution environment.
- An outcome.
- An evidence artifact or immutable reference.

Where applicable, the result MUST also reference a requirement or acceptance criterion.

### 4.4 Separation of execution and acceptance

Test execution and evidence acceptance are separate activities.

A test runner MAY report a passing result, but that result MUST NOT automatically be treated as accepted lifecycle evidence.

Evidence acceptance requires review of source, configuration, test relevance, execution completeness, and artifact availability according to the applicable assurance level.

### 4.5 No implicit pass

Missing, skipped, blocked, inconclusive, or failed results MUST NOT be counted as passing results.

A test suite MUST NOT report overall PASS when a required test has an outcome that prevents acceptance under the suite's declared policy.

### 4.6 Immutable execution identity

Each verification execution MUST have a unique execution identifier.

The execution identifier MUST distinguish separate runs, even when they use the same source revision and configuration.

Re-running a test MUST NOT overwrite the evidence from an earlier execution.

## 5. Assurance-level alignment

KVRF supports the KRITVA IP Lifecycle Policy assurance levels.

| Level | Description | Verification expectation |
|---|---|---|
| L0 | Registered / Initial assessment | Verification scope and major unknowns identified |
| L1 | Evaluated / Basic evidence | Basic functional evaluation and initial checks |
| L2 | Verified / Controlled engineering evidence | Defined verification plan, functional regression, traceable evidence, and reviewed results |
| L3 | Qualified / Release-oriented evidence | Release-scope regression, coverage assessment, integration evidence, and qualification review |

### 5.1 L0 expectations

At L0:

- The verification scope SHOULD be identified.
- Major functional requirements SHOULD be listed.
- Verification unknowns SHOULD be recorded.
- Candidate test approaches MAY be documented.
- Tool versions MAY remain unverified.

L0 does not require a completed testbench or passing regression.

### 5.2 L1 expectations

At L1:

- Basic functional behavior SHOULD be evaluated.
- Important interfaces SHOULD be exercised.
- Basic positive and negative scenarios SHOULD be considered.
- Initial lint, elaboration, or structural checks SHOULD be performed where applicable.
- Test outcomes SHOULD be retained.
- Known verification gaps MUST be documented.

L1 evidence MAY be produced by a native testbench or another suitable evaluation method.

### 5.3 L2 expectations

At L2:

- A controlled verification plan MUST exist.
- Test and suite identifiers MUST be stable.
- Relevant functional requirements MUST be mapped to tests or other accepted evidence.
- Functional regression MUST be executed.
- Evidence records MUST conform to the applicable KVRF schema.
- Required tests MUST have acceptable outcomes.
- Failures and unresolved issues MUST be dispositioned.
- The source revision and configuration MUST be identifiable.
- Relevant logs and reports MUST be retained.
- The verification environment MUST be documented sufficiently for reproduction.
- Evidence MUST be reviewed.

For new KRITVA-developed IP, the KVRF reference flow using Python, cocotb, and SystemVerilog is the default at L2 and above.

An equivalent flow is acceptable if it meets the evidence requirements in this specification.

### 5.4 L3 expectations

At L3:

- L2 criteria MUST be satisfied.
- The release source baseline MUST be identified.
- The supported configuration set MUST be documented.
- Release-scope regression MUST be completed.
- Coverage results MUST be reviewed against defined targets.
- Coverage exclusions MUST be justified and approved.
- Relevant integration tests MUST be completed.
- Applicable interface, reset, and clock behavior MUST be verified.
- Known defects MUST have approved dispositions.
- The verification environment and tool versions MUST be recorded.
- Reproducibility limitations MUST be documented.
- The qualification evidence MUST be reviewed and approved.

L3 is scoped qualification. It does not automatically imply silicon validation or qualification for every possible configuration.

### 5.5 Not-applicable criteria

A verification criterion MAY be marked not applicable only when a technical rationale is recorded.

The record MUST identify:

- The criterion.
- The reason it does not apply.
- The affected IP or configuration.
- The reviewer.
- The approval, where required.

An unexecuted test MUST NOT be marked not applicable merely because it was not implemented.

## 6. Reference verification architecture

### 6.1 Overview

The KVRF reference architecture consists of:

1. RTL design under verification (DUT).
2. Simulator.
3. SystemVerilog interface or wrapper layer.
4. cocotb testbench.
5. Python test utilities and reusable components.
6. Test and suite definitions.
7. Result collection.
8. KVRF evidence generation.
9. Evidence and artifact storage.
10. CI execution and publication.

The architecture is intended to separate functional verification intent from simulator-specific execution details.

### 6.2 Reference flow

~~~text
                 IP Requirements
                        |
                        v
                Verification Plan
                        |
                        v
               Test / Suite Registry
                        |
                        v
+------------------------------------------------+
|              KVRF Testbench                    |
|                                                |
|  Python + cocotb                               |
|       |                                        |
|       +-- Test sequences                       |
|       +-- Drivers                              |
|       +-- Monitors                             |
|       +-- Scoreboards                          |
|       +-- Functional checks                    |
|       +-- Coverage collection                  |
|                                                |
+-----------------------+------------------------+
                        |
                        v
               SystemVerilog DUT
                        |
                        v
                    Simulator
                        |
                        v
                Execution Results
                        |
             +----------+----------+
             |                     |
             v                     v
        Logs/Reports          Coverage Data
             |                     |
             +----------+----------+
                        |
                        v
                KVRF Evidence
                  Generator
                        |
                        v
              KVRF Evidence Records
                        |
                        v
                CI / Review / Gate
                        |
                        v
              Assurance Assessment
~~~

This diagram is conceptual. An equivalent architecture MAY be used if it preserves the required evidence and traceability.

### 6.3 SystemVerilog role

SystemVerilog MAY be used for:

- RTL implementation.
- Testbench-facing interfaces.
- Bind modules and assertions.
- Protocol monitors.
- Verification adapters.
- Simulator interoperability.
- DUT-specific wrappers.

The reference flow does not require all verification logic to be written in SystemVerilog.

SystemVerilog components SHOULD remain reusable and should avoid embedding unnecessary test-specific behavior into the DUT.

### 6.4 Python and cocotb role

Python and cocotb provide the default high-level verification environment for new KRITVA-developed IP at L2 and above.

They MAY be used for:

- Test sequencing.
- Bus-functional models.
- Drivers and monitors.
- Scoreboards.
- Reference models.
- Data generation.
- Functional checking.
- Coverage sampling.
- Test parameterization.
- Result collection.
- Evidence generation.

Test code SHOULD separate stimulus generation, protocol handling, checking, and reporting.

### 6.5 Reusable verification components

Reusable components MAY include:

- APB master BFM.
- AXI interface BFM.
- Register access helpers.
- Reset and clock control.
- Interrupt monitors.
- FIFO monitors.
- Memory models.
- Scoreboards.
- Protocol checkers.
- Functional coverage collectors.
- Reference models.

A reusable component MUST document its supported protocol profile and limitations.

A reusable component MUST NOT claim protocol compliance beyond the behavior it actually checks.

### 6.6 DUT boundary

The verification plan MUST identify the DUT boundary.

The boundary SHOULD include:

- DUT top-level module.
- Interface definitions.
- Clock and reset inputs.
- Configuration parameters.
- External dependencies.
- Memory or register models.
- Interrupt and status outputs.
- Protocol connections.

The boundary MUST be consistent with the source revision and configuration recorded in the evidence.

## 7. Test organization and identification

### 7.1 Test identity

Every managed KVRF test MUST have a stable test identifier.

Recommended format:

`KVRF-TST-<IP>-<AREA>-NNN`

Where:

- `KVRF-TST` identifies a test.
- `<IP>` identifies the IP or IP family.
- `<AREA>` identifies the functional area.
- `NNN` is a unique numeric sequence.

Example:

`KVRF-TST-TIMER-REG-001`

The example is illustrative and does not reserve an IP identifier.

A test identifier MUST NOT be changed merely because the test implementation is refactored.

If the test's verification intent changes materially, a new test identifier SHOULD be assigned and the previous test SHOULD be marked superseded.

### 7.2 Test suite identity

Every managed suite MUST have a stable suite identifier.

Recommended format:

`KVRF-SUITE-<IP>-<LEVEL>-NNN`

Example:

`KVRF-SUITE-TIMER-L2-001`

A suite MUST declare:

- Suite identifier.
- Suite name.
- Assurance level or intended use.
- Included test identifiers.
- Required tests.
- Optional tests.
- Configuration assumptions.
- Expected execution conditions.
- Suite acceptance criteria.

### 7.3 Test categories

A verification plan SHOULD organize tests into relevant categories:

| Category | Purpose |
|---|---|
| Smoke | Basic elaboration and initial operation |
| Functional | Required functional behavior |
| Register | Register access, reset values, and side effects |
| Protocol | Bus or interface protocol behavior |
| Reset | Reset assertion, release, and recovery |
| Clock | Clock-dependent behavior and assumptions |
| Interrupt | Interrupt generation, masking, and clearing |
| Parameter | Supported configuration and parameter combinations |
| Boundary | Minimum, maximum, and boundary conditions |
| Negative | Invalid or unsupported transactions and inputs |
| Stress | Repeated or high-volume operation |
| Error recovery | Fault handling and recovery |
| Integration | Interaction with surrounding components |
| Regression | Re-execution of the controlled test set |

The categories are descriptive. An IP MAY define additional categories.

### 7.4 Test metadata

Each test SHOULD declare:

- Test ID.
- Test name.
- Description.
- Functional category.
- Requirement references.
- Preconditions.
- Stimulus summary.
- Expected behavior.
- Pass criteria.
- Timeout criteria.
- Configuration requirements.
- Applicable assurance levels.
- Test owner.
- Test implementation revision.

A test without a clear pass criterion MUST NOT be used as an acceptance test at L2 or L3.

### 7.5 Requirement traceability

Where an IP has a controlled requirement baseline, tests MUST reference the applicable requirement IDs.

A requirement MAY be verified by:

- One or more tests.
- Assertions.
- Formal properties.
- Static analysis.
- Other accepted evidence.

The verification plan MUST identify the method used.

A test MUST NOT be claimed as verifying a requirement when it does not exercise or establish the required behavior.

### 7.6 Test retirement and supersession

Tests MAY be retired when requirements change or when their verification intent is no longer valid.

A retired test ID MUST remain traceable in historical evidence.

A replacement test MUST reference the superseded test where applicable.

Test IDs MUST NOT be silently reused for unrelated verification intent.

## 8. Execution model

### 8.1 Execution identity

Each KVRF execution MUST have a unique run identifier.

Recommended format:

`KVRF-RUN-<UTC-DATE>-<SEQUENCE>`

Example:

`KVRF-RUN-20261112-001`

The format is a recommendation and MAY be adapted by an implementation.

Run identifiers MUST be unique within the relevant evidence registry.

### 8.2 Execution metadata

Each execution MUST record:

- Run ID.
- Execution timestamp.
- IP identifier.
- Source revision.
- Test or suite identifier.
- Configuration identifier.
- Simulator name.
- Simulator version or `UNVERIFIED`.
- Operating environment.
- Test framework and version or `UNVERIFIED`.
- Relevant dependency versions.
- Execution command or reproducible invocation reference.
- Execution outcome.
- Log and report references.

### 8.3 Test execution

A test runner MUST distinguish between:

- A test that executed and passed.
- A test that executed and failed.
- A test that could not execute because of an environment or dependency problem.
- A test that was intentionally not run.
- A test that is not applicable to the declared scope.
- A test whose result cannot be determined.

A test runner SHOULD retain stdout, stderr, simulator logs, and relevant failure diagnostics.

### 8.4 Timeouts

Tests MUST define timeouts appropriate to their expected execution behavior.

A timeout MUST produce a non-passing result.

The test record SHOULD identify:

- Configured timeout.
- Actual elapsed time, where available.
- Timeout reason.
- Relevant execution log.

A timeout MUST NOT be treated as a pass simply because no explicit assertion failed.

### 8.5 Randomized testing

Randomized tests SHOULD record:

- Random seed.
- Randomization constraints or configuration.
- Number of iterations.
- Relevant generated input metadata.
- Failure reproduction information.

A failure MUST be reproducible where the environment and randomization model permit.

If the exact failure cannot be reproduced, the original failure evidence MUST still be retained and dispositioned.

## 9. KVRF evidence schema

### 9.1 Evidence record purpose

The KVRF evidence record is the common machine-readable representation of a verification result.

Each test execution MUST produce an evidence record or a traceable record within an equivalent evidence package.

A suite execution SHOULD produce a suite-level evidence record that references its individual test records.

### 9.2 Evidence record fields

The following fields define the minimum conceptual evidence model.

The final machine-readable schema and exact field types remain subject to the open items in this specification.

| Field | Required | Description |
|---|---|---|
| `schema_version` | MUST | KVRF evidence schema version |
| `evidence_id` | MUST | Unique evidence record identifier |
| `run_id` | MUST | Unique execution identifier |
| `ip_id` | MUST | IP identifier |
| `ip_name` | SHOULD | Human-readable IP name |
| `source_revision` | MUST | Source commit, tag, or immutable revision |
| `configuration_id` | MUST | Configuration identifier |
| `test_id` | MUST for test records | Stable test identifier |
| `suite_id` | MUST for suite records | Stable suite identifier |
| `test_name` | SHOULD | Human-readable test name |
| `requirement_ids` | SHOULD | Requirements addressed by the test |
| `outcome` | MUST | Controlled outcome value |
| `start_time` | MUST | Execution start timestamp |
| `end_time` | MUST | Execution end timestamp |
| `duration_ms` | SHOULD | Execution duration |
| `toolchain` | MUST | Tool and version information |
| `environment` | MUST | Execution environment information |
| `command` | SHOULD | Reproducible invocation or command reference |
| `seed` | Conditional | Random seed where applicable |
| `artifacts` | MUST | Log, report, and evidence artifact references |
| `coverage` | SHOULD | Coverage summary or reference |
| `failure_summary` | Conditional | Failure details when applicable |
| `review_status` | SHOULD | Evidence review state |
| `producer` | MUST | Evidence producer identity |
| `notes` | MAY | Additional context |

The final schema MUST define field types, required/optional status, enumerations, and validation behavior.

### 9.3 Example test evidence record

~~~json
{
  "schema_version": "0.1.0",
  "evidence_id": "KVRF-EVD-EXAMPLE-0001",
  "run_id": "KVRF-RUN-20261112-001",
  "record_type": "test",
  "ip_id": "KIP-IP-EXAMPLE-001",
  "ip_name": "Example IP",
  "source_revision": "0123456789abcdef",
  "configuration_id": "default",
  "test_id": "KVRF-TST-EXAMPLE-REG-001",
  "test_name": "register_reset_values",
  "requirement_ids": [
    "IP-REQ-REG-001"
  ],
  "outcome": "PASS",
  "start_time": "2026-11-12T10:00:00Z",
  "end_time": "2026-11-12T10:00:02Z",
  "duration_ms": 2000,
  "toolchain": {
    "simulator": {
      "name": "UNVERIFIED",
      "version": "UNVERIFIED"
    },
    "python": {
      "name": "Python",
      "version": "UNVERIFIED"
    },
    "cocotb": {
      "name": "cocotb",
      "version": "UNVERIFIED"
    }
  },
  "environment": {
    "os": "UNVERIFIED",
    "architecture": "UNVERIFIED",
    "container_image": "UNVERIFIED"
  },
  "artifacts": [
    {
      "type": "log",
      "uri": "artifacts/example-test.log"
    },
    {
      "type": "report",
      "uri": "artifacts/example-test-report.json"
    }
  ],
  "coverage": {
    "status": "NOT_REPORTED"
  },
  "review_status": "PENDING",
  "producer": "KVRF",
  "notes": []
}
~~~

This record is illustrative and does not define the final JSON schema. The example values MUST NOT be interpreted as actual execution evidence.

### 9.4 Evidence record validation

An evidence validator SHOULD check:

1. Schema version.
2. Required fields.
3. Identifier format.
4. Allowed outcome values.
5. Timestamp validity.
6. Source revision presence.
7. Toolchain fields.
8. Artifact references.
9. Test or suite identity.
10. Configuration identity.
11. Required conditional fields.
12. Evidence record uniqueness.

A schema-valid record does not automatically establish that its claimed result is technically valid.

### 9.5 Evidence integrity

Evidence artifacts SHOULD be immutable after publication.

Where supported, the evidence package SHOULD include checksums for:

- Source revision or source manifest.
- Test configuration.
- Evidence record.
- Logs.
- Coverage reports.
- Other relevant artifacts.

If an artifact is regenerated, the new artifact MUST receive a new identity or revision.

The previous artifact MUST remain traceable where it was used for an accepted decision.

## 10. Standard outcomes

### 10.1 Controlled outcome values

KVRF defines the following outcomes:

| Outcome | Meaning | Passing result? |
|---|---|---|
| `PASS` | Test completed and all defined pass criteria were satisfied | Yes |
| `FAIL` | Test completed and one or more pass criteria failed | No |
| `BLOCKED` | Test could not proceed because of a dependency, environment, setup, or prerequisite issue | No |
| `NOT_RUN` | Test was not executed | No |
| `NOT_APPLICABLE` | Test does not apply to the declared IP or configuration scope | No; requires rationale |
| `INCONCLUSIVE` | Test executed but did not establish a reliable pass or fail result | No |

Only `PASS` is a passing execution outcome.

### 10.2 PASS

`PASS` MUST be reported only when:

- The test executed to completion.
- Required checks completed.
- All defined pass criteria were satisfied.
- No unresolved execution error invalidates the result.
- Required evidence artifacts were produced.

### 10.3 FAIL

`FAIL` MUST be reported when:

- An assertion fails.
- An expected behavior is not observed.
- A protocol or functional violation is detected.
- A required acceptance criterion is not satisfied.
- An unexpected execution result invalidates the test.

A failure MUST include a summary and relevant diagnostic references.

### 10.4 BLOCKED

`BLOCKED` MUST be used when execution cannot proceed because a prerequisite is unavailable.

Examples include:

- Missing simulator capability.
- Unavailable dependency.
- Missing configuration.
- Invalid build environment.
- Unavailable required test resource.
- An unresolved prerequisite that prevents meaningful execution.

A blocked test MUST identify the blocking reason.

### 10.5 NOT_RUN

`NOT_RUN` MUST be used when the test was not executed.

Examples include:

- Deliberate exclusion from a particular run.
- Suite selection that did not include the test.
- An execution plan that deferred the test.
- An interrupted workflow before the test started.

The reason SHOULD be recorded.

### 10.6 NOT_APPLICABLE

`NOT_APPLICABLE` MUST be used only when the test does not apply to the declared IP or configuration.

The evidence record MUST include a rationale and, where required, reviewer approval.

A test MUST NOT be marked not applicable because it is difficult to implement or because the expected result is unknown.

### 10.7 INCONCLUSIVE

`INCONCLUSIVE` MUST be used when the test executed but could not establish a reliable outcome.

Examples include:

- Ambiguous testbench behavior.
- Incomplete observation.
- An unresolved simulator or environment anomaly.
- A checker limitation that prevents a reliable conclusion.

The reason and follow-up action MUST be recorded.

### 10.8 Suite outcome aggregation

A suite MUST define its outcome aggregation rules.

The default aggregation rule is:

- `FAIL` if any required test is `FAIL`.
- `BLOCKED` if no required test has failed but at least one required test is `BLOCKED`.
- `INCONCLUSIVE` if no required test has failed or been blocked but at least one required test is `INCONCLUSIVE`.
- `NOT_RUN` if the suite was not meaningfully executed.
- `NOT_APPLICABLE` only when the entire suite is demonstrably outside the declared scope.
- `PASS` only when all required tests pass and all suite acceptance criteria are satisfied.

A suite MAY report additional diagnostic counts for optional tests.

Optional tests MUST NOT be used to hide failures in required tests.

A suite-level PASS MUST NOT imply that all possible configurations or behaviors have been verified.

## 11. Functional coverage and quality gating

### 11.1 Coverage principles

Coverage is evidence of exercised verification space. It is not proof of correctness.

Coverage MUST be interpreted together with:

- Requirements.
- Test intent.
- Assertions and checkers.
- Test outcomes.
- Known limitations.
- Coverage exclusions.
- Configuration scope.

A coverage percentage MUST NOT be presented as a standalone measure of IP quality.

### 11.2 Coverage categories

Where applicable, KVRF SHOULD collect:

| Coverage category | Purpose |
|---|---|
| Requirement coverage | Measures whether required behaviors have associated verification evidence |
| Functional coverage | Measures exercised functional scenarios and conditions |
| Protocol coverage | Measures exercised interface and protocol conditions |
| Register coverage | Measures register and field access scenarios |
| Configuration coverage | Measures supported parameter and configuration combinations |
| State coverage | Measures relevant state-machine states and transitions |
| Error coverage | Measures exercised error and recovery scenarios |
| Code coverage | Measures structural RTL execution, where supported |
| Assertion coverage | Measures assertion and property activity, where supported |

Not every category is applicable to every IP.

### 11.3 Coverage model

The verification plan MUST define the coverage model before the relevant assurance review.

The model SHOULD identify:

- Coverage points.
- Coverage bins or conditions.
- Cross coverage where appropriate.
- Excluded conditions.
- Target values.
- Evidence sources.
- Coverage ownership.
- Review criteria.

Coverage models SHOULD be derived from the functional specification and requirements.

### 11.4 Coverage gating by assurance level

| Assurance level | Coverage expectation | Gate |
|---|---|---|
| L0 | Coverage plan may be absent or preliminary | No numerical closure gate |
| L1 | Basic scenarios identified and exercised where practical | Gaps documented |
| L2 | Requirement and functional coverage model defined for the verified scope | Critical gaps dispositioned and reviewed |
| L3 | Release-scope coverage assessed against approved targets | Targets met or exclusions formally approved |

### 11.5 L2 coverage gate

For L2:

- The verification plan MUST identify applicable coverage categories.
- Critical requirements MUST have verification evidence.
- Coverage gaps affecting required functionality MUST be documented.
- Uncovered critical behavior MUST NOT be silently accepted.
- Coverage exclusions MUST have a rationale.
- The reviewer MUST assess whether the evidence supports the declared L2 scope.

A universal numerical coverage threshold is not imposed by this initial specification.

IP-specific acceptance criteria MAY define numerical targets.

### 11.6 L3 coverage gate

For L3:

- Coverage targets MUST be defined for the release scope.
- Relevant requirement and functional coverage MUST be reviewed.
- Coverage gaps MUST be dispositioned.
- Exclusions MUST be justified and approved.
- Code coverage SHOULD be reviewed where supported and meaningful.
- Assertion coverage SHOULD be reviewed where assertions are used.
- Cross coverage SHOULD be used where interactions materially affect correctness.

A numerical target MUST be justified by the IP verification plan.

A high percentage MUST NOT compensate for missing verification of a critical requirement.

### 11.7 Quality gates

Quality gates MAY include:

- Successful elaboration.
- Lint and structural checks.
- Functional regression.
- Assertion checks.
- Protocol checks.
- Requirement traceability.
- Coverage review.
- Known-defect review.
- Configuration validation.
- Reproducibility checks.
- Evidence-schema validation.

The verification plan MUST identify mandatory and advisory gates.

A mandatory gate failure MUST prevent the associated assurance acceptance unless an explicit, approved exception permits the affected scope.

### 11.8 Waivers and exclusions

A coverage exclusion or verification waiver MUST include:

- Identifier.
- Affected requirement or coverage point.
- Rationale.
- Scope.
- Risk.
- Compensating evidence, where available.
- Owner.
- Reviewer.
- Approver.
- Review or expiry date.

A waiver MUST NOT convert an uncovered behavior into covered behavior.

Waiver types, validity, expiry and approval authority are defined in the IP Lifecycle Policy section 13.4. `WAIVED` is not a KVRF evidence outcome.

## 12. APB-first register and bus verification

### 12.1 Register-bus principle

APB is the primary control/register bus for KRITVA IP.

The APB revision and detailed profile remain subject to the applicable common standard and integration profile.

KVRF MUST support verification of APB-attached control and register interfaces.

### 12.2 APB verification expectations

Where an IP exposes an APB interface, the verification plan SHOULD include relevant checks for:

- Address decoding.
- Read and write access.
- Read data validity.
- Write data capture.
- Transfer completion.
- Select and enable sequencing.
- Wait-state behavior, where supported.
- Error response behavior, where supported.
- Access to reserved addresses.
- Access permissions.
- Register reset values.
- Read-only and write-only fields.
- Write-one-to-clear or other side-effect semantics.
- Byte strobes or lane behavior, where supported.
- Back-to-back transfers.
- Reset during or around transactions, where specified.
- Register side effects and interrupt interactions.

The test plan MUST reflect the actual supported APB profile.

A testbench MUST NOT assume optional APB features are implemented unless the IP specification requires them.

### 12.3 Register specification traceability

Register verification SHOULD be derived from a controlled register specification.

Where available, the verification environment SHOULD use machine-readable register descriptions to generate or cross-check:

- Register addresses.
- Field positions.
- Reset values.
- Access permissions.
- Reserved fields.
- Side effects.
- Test scenarios.

Generated tests MUST be reviewed to ensure they reflect the approved register specification.

### 12.4 AXI and other interfaces

AXI4 MAY be used for data or high-bandwidth interfaces.

AXI4-Lite, AHB-Lite, and Wishbone MAY be used only through documented bridges where permitted by the applicable KRITVA standard and integration profile.

KVRF MUST identify the actual interface and supported profile under test.

Protocol verification MUST use the applicable protocol specification and declared IP interface requirements.

### 12.5 Bus-functional models

KVRF MAY provide reusable bus-functional models.

A bus-functional model MUST document:

- Supported protocol revision or profile.
- Supported transfer types.
- Timing assumptions.
- Error behavior.
- Limitations.
- Applicable test scenarios.

A bus-functional model MUST NOT claim complete protocol compliance unless its verification scope supports that claim.

## 13. Reset, clock, and configuration verification

### 13.1 Reset

Where applicable, verification MUST cover:

- Reset assertion.
- Reset polarity.
- Reset value behavior.
- Reset release.
- Recovery behavior.
- Reset interaction with transactions.
- Reset interaction with interrupts and status.
- Reset behavior across supported operating configurations.

The default KRITVA reset convention is active-low, using the naming convention:

`rst_<domain>_n_i`

Active-high reset use requires an approved waiver under the applicable standard.

KVRF verifies externally observable reset behavior. It does not authorize IP to implement unapproved reset synchronizer logic.

### 13.2 Clock

Where applicable, the verification plan SHOULD identify:

- Clock domains.
- Clock frequency assumptions.
- Clock relationships.
- Clock enable behavior.
- Clock stoppage or restart behavior.
- Asynchronous interface assumptions.
- Reset release relationships.

Simulation-based clock tests do not replace CDC/RDC analysis where such analysis is required.

### 13.3 Configuration and parameters

For parameterized IP:

- Supported parameter values MUST be documented.
- Verification configurations MUST be identified.
- Boundary values SHOULD be tested.
- Unsupported combinations SHOULD be rejected or explicitly documented.
- Evidence MUST identify the exact configuration used.

A passing result for one configuration MUST NOT be generalized to all configurations without supporting evidence.

## 14. Upstream IP verification

### 14.1 Native testbench support

Third-party or upstream IP MAY retain its native verification environment.

KVRF does not require upstream projects to replace their native testbench with cocotb.

The adoption record MUST identify:

- Native testbench framework.
- Native test execution method.
- Relevant upstream evidence.
- Known limitations.
- Tool and version information.
- Source revision.

### 14.2 Wrapper-level KVRF tests

For adopted upstream IP, a wrapper-level KVRF test SHOULD be provided where appropriate.

The wrapper-level test SHOULD verify KRITVA-specific integration behavior, including relevant:

- Interface adaptation.
- Reset assumptions.
- Clock assumptions.
- Configuration.
- Register or control-bus behavior.
- Interrupt behavior.
- Parameter mapping.
- Integration constraints.

The wrapper-level test MUST NOT claim to replace upstream verification of all internal IP functionality.

### 14.3 Evidence combination

Upstream native evidence and wrapper-level KVRF evidence MAY be combined.

The evidence package MUST distinguish:

- Upstream-generated evidence.
- KRITVA-generated evidence.
- Wrapper-level evidence.
- Independent review or analysis.
- Evidence accepted from an upstream release.

The source revision and provenance of each evidence item MUST be traceable.

### 14.4 Customized upstream IP

Where upstream IP is patched, forked, or materially customized:

- The customized source revision MUST be identified.
- The customization MUST be recorded under the IP Customization Policy.
- Affected upstream evidence MUST be reassessed.
- KRITVA-specific verification MUST cover the customization's intended behavior.
- Evidence MUST identify whether it applies to upstream source or customized source.

## 15. Reproducibility

### 15.1 Reproducibility objective

A KVRF evidence package SHOULD enable an independent reviewer to understand and, where practical, reproduce the reported execution.

At L2 and above, the verification environment MUST be documented sufficiently to support reproduction or explain why exact reproduction is unavailable.

### 15.2 Reproducibility inputs

The evidence package SHOULD capture:

- Source revision.
- Testbench revision.
- Configuration files.
- Parameter values.
- Test and suite identifiers.
- Simulator and tool versions.
- Python version.
- cocotb version.
- Dependency versions.
- Operating environment.
- Container or environment image reference, where applicable.
- Random seed.
- Execution command.
- Relevant environment variables.
- External model or data dependencies.

### 15.3 Version recording

All tool and dependency versions MUST be recorded when verified.

Where a version is not verified, it MUST be marked:

`UNVERIFIED`

This initial specification does not pin specific simulator, Python, cocotb, compiler, or CI versions.

Tool versions MUST NOT be invented or assumed.

### 15.4 Determinism

Tests SHOULD be deterministic for a fixed source revision, configuration, and random seed.

Where deterministic execution is not practical, the verification plan MUST describe:

- Sources of nondeterminism.
- Seed handling.
- Reproduction procedure.
- Expected variation.
- Failure triage procedure.

### 15.5 Artifact retention

The verification environment MUST retain or reference the artifacts needed to support its declared assurance level.

At minimum, L2 and L3 evidence MUST provide traceable execution logs and result records.

Coverage reports, simulator logs, failure traces, and configuration manifests SHOULD be retained where relevant.

### 15.6 Reproduction failure

If a previously reported failure cannot be reproduced:

- The original evidence MUST be retained.
- The reproduction attempt MUST receive its own run ID.
- The reproduction outcome MUST be recorded separately.
- The original failure MUST NOT be erased or overwritten.
- A reviewer MUST determine the disposition.

## 16. CI integration

### 16.1 General requirements

KVRF SHOULD integrate with repository CI.

CI execution SHOULD validate:

- Source elaboration.
- Test discovery.
- Required suite execution.
- Evidence generation.
- Evidence-schema validation.
- Artifact publication.
- Required quality gates.

CI MUST preserve the distinction between a test result and an evidence-acceptance decision.

### 16.2 Recommended CI stages

A reference pipeline MAY contain:

1. Repository and source checks.
2. Dependency and environment checks.
3. RTL elaboration.
4. Lint or structural checks.
5. Test discovery.
6. Smoke tests.
7. Functional tests.
8. Regression tests.
9. Coverage collection.
10. Evidence generation.
11. Evidence-schema validation.
12. Artifact publication.
13. Review or acceptance gate.

The exact stage sequence MAY vary by IP category and assurance level.

### 16.3 CI result mapping

CI systems MUST map their native outcomes to the KVRF outcome vocabulary.

A native CI success status MUST NOT automatically imply that every test passed.

A CI failure caused by infrastructure MUST be distinguished from a functional test failure where possible.

A CI job that is skipped MUST NOT be represented as PASS.

### 16.4 Pull request checks

At minimum, a pull request verification workflow SHOULD:

- Elaborate the affected RTL.
- Run applicable smoke tests.
- Run affected functional tests.
- Validate evidence records.
- Publish logs and artifacts.
- Report the source revision tested.

The required pull request gates MUST be defined by the IP repository's verification plan.

### 16.5 Regression scheduling

Repositories MAY define separate CI profiles for:

- Pull request regression.
- Main-branch regression.
- Nightly regression.
- Release regression.
- Configuration-matrix regression.

Each profile MUST identify its suite and configuration scope.

A partial regression MUST NOT be represented as a full regression.

### 16.6 Evidence publication

CI MUST publish or retain evidence artifacts according to the repository's retention policy.

Evidence records MUST identify the CI execution or workflow run when available.

A lifecycle approval MUST reference the accepted evidence, not merely the CI job URL or a summary badge.

### 16.7 CI failure handling

A failed mandatory gate MUST prevent the corresponding verification acceptance.

A blocked or unavailable CI dependency MUST be reported as blocked or otherwise mapped to a non-passing outcome.

Manual override MUST require an explicit, recorded exception and approval.

## 17. Quality and failure management

### 17.1 Failure classification

Verification failures SHOULD be classified to support triage.

Suggested categories:

- RTL functional defect.
- Specification ambiguity.
- Testbench defect.
- Reference-model defect.
- Protocol violation.
- Configuration error.
- Simulator or tool issue.
- Environment or infrastructure failure.
- Coverage-model defect.
- Unknown or under investigation.

The classification MAY be refined during investigation.

### 17.2 Failure records

A failure record SHOULD include:

- Failure identifier.
- IP identifier.
- Run ID.
- Test ID.
- Source revision.
- Configuration.
- Failure category.
- Description.
- Reproduction steps.
- Relevant log references.
- Severity.
- Owner.
- Disposition.
- Closure evidence.

### 17.3 Failure disposition

A failure MUST be dispositioned before it can be considered closed.

Possible dispositions include:

- RTL fix required.
- Testbench fix required.
- Specification clarification required.
- Environment issue resolved.
- Known limitation accepted.
- Not a defect, with rationale.
- Deferred with approved risk.
- Duplicate of another tracked issue.

A deferred failure MUST remain visible in the evidence and issue records.

### 17.4 Regression after fixes

A fix MUST be verified by an appropriate test or suite.

The regression evidence MUST identify the source revision containing the fix.

A test passing on an earlier source revision MUST NOT be used as proof that a later fix is correct.

## 18. Security and verification integrity

### 18.1 Verification input handling

Testbenches SHOULD validate external input files and generated stimulus.

Verification scripts MUST NOT silently ignore malformed configuration or evidence data.

### 18.2 Evidence integrity

Evidence records and artifacts SHOULD be protected against accidental modification.

Where CI supports artifact checksums or immutable storage, those mechanisms SHOULD be used.

### 18.3 Untrusted upstream artifacts

Upstream verification artifacts MAY be used as supporting evidence.

The evidence record MUST identify their origin and source revision.

Unverified upstream claims MUST NOT be represented as KRITVA-executed verification.

### 18.4 Secret handling

Verification logs and evidence artifacts MUST NOT contain credentials, access tokens, or other secrets.

CI workflows MUST use approved secret-handling mechanisms.

## 19. Suggested repository organization

A KVRF-enabled IP repository MAY use the following organization:

~~~text
ip-repository/
├── rtl/
├── verification/
│   ├── README.md
│   ├── requirements/
│   │   └── verification-plan.yaml
│   ├── tests/
│   │   ├── test_smoke.py
│   │   ├── test_registers.py
│   │   └── test_functional.py
│   ├── suites/
│   │   └── suites.yaml
│   ├── models/
│   ├── agents/
│   ├── coverage/
│   ├── config/
│   └── scripts/
├── evidence/
│   ├── schema/
│   ├── records/
│   ├── reports/
│   └── manifests/
└── docs/
    └── VERIFICATION.md
~~~

This layout is illustrative. Repositories MAY use a different structure if the authoritative locations of tests, plans, schemas, and evidence are documented.

## 20. Suggested verification plan

Each IP SHOULD maintain a verification plan.

The plan SHOULD include:

| Field | Description |
|---|---|
| IP identifier | Unique IP identity |
| IP revision | Source revision or baseline |
| Verification owner | Responsible verification owner |
| Assurance target | L0, L1, L2, or L3 |
| DUT boundary | Modules and interfaces under test |
| Requirements baseline | Requirement identifiers and revision |
| Configuration matrix | Supported parameter and configuration values |
| Test suites | Suite IDs and intended scope |
| Coverage model | Coverage categories and targets |
| Toolchain | Tool names and verified versions |
| Environment | Simulator and execution environment |
| Quality gates | Mandatory and advisory gates |
| Evidence destination | Authoritative evidence location |
| Known limitations | Gaps, exclusions, and risks |
| Approval | Reviewer and approver records |

The verification plan MUST be updated when material changes affect the verification scope.

## 21. Example suite definition

The following example is illustrative and does not define a finalized suite schema.

~~~yaml
schema_version: "0.1.0"

suite:
  suite_id: "KVRF-SUITE-EXAMPLE-L2-001"
  name: "Example IP L2 Functional Suite"
  assurance_level: "L2"
  description: "Illustrative functional regression suite"

  ip:
    ip_id: "KIP-IP-EXAMPLE-001"
    source_revision: "TBD"

  configuration:
    configuration_id: "default"
    parameters: {}

  required_tests:
    - test_id: "KVRF-TST-EXAMPLE-SMOKE-001"
    - test_id: "KVRF-TST-EXAMPLE-REG-001"
    - test_id: "KVRF-TST-EXAMPLE-FUNC-001"

  optional_tests: []

  acceptance:
    required_tests_must_pass: true
    blocked_tests_allowed: false
    inconclusive_tests_allowed: false
    evidence_schema_validation_required: true

  coverage:
    requirement_coverage_required: true
    functional_coverage_required: true
    targets: {}

  toolchain:
    simulator: "UNVERIFIED"
    python: "UNVERIFIED"
    cocotb: "UNVERIFIED"

  owner: "Dinesh Annayya"
~~~

## 22. Example test definition

~~~yaml
schema_version: "0.1.0"

test:
  test_id: "KVRF-TST-EXAMPLE-REG-001"
  name: "register_reset_values"
  category: "register"
  description: "Checks documented register reset values"

  ip_id: "KIP-IP-EXAMPLE-001"

  requirements:
    - "IP-REQ-REG-001"

  preconditions:
    - "DUT elaborated with default configuration"
    - "Reset asserted and released according to specification"

  stimulus:
    - "Read documented reset registers"

  expected:
    - "Read values match documented reset values"

  pass_criteria:
    - "All required register values match"

  timeout:
    value: 1000
    unit: "us"

  applicable_levels:
    - "L1"
    - "L2"
    - "L3"

  owner: "Dinesh Annayya"
~~~

## 23. Implementation and toolchain status

### 23.1 Reference toolchain

The reference flow is based on:

| Component | Reference role | Version status |
|---|---|---|
| Python | Testbench language and utilities | UNVERIFIED |
| cocotb | Python-based HDL verification framework | UNVERIFIED |
| SystemVerilog | RTL and verification interface language | UNVERIFIED |
| Simulator | HDL execution | UNVERIFIED |
| Evidence generator | KVRF record generation | TBD |
| Evidence validator | Schema validation | TBD |
| CI platform | Automated execution and publication | UNVERIFIED |
| Coverage tooling | Functional and/or structural coverage | UNVERIFIED |

No specific tool version is approved by this initial specification.

### 23.2 Tool selection

A repository MAY select suitable tools based on:

- Language support.
- Simulator compatibility.
- cocotb support.
- Required protocol features.
- Coverage capabilities.
- CI compatibility.
- Reproducibility.
- Licensing and availability.
- Evidence export capabilities.

The selected toolchain MUST be documented in the verification plan.

### 23.3 Tool changes

A tool or version change MUST be assessed for its potential impact on:

- Test semantics.
- Simulator behavior.
- Timing and scheduling.
- Coverage collection.
- Evidence generation.
- Reproducibility.
- Previously accepted results.

Where a tool change materially affects results, relevant regression MUST be repeated or the impact MUST be explicitly reviewed and approved.

## 24. Compliance

A KVRF implementation is compliant with this specification when:

1. Its verification scope is documented.
2. Tests and suites have stable identifiers.
3. Execution records identify source and configuration.
4. Outcomes use the defined vocabulary.
5. Evidence records conform to the applicable KVRF schema.
6. Evidence artifacts are traceable.
7. Tool versions are recorded or marked UNVERIFIED.
8. Applicable assurance-level gates are addressed.
9. Failures and exclusions are dispositioned.
10. CI results preserve the distinction between execution and acceptance.
11. Evidence is reproducible to the extent required by the declared assurance level.
12. The verification plan and evidence are reviewed at the required level.

Compliance status MUST distinguish:

- `COMPLIANT`
- `NON_COMPLIANT`
- `PARTIALLY_COMPLIANT`
- `NOT_ASSESSED`
- `NOT_APPLICABLE`

A `NOT_ASSESSED` result MUST NOT be represented as compliant.

A schema-valid evidence record alone MUST NOT establish compliance with this specification.

## 25. Open items

The following items remain open for KVRF finalization. Each item is owned by Dinesh Annayya.

| ID | Open item | Required decision |
|---|---|---|
| KVRF-OI-001 | Evidence schema | Approve the canonical JSON schema, field types, and validation rules. |
| KVRF-OI-002 | Schema versioning | Define compatibility and migration rules for evidence schema versions. |
| KVRF-OI-003 | Test ID convention | Approve the canonical test and suite identifier formats. |
| KVRF-OI-004 | Run ID convention | Approve the canonical run identifier format and uniqueness scope. |
| KVRF-OI-005 | Evidence storage | Define authoritative evidence storage and retention locations. |
| KVRF-OI-006 | Artifact integrity | Define required checksums, manifests, and integrity controls. |
| KVRF-OI-007 | Reference implementation | Select and publish the initial reference KVRF implementation. |
| KVRF-OI-008 | Python and cocotb versions | Select and verify supported Python and cocotb versions. |
| KVRF-OI-009 | Simulator support | Identify supported simulator implementations and compatibility expectations. |
| KVRF-OI-010 | SystemVerilog support | Define the required SystemVerilog language subset and simulator compatibility checks. |
| KVRF-OI-011 | Coverage schema | Define the canonical coverage evidence representation. |
| KVRF-OI-012 | L2 coverage gate | Define minimum category-specific coverage expectations for L2. |
| KVRF-OI-013 | L3 coverage gate | Define release-scope coverage targets and exclusion approval requirements. |
| KVRF-OI-014 | Requirement traceability | Define the canonical requirement-to-test/evidence mapping format. |
| KVRF-OI-015 | APB BFM | Define the supported APB profile and reference BFM requirements. |
| KVRF-OI-016 | Register test generation | Decide whether machine-readable register descriptions are required or recommended. |
| KVRF-OI-017 | CI reference pipeline | Publish a reusable CI pipeline and evidence publication contract. |
| KVRF-OI-018 | Reproducibility | Define minimum environment capture and reproducibility requirements by assurance level. |
| KVRF-OI-019 | Failure taxonomy | Approve severity and disposition conventions for verification failures. |
| KVRF-OI-020 | Evidence review authority | Confirm roles authorized to accept KVRF evidence for L2 and L3. |
| KVRF-OI-021 | Upstream evidence acceptance | Define minimum review requirements for accepting upstream-native evidence. |
| KVRF-OI-022 | Evidence retention | Define retention periods for test records, logs, coverage reports, and release evidence. |
| KVRF-OI-023 | Security controls | Define required controls for verification scripts, external inputs, and CI secrets. |
| KVRF-OI-024 | Compliance automation | Decide which KVRF checks are mandatory CI gates and which are advisory. |

No open item is considered approved by its inclusion in this table.

An open item MUST be closed through an explicit owner decision and, where required, a revision to this specification or its supporting schemas.

## 26. Change control

Changes to this specification MUST be reviewed and approved by the designated KVRF owner or authorized delegate.

Changes MUST preserve:

- Existing test and suite identifiers.
- Historical execution records.
- Evidence traceability.
- Source and configuration identity.
- Historical outcome semantics.
- Assurance-level assessment history.

A specification revision MUST identify material changes and their impact on existing evidence and verification implementations.

A schema change MUST define compatibility and migration requirements.

### 26.1 Versioning

This specification uses semantic versioning:

- MAJOR: incompatible changes to evidence semantics, required fields, outcome definitions, or reference-flow requirements.
- MINOR: compatible additions to requirements, evidence fields, or verification capabilities.
- PATCH: editorial corrections and non-semantic clarifications.

The initial version is `0.1.0`, with status `DRAFT`.

### 26.2 Review history

| Version | Date | Author | Status | Description |
|---|---|---|---|---|
| 0.1.0 | TBD | Dinesh Annayya | DRAFT | Initial KRITVA Verification Reference Flow specification. |

## 27. References

1. KRITVA IP Standard.
2. KRITVA IP Lifecycle Policy.
3. KRITVA IP Adoption Process.
4. KRITVA IP Customization Policy.
5. KRITVA IP Upstream Maintenance Policy.
6. Applicable IP specifications and requirement baselines.
7. Applicable KVRF evidence schema and validator.
8. Python documentation.
9. cocotb documentation.
10. SystemVerilog language reference.
11. Applicable APB specification and approved KRITVA interface profile.
12. Applicable simulator and verification-tool documentation.

External standards, tools, and frameworks MUST be referenced by verified version or revision when used for an acceptance decision. Unverified versions MUST be marked `UNVERIFIED`.

---

**End of Document**
