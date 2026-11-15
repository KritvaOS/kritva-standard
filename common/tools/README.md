# Common tools

Copyright (c) 2026 Kritva Robotics Private Limited.
SPDX-License-Identifier: Apache-2.0

| Field | Value |
|---|---|
| Document | Index of common checker scripts |
| Repository | `KritvaOS/kritva-standard` |
| Version | 0.2.0 |
| Status | DRAFT |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Last Updated | 2026-11-15 |

**Final decision, 2026-11-15: scripts needed for a local commit live inside the local folder of each repository. All program-level checks, including standard-conformance checks, live in kritva-program. kritva-standard holds no authoritative scripts. The copies in this folder are reference copies only; they are not authoritative and are due for removal once the setup is clean.**

Earlier the same day the Owner decided that the common scripts (`check_readme.py`, `check_commit_format.py` and the other common scripts) move to `common/tools/`; that decision, and the intermediate one that all checkers stay in kritva-program, are superseded by the one above. This index records what was copied, what each copy was based on, and what is not yet done. Nothing here is approved, and no repository has been changed to use these copies.

## 1. Copied files (verbatim)

All files are byte-for-byte copies. They have no copyright header and refer to `kritva-program` paths, as in the source.

| File here | Source | SHA-256 |
|---|---|---|
| [readme/check_readme.py](readme/check_readme.py) | kritva-program scripts/docs/ | `ed2b3b4e924ecae3b7d437a2a2683db9a0deb7316b650d145e933e72c541bd84` |
| [readme/test_check_readme.py](readme/test_check_readme.py) | kritva-program tests/ | `d4472495bb009fe89e7c7bb4c6cc9a30af7b65d8adbedd8e8e212b5a689b7fc7` |
| [commit/check_commit_format.py](commit/check_commit_format.py) | kritva-program scripts/security/ | `aec47664e4bb65336d19bd5f4614c0877d1f09b2ed0e8876b96e859848df0a5d` |
| [commit/check_commit_messages.py](commit/check_commit_messages.py) | kritva-program scripts/security/ | `4bf75f3dcb032cbee4eb93d734efcdaf6ff58bcf5e7264d660d93b83e95c911d` |
| [commit/test_check_commit_messages.py](commit/test_check_commit_messages.py) | kritva-program tests/commit_message_check/ | `7f185860d0053f079875dea75304b298471c8c56a77673dd1e6793b14469ac74` |
| [gate/pr_gate.py](gate/pr_gate.py) | kritva-program scripts/pipeline/ (identical to kritva-sense) | `ec80b1e300a7b3c768e693c2dd5c15f0497a7f9240531b5f8fdb158f271e9cae` |
| [status/progress_report.py](status/progress_report.py) | kritva-core scripts/ (identical in core, sense, community) | `c856a24c3503b1a84015442c99719c154805251a9c462d87d24a09effc7215a2` |
| [contract/check_contract_pin.py](contract/check_contract_pin.py) | kritva-core scripts/contract/ | `e29c84c78e6f741a066fc26f39a4acc57b10b24aa189c05eceef0ae5f31c1a4f` |
| [contract/test_check_contract_pin.py](contract/test_check_contract_pin.py) | kritva-core scripts/contract/ | `cf66fcea521ded2e3c5fe94962d338af541b43387f4a9b7f387b7cfced309860` |

## 2. Variants found in the repositories

Repositories carry their own copies of these scripts. The copies are not all identical.

| Script | Variants (SHA-256 prefix, where) | Basis chosen here |
|---|---|---|
| check_commit_format.py | `aec47664e4bb` kritva-program; `c54e9f026fc0` kritva-sense; `fdaa62e9d5b8` kritva-core and kritvaos-community | **Decided by the Owner, 2026-11-15: the kritva-program version is the standard commit format checker.** Compared with core and sense, the only differences found were the header block and the wording of the opening docstring. The core, community and sense copies are to be replaced by this one (TLS-OI-004) |
| check_commit_messages.py | program and sense 2,492 bytes; core 3,099; community 3,084 | kritva-program. Compared with core: header block and docstring position only |
| check_readme.py | program 4,859 bytes; sense 4,882; core 5,494; community 5,497 | kritva-program. Compared with core and sense: header block and docstring wording only. Not compared in full against community, mind, motion or skill |
| progress_report.py | identical in core, sense and community | any copy |
| pr_gate.py | identical in program and sense | either copy |
| check_source_headers.py | core 5,231 bytes; community 7,869 | **Not copied.** The two versions differ in size, and both require the text `Copyright (c) 2026 KritvaOS`. They must change together with the copyright decision (see section 4) |

