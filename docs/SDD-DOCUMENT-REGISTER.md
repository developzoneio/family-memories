# Family Memories — SDD Document Register & Generation Checklist

> **Document ID:** SDD-REG-001  
> **Version:** 1.1.0  
> **Last updated:** 2026-11-11  
> **Owner:** Project maintainer  
> **Status:** Active — Step 2 reconciled (Reviewed with Open Gaps)  
> **Canonical repository path:** `docs/SDD-DOCUMENT-REGISTER.md`

## 1. Purpose and rules

This document is the **single inventory and generation checklist** for Family Memories' Spec-Driven Development (SDD) artifacts. It answers:

1. Which documents **exist as actual files**?
2. Which documents are **approved, draft, outdated, or missing**?
3. Which documents must be created or reviewed **before the next SDD phase**?
4. How must ChatGPT and Codex CLI update the inventory whenever they generate, rename, approve, or supersede a document?

**Critical distinction:** Prior ChatGPT design discussions are not automatically repository documents. For this review, the actual remote GitHub branch `feature/001-project-foundation` was inspected on 2026-11-11. The file inventory below distinguishes nonempty Markdown content, zero-byte placeholders, and genuinely missing files. Content in earlier chat summaries does not prove that the detailed design has been exported or fully verified. The local working tree was not inspected.

### Document lifecycle

- **File presence:** `Exists (GitHub; content)` / `Placeholder (0 bytes)` / `Missing` / `Chat only`.
- **Review state:** `Approved` / `Draft` / `Pending review` / `Not started` / `N/A` / `Superseded`.
- **Repository state:** inspected on remote GitHub branch `feature/001-project-foundation` as of 2026-11-11; local checkout remains unverified.
- Approval is a **human decision**; generating a document does not approve it.
- A required file must not be marked `Exists` solely because its name is listed in a plan.
- Keep document **status**, **version**, and **last-updated date** in sync with this register. Record discrepancies transparently until resolved.

## 2. Current artifact inventory (as of 2026-11-11)

### A. SDD governance and Milestone 1

| ID | Document | Intended repository path | File presence | Review state | Notes / next action |
|---|---|---|---|---|---|
| GOV-001 | Project SDD README | `README.md` | Exists (GitHub; content) | Active; references outdated | References and document status require alignment; GAP-01/GAP-02 remain open. |
| GOV-002 | **SDD Document Register** | `docs/SDD-DOCUMENT-REGISTER.md` | Exists (GitHub; content) | Active — Step 2 reviewed | This register records DR-001/DR-002 and open gaps; it is not proof that underlying designs were reconciled in full. |
| SDD-001 | SPEC-001 requirements | `docs/specs/001-project-foundation/spec.md` | Exists (GitHub; content) | **Approved (recorded), 2026-11-11** | v1.0.0 approved scope; checklist audit remains pending. |
| SDD-002 | SPEC-001 review checklist | `docs/specs/001-project-foundation/checklists/requirements.md` | Exists (GitHub; content) | Scope approval recorded; audit open | Individual unchecked attestations are not approved by implication. |
| SDD-003 | SPEC-001 technical plan | `docs/specs/001-project-foundation/plan.md` | Exists (GitHub; content) | **Draft — not approved** | Existing planning draft, not modified or ratified by Document Reconciliation. |
| SDD-004 | SPEC-001 implementation tasks | `docs/specs/001-project-foundation/tasks.md` | **Placeholder (0 bytes)** | Not started | Empty file is not a task breakdown; do not populate before plan approval. |
| SDD-005 | Implementation verification report | `docs/specs/001-project-foundation/verification.md` | **Missing** | Not started | Deferred until implementation and acceptance evidence exist. |
| ADR-001 | Architecture Decision Records | `docs/adr/` | **Placeholder (0-byte README)** | Not started / conditional | Create actual ADRs only for decisions requiring durable rationale; no duplicate ADR location. |

### B. Product, frontend and backend design sources

| ID | Document | Intended repository path | File presence | Review state | Why it matters |
|---|---|---|---|---|---|
| DES-001 | Product Requirements / Product Scope baseline | `docs/product/requirements.md` | **Placeholder (0 bytes)** | Partial Approved / Unverified | Product decisions exist in chat/SPEC-001, but no content in canonical file; full product baseline not verified. |
| DES-002 | **Backend Design** | `docs/architecture/backend-design.md` | **Placeholder (0 bytes)** | Unverified | Backend stack/architecture details require original discussion or supporting design source. |
| DES-003 | **Frontend Design** | `docs/architecture/frontend-design.md` | **Placeholder (0 bytes)** | Partial Approved / Unverified | React and responsive browser mockup decisions recorded in chat; detailed technology and UX design need source reconciliation. |
| DES-004 | **Technical Design Document (TDD)** | `docs/architecture/technical-design.md` | **Placeholder (0 bytes)** | Unverified | Original Milestone 1 scope and cross-cutting decisions not yet verified. |
| DES-005 | UI/UX mockup specification or references | `docs/design/ui-ux-reference.md` | **Missing (chat only)** | Mockup approved in chat; file unverified | No confirmed canonical screenshot or reference file on this branch; do not invent one. |

