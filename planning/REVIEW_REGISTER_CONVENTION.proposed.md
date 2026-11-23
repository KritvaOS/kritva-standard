# Per-repository review register convention (proposed)

Copyright (c) 2026 Kritva Robotics Private Limited.
SPDX-License-Identifier: Apache-2.0

| Field | Value |
|---|---|
| Document ID | Not allocated (KSTD-GOV-006 proposed if adopted) |
| Document | Per-repository review register convention |
| Repository | `KritvaOS/kritva-standard` |
| Version | 0.1.0 |
| Status | PROPOSED. A recommendation, not a decision and not normative |
| Classification | PUBLIC |
| Owner | Dinesh Annayya (`dineshannayya`) |
| Reviewer / Approver | Not yet assigned. Owner approval is provisional and is not independent review |
| Last Updated | 2026-11-23 |
| Authority | INPUT (proposal for Owner review) |
| Related Tasks | KOS-STD-015 (repository-local proposal; no weight, no credit) |
| Related Documents | [GOVERNANCE.md](../GOVERNANCE.md), [AGENTS.md](../AGENTS.md), [PROPOSALS_FOR_KRITVA_PROGRAM.md](PROPOSALS_FOR_KRITVA_PROGRAM.md) |

> **Status notice:** Nothing here is approved. It adds no requirement to any repository, changes no existing register, and gives no program credit. It becomes guidance only after explicit Owner approval recorded against a repository commit (GOVERNANCE section 2).

## 1. Why

Owner approvals given in chat, or as a provisional stand-in for roles that are not yet filled, are easy to lose and easy to mistake for accepted decisions. A repository needs one place that says where each such decision lives, who approved it and in what form, and when it should be looked at again. The `kritva-connect` repository already keeps such an index (`planning/REVIEW_REGISTER.md`), and the format has settled enough to write down.

## 2. What the convention recommends

The convention is a recommendation. It is not mandatory and it is not retroactive. A repository adopts it by choice, and a repository that does not adopt it is not out of conformance.

### 2.1 One register per repository

Each repository that adopts the convention keeps one register at `planning/REVIEW_REGISTER.md` (or the nearest equivalent planning folder). A register covers only the decisions that repository owns. Public and private repositories keep separate registers, so a public register never needs to mention a private one.

### 2.2 The register is an index only

A register points to records; it does not hold them.

1. It copies no decision text and no approval state. The "Authoritative record" column says where the decision lives, and that record wins if the two differ.
2. A row with no repository record is marked **Not yet recorded**. It is only as strong as the cited statement and is not an approved decision.
3. A register does not replace a repository's decision log, ADRs or program decisions. It creates none and supersedes none.

### 2.3 Row identity and fields

Row IDs use `<REPO>-REV-nn`, where `<REPO>` is a short upper-case repository code. An ID is never renumbered or reused, including after a row is closed or replaced (the same rule as GOVERNANCE section 4).

| Field | Meaning |
|---|---|
| ID | `<REPO>-REV-nn` |
| Subject | One sentence naming the decision or area. No decision body |
| Authoritative record | Link to the record that holds the decision, with a commit, merge or run identifier where one exists; or **Not yet recorded** |
| Approval basis | Who approved it and in what form (for example an owner statement and its date, or a recorded approval). Evidence, not a status |
| Reopen when | The condition that makes the decision worth revisiting |
| Re-review by | The role or review that should look again |
| Open items | What is missing or unverified. "None" is a valid entry |

### 2.4 Provisional and accepted

A register separates two states and never blurs them.

1. **Provisional**: the Owner approved it, but no independent reviewer has. The register says so in plain words and lists it under "awaiting re-review".
2. **Accepted**: the repository's own approval process has recorded the approval against a commit. An accepted row links that record; the register does not become the approval.

A row moves from provisional to accepted only when the authoritative record says so. Editing the register alone never changes a decision's status.

### 2.5 Owner and reviewer authority

1. The Owner may record a provisional approval. It stands in for the accountable roles for now and is never described as independent review (GOVERNANCE section 2).
2. A register names the reviewer role it still needs, not only the person. Reviews that are pending but not tied to a row go in a separate "reviews still pending" table.
3. Delegation needs an Owner decision (GOV-OI-001). The register does not create or imply delegation.
4. AI-assisted drafting is advisory. A register may say a row rests on AI-assisted drafting; it never counts that as review.