Copies in kritva-mind, kritva-motion and kritva-skill were not inspected.

## 3. Not moved

| Item | Reason |
|---|---|
| `kritva-program/tools/*` (baseline, approvals, consolidation, dashboard, planning inventory, and similar) | Planning and status-monitoring tooling; stays in `kritva-program` |
| `scripts/pipeline/` manifest, ship, merge and PR-open scripts, and `pr_check.py` | Program pipeline tooling driven by `repo-pipeline.json`; stays in `kritva-program` unless you decide otherwise |
| `kritva-core/scripts/audit/*`, `gen_status.py`, `check_toolchain.py` | Specific to one repository's API, status or toolchain; not common. `gen_status.py` has differing versions in core and community and is a candidate once a base is chosen |

## 4. Cautions

1. **No repository uses these copies yet.** Repository Makefiles and CI call their own local copies. Switching them is a separate change in each repository.
2. **Copied tests do not run at the new location.** They set their import path relative to their old repository layout (for example `scripts/docs`, `scripts/security`). They are kept verbatim for traceability. They need a path adaptation before use.
3. **The README checker applied to this repository's new README fails.** It reports missing sections (milestones, tasks and acceptance, status reporting, validation, safety and security, release, ownership, related repositories). The README standard assumes a full 18-topic README. Whether `kritva-standard`, as a documentation repository, follows all topics or records an exception under section 12 of the standard is open.
4. **Copyright wording.** The source scripts that carry headers say `Copyright (c) 2026 KritvaOS`. The copies here have no header. Adding the `Kritva Robotics Private Limited` header changes the file hashes and so needs its own recorded step.

## 5. Open items

| ID | Item |
|---|---|
| TLS-OI-001 | Choose the canonical `check_source_headers.py` base, change the required copyright text to `Kritva Robotics Private Limited`, and update the header lint configuration in core and community together with their headers |
| TLS-OI-002 | Adapt the copied tests to the new layout and run them |
| TLS-OI-003 | Add headers to the copied scripts (public header from GOVERNANCE.md section 8) |
| TLS-OI-004 | Decide how repositories consume the tools (vendored copy, submodule or fetch), and when each repository's local copy is removed |
| TLS-OI-005 | Inspect the copies in kritva-mind, kritva-motion and kritva-skill and compare with the base |
| TLS-OI-006 | Decide whether `gen_status.py` and the pipeline gate scripts become common tools |
| TLS-OI-007 | README checker compliance of this repository (section 4, item 3): resolved 2026-11-15, the README passes the kritva-program checker |
| TLS-OI-008 | Approve the local and program-level split and the drift control in section 6 |

## 6. Local and program-level copies (DRAFT proposal, refines the decision above)

Owner preference, 2026-11-15: where needed, keep both copies, the program-level checker in kritva-program and the local checker in the repository that commits. This section proposes which checker belongs where. It is not approved.

| Checker | Local copy (repository, at commit) | Program-level copy (kritva-program, CI and approval) |
|---|---|---|
| Commit format (`check_commit_format.py`) | Yes | Yes; the kritva-program version is the standard (decided) |
| Commit message, no AI-session metadata (`check_commit_messages.py`) | Yes | Yes |
| README structure (`check_readme.py`) | Optional, for authors | Yes, as the standard check across repositories |
| PR acceptance gate (`pr_gate.py`) | No | Yes (a copy is also vendored in capability repositories today) |
| Source header lint (`check_source_headers.py`) | Yes, repository-specific | No; the program may check that the lint exists |
| Contract pin check (`check_contract_pin.py`) | In kritva-core, which pins its own copy of the contract | Program-level check that every repository pins the same contract |
| Status generation and progress report | Yes, each repository generates its own status | Consolidation and verification only |

**Drift control (proposed).** Two copies drift. The commit format checker already exists in three versions across the repositories (see section 2). To keep both copies honest:

1. The kritva-program copy is the base. A local copy is byte-identical to it, or differs only in its leading header block.
2. The program-level compliance report (`engineering_compliance.py` already reads each repository's default branch) records the SHA-256 of each local checker body and flags any that differ from the base.
3. A local copy is changed only by copying the new base and recording the change; the base changes through the Owner-approved process.

**Open:** which repositories need which local checkers, how the header block is excluded from the comparison, and whether the existing differing copies are replaced in one step (TLS-OI-004, TLS-OI-008).