**Confirmed from prior project discussions, not from files:** React frontend, home self-hosting, medium scale, family-scoped privacy, manual image upload, support for original and optimized image renditions. Exact backend version, DB engine, CSS/UI library, local OS, and CI provider remain **planning decisions pending reconciliation**, not settled by this register.

### Snapshot / status counts (remote GitHub branch, 2026-11-11)

- **13 tracked files verified** on `feature/001-project-foundation`: **7 nonempty** (README, docs/README, Document Register, SPEC-001, plan, checklist, .gitignore) and **6 zero-byte placeholders** (Product, Backend, Frontend, Technical Design, ADR README, tasks).
- **1 approved requirements specification** (SPEC-001 v1.0.0; approval recorded, checklist audit pending).
- **1 draft technical plan** (`plan.md`, not approved).
- **4 empty canonical product/architecture source files**; the approved UI/UX mockup is not verified as a canonical repository reference.
- **1 empty tasks placeholder** and **1 missing verification report**; ADRs are conditional and no substantive ADR exists.
- **Phase 1 — Foundation Inventory / Step 2: Document Reconciliation**: **Completed — Reviewed with Open Gaps**, approved by project maintainer on 2026-11-11. No gaps closed by this review.

## 3. Milestone 1 readiness checklist

### Gate A — Requirements (Specify / Approve)

- [x] Generate SPEC-001 functional and nonfunctional requirements with acceptance tests.
- [x] Maintainer approves SPEC-001 in chat (2026-11-11).
- [x] Update the generated `spec.md` approval metadata and review checklist without changing substantive scope. (Git commit still unverified.)
- [x] Confirm SPEC-001, review checklist, README, and this register exist on the inspected remote feature branch (2026-11-11; local checkout not reviewed).

### Gate B — Architecture (Plan)

- [ ] Generate `docs/architecture/backend-design.md` from the prior approved Backend Design decisions; label any inferred choices as proposals.
- [ ] Generate `docs/architecture/frontend-design.md` from prior Frontend Design decisions and approved mockup context.
- [ ] Generate `docs/architecture/technical-design.md` or explicitly document where the Milestone 1 TDD decisions are captured.
- [ ] Reconcile scope conflict (SPEC-001 foundation versus any broader Milestone 1 in the TDD).
- [ ] Resolve or explicitly approve assumptions for SPEC-001 open questions **OQ-001 … OQ-005**: scope, backend stack, primary development OS, local infrastructure, CI.
- [ ] Review and finalize `docs/specs/001-project-foundation/plan.md` against the above design files.
- [ ] Maintainer approves `plan.md` and records date/version.

### Gate C — Task planning (Tasks)

- [ ] Generate `docs/specs/001-project-foundation/tasks.md` from the **approved** plan.
- [ ] Ensure each executable task traces to an FR/NFR and/or AT ID.
- [ ] Verify dependencies and task order; do not add features excluded from SPEC-001.

### Gate D — Implementation and acceptance

- [ ] Implement the foundation using the approved plan and tasks.
- [ ] Run/document acceptance scenarios **AT-001 … AT-011**.
- [ ] Generate `verification.md` with pass/fail evidence and remaining gaps.
- [ ] Review/merge changes after checks pass and update this register.

**SDD implementation gate:** **B — Architecture (Plan draft, not approved)**. **Foundation Inventory Phase 1, Step 2 is complete at review level only**. The Backend/Frontend/TDD paths contain empty placeholders, not usable design content. This approval does not authorize code, new planning work or Constitution Review.

## 4. Dependencies between documents

```text
Prior design decisions in chat
        │
        ├── [Empty] Backend Design file ──────┐
        ├── [Empty] Frontend Design file ─────┼──> Reconcile [Draft] plan.md
        └── [Empty] TDD file ─────────────────┘              │
                                                            v
[Approved (recorded)] SPEC-001 spec.md ─────────> [Draft] plan.md (approval pending)
                                                            │
                                                            v
                                                       tasks.md (empty placeholder)
                                                            │
                                                            v
                                                 Implementation + tests
                                                            │
                                                            v
                                                 verification.md (missing)

Every new document/update ─────────> update this register in the same change
```

