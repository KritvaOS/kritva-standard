# Engineering Contract revision notes

| Property | Value |
|---|---|
| Document | Review notes and proposed revision for the Engineering Contract |
| Status | PROPOSED (Task KOS-STD-004); not approved |
| Owner | Dinesha Annayya (`dineshannayya`) |
| Last Updated | 2026-11-16 |

The authoritative DRAFT is `common/contract/ENGINEERING_CONTRACT.md` (SHA-256 `b57e24ba9771b0d1…`, equal to the copy pinned in kritva-core). It is unchanged. The proposed revision is [ENGINEERING_CONTRACT.proposed.md](ENGINEERING_CONTRACT.proposed.md) (SHA-256 `f46d0b34b1447887092c8c37f137906218ef43fd6245be9ac25ca0e09e4746e5`). Approving it replaces the DRAFT text, and the pin must then move (see Approval steps).

## Owner decisions applied (2026-11-16)

1. Pin design: kritva-standard is authoritative; core keeps a byte-identical pinned copy; kritva-program checks that every pinned copy equals the authoritative copy.
2. Applicability: sections 6 and 8 apply by repository type (engineering, documents-only, planning and program).

## Changes in the proposed text

| Place | Change |
|---|---|
| Scope | The acceptance standard citation names the kritva-standard copy as authoritative from 2026-11-15 |
| New section "Applicability" | Table of repository types and the sections that apply; the two workflows and the commit checker are required in every type |
| Section 3, item 6 | States that each repository keeps a local checker, the kritva-program copy is the base, and local copies differ only in the header block |
| Section 9, new item 5 | Authoritative copy in kritva-standard; pinned repositories keep a byte-identical copy; kritva-program checks the copies |

No rule about branches, commit format, definition of done, milestone closure, test gates or tags changed.

## Known gaps that follow from the text

kritva-standard does not yet meet the "required in every type" line: it has no `secret-scan` or `commit-message-check` workflow and no local commit checker (decision D-12 says repositories keep the scripts their local commit needs). Tracked as KOS-STD-014.

## Approval steps (Owner)

1. Review `ENGINEERING_CONTRACT.proposed.md`.
2. Record the approval as a kritva-program decision, with the SHA-256 above.
3. Replace `common/contract/ENGINEERING_CONTRACT.md` with the approved text in a kritva-standard PR; update its hash in `common/README.md`.
4. After that merge, replace core's copy with the identical file and update core's `ENGINEERING_CONTRACT.pin.json` (new `sha256`, new `commit_sha`) in a separate PR, because a commit cannot contain its own SHA.
5. Add the program-level check that every pinned copy equals the authoritative SHA-256.
