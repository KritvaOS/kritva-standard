# Proposals for kritva-program decision records

| Property | Value |
|---|---|
| Document | Draft proposals for kritva-program (not entered in any ledger) |
| Status | PROPOSED; only the Owner approves, and only in kritva-program |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Last Updated | 2026-11-15 |

Nothing in this file is a decision. It is wording the Owner can adopt in the kritva-program decision log. Approval is recorded there by the Owner's own `--approve` run, not here.

## P-1 Engineering Contract approval and pin (Task KOS-STD-004)

Proposed decision: approve `ENGINEERING_CONTRACT.md` as the common engineering contract, with the authoritative copy at `common/contract/ENGINEERING_CONTRACT.md` in kritva-standard.

Basis: the copy in kritva-standard is byte-identical to the DRAFT pinned in kritva-core (SHA-256 starting `b57e24ba`, core pin commit starting `71a82e9b`; full values are in core's pin file and in `common/README.md`).

Proposed steps, in order:

1. The Owner reviews the contract text and records any change requests.
2. The Owner records the approval as a new kritva-program decision, which supersedes the DRAFT status noted in D-023 and D-113 only to the extent the text says.
3. Core's pin is updated to point at the kritva-standard copy before core's own copy is removed.
4. kritva-program gains a program-level check that every repository pins the same contract hash.

Open for the Owner: whether the contract keeps controlling over the acceptance standard where they differ (as the DRAFT states).

## P-2 Visibility classes (Task KOS-STD-003)

Proposed records:

| Repository | Proposed class | Header consequence |
|---|---|---|
| kritva-standard | PUBLIC (GitHub setting seen as public on 2026-11-14) | Public header |
| kritva-nexus | PRIVATE | Private header (`All rights reserved.`) |

kritva-nexus's class is a proposal from the Owner's earlier direction and has not been recorded; kritva-enterprise-program was not connected, so its header is unchecked.

## P-3 Copyright holder rollout

See `COPYRIGHT_ROLLOUT_PLAN.md`. Proposed as one decision that records D-1 (holder `Kritva Robotics Private Limited`) and the transition plan for the header lints.