The register is the inventory, **not** a replacement for the full content of missing architecture documents.

## 5. Mandatory update procedure — ChatGPT and Codex CLI

When **any** project document is generated, imported, renamed, approved, revised materially, or superseded:

1. **Verify the actual file exists** at its canonical repository path (or record that it exists only as a generated chat attachment awaiting copy).
2. **Add or update one row** in Section 2. Use a stable ID; include path, file presence, approval state and follow-up.
3. **Update the corresponding checkbox(es)** in Section 3. Only check tasks whose result was actually verified.
4. **Update metadata** at the top of this register: version and last-updated date. Add a concise entry to Section 8.
5. **Keep counts in Section 2 accurate**; do not imply a file is committed unless Git actually confirms it.
6. **Commit register updates in the same Git commit/PR** as the document change. Where possible, link reviewers to both.
7. For **source-code-only changes**, no register update is required unless document status, planned scope or acceptance evidence changed.

> **Automation limit:** This Markdown file cannot self-update when the Git repository changes. ChatGPT will update it when we create documents **in a session where the latest register is supplied or accessible**. Codex CLI can update it when instructed to do so (for example via the prompt below, or a repository-level `AGENTS.md` policy). No watcher or Git hook has been installed by this file.

### Reusable Codex CLI instruction

Copy the following into Codex CLI when performing documentation work:

```text
Read docs/SDD-DOCUMENT-REGISTER.md first.
Scan the repository to verify which referenced files actually exist.
Treat the register as an inventory, not as evidence that missing files exist.
Perform the requested document work only within the current approved SDD gate.
Whenever you create, revise, rename, or approve a document, update
  docs/SDD-DOCUMENT-REGISTER.md in the same change:
  - file presence, canonical path, review/approval state and version
  - Milestone 1 checklist and dependency blockers
  - status counts, last-updated date and change history
Do not mark documents Approved without explicit maintainer approval.
Do not assume previous ChatGPT sessions are available in this repository.
Do not start implementation until plan.md is approved and tasks.md is prepared.
Report missing inputs and contradictions instead of fabricating design decisions.
```

## 6. Next recommended documentation sequence

1. **Export Backend Design** into `docs/architecture/backend-design.md` (use prior conversation material or a supplied review copy; distinguish confirmed decisions from proposals).
2. **Export Frontend Design** into `docs/architecture/frontend-design.md`, including approved responsive browser UX constraints.
3. **Export Technical Design Document** or a Milestone 1 design baseline at `docs/architecture/technical-design.md`.
4. **Resolve OQ-001 … OQ-005; revise and approve `plan.md`** without changing the approved requirements inadvertently.
5. **Generate `tasks.md`**, then implement using Codex CLI and capture the acceptance evidence.

This sequence avoids instructing Codex to reconcile against nonexistent local files.

## 7. Phase 1 — Foundation Inventory, Step 2: Document Reconciliation

> **Final review status:** **Completed — Reviewed with Open Gaps**  
> **Approval date:** 2026-11-11  
> **Approved by:** Project maintainer (explicit approval in chat)  
> **Scope:** Documentation inventory, classification, inconsistencies, canonical mapping, reconciliation matrix and remaining gaps  
> **Review-only outcome:** No technical plan approval, no implementation, no Constitution Review; every remaining gap stays **Open**.

### Decision record (recorded in GitHub through this register)

| Decision ID | Decision | State | Evidence / constraint |
|---|---|---|---|
| DR-001 | `docs/specs/` is the canonical directory for SPEC-001 and related SDD artifacts | Approved — 2026-11-11 | Explicit maintainer selection in chat; files already exist under `docs/specs/001-project-foundation/`. Other files with stale links are not automatically corrected. |
| DR-002 | Close Phase 1 / Step 2 **at review level**, with all Remaining Gaps preserved | Approved — 2026-11-11 | Explicit maintainer approval in chat; not equivalent to approving the technical plan, resolving design uncertainty or authorizing further phases. |

### Document Reconciliation Matrix