### 2.6 Evidence and commit pinning

1. A link to a decision or contract names an immutable identifier: a commit SHA, merge commit, pull request number or run ID. It does not name a branch (GOVERNANCE section 11).
2. A register that is itself pinned by another repository's record names the commit it was pinned at. A later register edit does not move the pin.
3. Software checks, calculations and simulation are not presented as physical, silicon or safety validation.

### 2.7 Conditions and re-review

1. Every row has a "Reopen when" condition. A row with a date-based expiry says so there, and the date is ISO (`YYYY-MM-DD`).
2. A reopened row is not edited in place into a new decision. The old row records what superseded it and points to the new row or record; the old ID stays.
3. Rows are reviewed when their reopen condition occurs or when the named re-review happens, not on a calendar unless the row says so.

### 2.8 Baseline and credit restrictions

A register and its rows are not baselines. They create no task, weight, estimate, gate, approval-ledger entry or credit. Every register states this near the top. Baselining and credit stay in `kritva-program` (GOVERNANCE section 3).

### 2.9 Public and private content

1. A public register holds no private rule text, credentials, customer data, contract terms or private infrastructure detail (GOVERNANCE section 7).
2. A public register does not name a private repository's register, path, rows, commits or decision IDs. Where a decision genuinely lives in a private repository, the row says "recorded in a private repository" or cites only what the public record already states.
3. A private register may link to public records. The reverse is not allowed.
4. The `kritva-program` records link to a public repository's register by name and commit. They do not copy rows.

### 2.10 Linking and upkeep

1. A repository that adopts the convention links its register from its README documents table and from its agent rules, so a contributor or agent finds it.
2. Changes to a register follow that repository's change process and carry a change log row. A planning change in a repository that keeps its own planning log is entered there.
3. A register is edited only when a record, an approval or a reopen condition changes. It is not a progress report.

## 3. Register skeleton

An adopting repository can start from this skeleton. It follows the header standard for detailed documents and has no sample rows.

```markdown
# <Repo>: Review Register

| Property | Value |
|---|---|
| Document ID | <REPO>-PLAN-REVIEW-REGISTER |
| Repository | `KritvaOS/<repo>` (public or private) |
| Document Type | Report (index) |
| Status | PROPOSED. Nothing here is a baseline, task, weight, estimate, gate or credit |
| Owner | <role> |
| Reviewer/Approver | <not yet assigned, or role> |
| Version | 0.1 |
| Last Updated | <YYYY-MM-DD> |
| Authority | REFERENCE (index only; the linked records govern) |

## Format
<Short statement of sections 2.2 and 2.3 of the convention.>

## 1. Provisional owner approvals awaiting re-review

| ID | Subject | Authoritative record | Approval basis | Reopen when | Re-review by | Open items |
|---|---|---|---|---|---|---|

## 2. Reviews still pending

| Review | Covers | Needed before |
|---|---|---|

## 3. Not approved

## 4. Program links

## 5. Change log

| Date | Change |
|---|---|
```

## 4. What this proposal does not do

1. It does not change, renumber or require changes to any existing register or record in any repository.
2. It does not make the convention mandatory, and it adds no check to any repository or to `kritva-program`.
3. It does not edit GOVERNANCE.md, AGENTS.md, README.md or any copied file under `common/`.
4. It does not approve any decision that an existing register lists, and it creates no program decision, baseline, task weight, gate or credit.

## 5. Adoption path (all steps need the Owner)

1. The Owner reviews this text and records any change requests.
2. If adopted, the Owner approves it as guidance and the approval is recorded against a repository commit. Whether it becomes `KSTD-GOV-006` is an Owner choice.
3. Only after that, any repository decides on its own whether to adopt it.
4. Any program-level check for register conformance would be a separate `kritva-program` proposal and is not suggested here.

## 6. Open items

| ID | Item |
|---|---|
| RRC-OI-001 | Whether the convention should be a standalone `KSTD-GOV` document or a short section in GOVERNANCE.md |
| RRC-OI-002 | Whether `planning/REVIEW_REGISTER.md` is the fixed path or only the default |
| RRC-OI-003 | Whether the skeleton belongs under `common/` as a template once the convention is approved |
| RRC-OI-004 | Reviewer roles are still unassigned (GOV-OI-001), so "Re-review by" names a review, not a person |

---

**End of document**