| ID | Document | GitHub evidence | Review classification | Outstanding action |
|---|---|---|---|---|
| DOC-01 | Product Requirements | `docs/product/requirements.md` (0 bytes) | Partial Approved / Unverified | Reconcile product decisions with original source |
| DOC-02 | Backend Design | `docs/architecture/backend-design.md` (0 bytes) | Unverified | Verify architecture/stack from full design source |
| DOC-03 | Frontend Design | `docs/architecture/frontend-design.md` (0 bytes) | Partial Approved / Unverified | Preserve approved React/browser mockup; verify detailed choices |
| DOC-04 | Technical Design | `docs/architecture/technical-design.md` (0 bytes) | Unverified | Verify original Milestone 1 boundary |
| DOC-05 | SPEC-001 | `docs/specs/001-project-foundation/spec.md` (content) | Approved (recorded) | Keep approved scope; audit checklist separately |
| DOC-06 | Technical Plan | `docs/specs/001-project-foundation/plan.md` (content) | Draft | No approval; no implementation |
| DOC-07 | Requirements checklist | Existing file with unchecked items | Scope approval recorded; audit pending | Retain audit items |
| DOC-08 | SDD Document Register | Existing file; this review synchronized | Active | Track open gaps and future evidence |
| DOC-09 | Root README | Existing file with stale location references | Active / outdated references | Resolve GAP-01/GAP-02 later |
| DOC-10 | `docs/README.md` | Existing starter README reporting old draft | Superseded candidate / outdated | Review as navigation page, avoid duplicate source of truth |
| DOC-11 | UI/UX references | No canonical file verified | Approved mockup in chat; file unverified | Verify references without inventing screenshots |
| DOC-12 | ADR | `docs/adr/README.md` (0 bytes) | Not started / conditional | Only write ADR when warranted |
| DOC-13 | Tasks | `docs/specs/001-project-foundation/tasks.md` (0 bytes) | Not started | Deferred until plan approval |

### Remaining Gaps — all remain OPEN

| Gap | Priority | Open issue | Completion evidence required later |
|---|---|---|---|
| GAP-01 | P0 | Incorrect links to legacy `specs/` path in existing documents | All links and references use approved `docs/specs/` mapping |
| GAP-02 | P0 | README/starter documentation and historical metadata are inconsistent | Cross-document status and version metadata synchronized without false approvals |
| GAP-03 | P0 | Backend Design has no substantive canonical content | Full design decisions reconciled with approved sources |
| GAP-04 | P0 | Frontend Design and approved mockup references not fully exported/verified | Detailed frontend and UI/UX source reconciliation |
| GAP-05 | P0 | TDD Milestone 1 scope (OQ-001) not verified against SPEC-001 | Explicit boundary agreement or documented discrepancy |
| GAP-06 | P1 | Backend stack choices (OQ-002) not verified | Source-backed .NET, database and migration decision |
| GAP-07 | P1 | Development OS, local infrastructure and CI choices (OQ-003–OQ-005) pending | Explicit approved choices/assumptions |
| GAP-08 | P1 | Product Requirements baseline is an empty placeholder | Product decisions exported and reviewed without inventing details |
| GAP-09 | P1 | SPEC-001 checklist audit is incomplete | Audit evidence for unchecked criteria |
| GAP-10 | P2 | UI/UX reference provenance and ADR location/use are unresolved | Verified references and conditional ADR policy |
| GAP-11 | Deferred | Tasks, implementation and acceptance verification are not started | Authorized later SDD gates; no work in this review |

**Reconciliation finding:** The confirmed issues concern documentation locations, review/status records, and missing primary design sources. A substantive conflict between SPEC-001 functional requirements and an earlier full Technical Design cannot be asserted without the original design source. The technology suggestions in draft `plan.md` remain proposals, not approved decisions.

**Source limitations:** GitHub file existence and content were checked directly. Prior chat decisions were available through Project conversation context and a Project SDD snapshot; complete earlier Backend/Frontend/Technical Design transcripts were not independently validated during this review. Consequently, source-dependent technical details remain Unverified.

**Remediation boundary:** This synchronization records the approval and current evidence; it does not close GAP-01 through GAP-11, revise architecture, edit technical plan, fill empty placeholders, create files, or advance the workflow.

## 8. Change history

| Date | Version | Change | Decision / source |
|---|---|---|---|
| 2026-11-11 | 1.0.0 | Initial register generated; inventoried SPEC-001, plan, checklist, README; synchronized administrative approval metadata and flagged chat-only Backend/Frontend/TDD and pending deliverables. | User request to introduce an SDD-generated-document checklist; SPEC-001 approval stated in chat. |
| 2026-11-11 | 1.1.0 | Synchronized DR-001/DR-002 and Step 2 Final Review; verified remote file inventory, canonical mapping, matrix and open gaps. | Explicit project maintainer approvals in chat; GitHub remote branch inspection. |

