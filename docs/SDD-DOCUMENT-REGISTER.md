# Family Memories — SDD Document Register & Generation Checklist

> **Document ID:** SDD-REG-001  
> **Version:** 1.3.1  
> **Last updated:** 2026-11-27  
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
| GOV-001 | Project SDD README | `README.md` | Exists (GitHub; content) | Active — references aligned | Document tree and Milestone 1 state synchronized with this register (2026-11-26, issue #1); GAP-01/GAP-02 closed. |
| GOV-003 | Docs navigation page | `docs/README.md` | Exists (GitHub; content) | Active — navigation only | Rewritten as a link index with no status of its own; points to this register (2026-11-26, issue #1). |
| GOV-002 | **SDD Document Register** | `docs/SDD-DOCUMENT-REGISTER.md` | Exists (GitHub; content) | Active — Step 2 reviewed | This register records DR-001/DR-002 and open gaps; it is not proof that underlying designs were reconciled in full. |
| SDD-001 | SPEC-001 requirements | `docs/specs/001-project-foundation/spec.md` | Exists (GitHub; content) | **Approved v1.1.0 (2026-11-27, PR #19 merge); v1.0.0 approved 2026-11-11** | Checklist audit remains pending. 2026-11-26 administrative fix (branch name, approval checkbox). 2026-11-27 v1.1.0: deployment target changed to Azure per ADR-001 (§2, FR-014, §8, AT-011); confirmed by merging PR #19 (2026-11-27). |
| SDD-002 | SPEC-001 review checklist | `docs/specs/001-project-foundation/checklists/requirements.md` | Exists (GitHub; content) | Scope approval recorded; audit open | Individual unchecked attestations are not approved by implication. Next-artifact path corrected to `docs/specs/` (2026-11-26). |
| SDD-003 | SPEC-001 technical plan | `docs/specs/001-project-foundation/plan.md` | Exists (GitHub; content) | **Draft — not approved** | Existing planning draft, not ratified. 2026-11-26: only the section 4 repository tree was corrected to place SDD documents under `docs/` (DR-001); no technology or scope change. |
| SDD-004 | SPEC-001 implementation tasks | `docs/specs/001-project-foundation/tasks.md` | **Placeholder (0 bytes)** | Not started | Empty file is not a task breakdown; do not populate before plan approval. |
| SDD-005 | Implementation verification report | `docs/specs/001-project-foundation/verification.md` | **Missing** | Not started | Deferred until implementation and acceptance evidence exist. |
| ADR-000 | ADR folder README / policy | `docs/adr/README.md` | **Placeholder (0 bytes)** | Not started | ADR policy still to be written (GAP-10, issue #8). Create ADRs only for decisions requiring durable rationale; no duplicate ADR location. |
| ADR-001 | ADR-001 Azure deployment target | `docs/adr/ADR-001-azure-deployment-target.md` | Exists (content) | **Accepted — maintainer, 2026-11-27** | Azure replaces home self-hosting; App Service + Static Web Apps + PostgreSQL Flexible Server + Key Vault; manual Portal provisioning. Rationale section awaits maintainer input. |
| SDD-101 | SPEC-002 Azure Deployment requirements | `docs/specs/002-azure-deployment/spec.md` | Exists (content) | **Draft v0.1.0 — not approved** | Depends on SPEC-001 implementation. Open questions OQ-201 … OQ-209; OQ-209 (health routes vs SWA `/api` prefix) must be decided before SPEC-001 implementation. |

### B. Product, frontend and backend design sources

| ID | Document | Intended repository path | File presence | Review state | Why it matters |
|---|---|---|---|---|---|
| DES-001 | Product Requirements / Product Scope baseline | `docs/product/requirements.md` | **Placeholder (0 bytes)** | Partial Approved / Unverified | Product decisions exist in chat/SPEC-001, but no content in canonical file; full product baseline not verified. |
| DES-002 | **Backend Design** | `docs/architecture/backend-design.md` | **Placeholder (0 bytes)** | Unverified | Backend stack/architecture details require original discussion or supporting design source. Export must be reconciled with ADR-001 (original source assumed home hosting). |
| DES-003 | **Frontend Design** | `docs/architecture/frontend-design.md` | **Placeholder (0 bytes)** | Partial Approved / Unverified | React and responsive browser mockup decisions recorded in chat; detailed technology and UX design need source reconciliation. |
| DES-004 | **Technical Design Document (TDD)** | `docs/architecture/technical-design.md` | **Placeholder (0 bytes)** | Unverified | Original Milestone 1 scope and cross-cutting decisions not yet verified. Deployment sections superseded by ADR-001. |
| DES-005 | UI/UX mockup specification or references | `docs/design/ui-ux-reference.md` | **Missing (chat only)** | Mockup approved in chat; file unverified | No confirmed canonical screenshot or reference file on this branch; do not invent one. |

**Confirmed from prior project discussions, not from files:** React frontend, medium scale, family-scoped privacy, manual image upload, support for original and optimized image renditions. Exact backend version, DB engine, CSS/UI library, local OS, and CI provider remain **planning decisions pending reconciliation**, not settled by this register. The earlier "home self-hosting" decision is **superseded by ADR-001 (Azure, 2026-11-27)**.

### Snapshot / status counts (remote GitHub branch, 2026-11-11)

- **15 tracked files** on `feature/001-project-foundation` after the ADR-001 change: **9 nonempty** (README, docs/README, Document Register, SPEC-001, plan, checklist, ADR-001, SPEC-002, .gitignore) and **6 zero-byte placeholders** (Product, Backend, Frontend, Technical Design, ADR README, tasks).
- **1 accepted ADR** (ADR-001 Azure deployment target) and **1 draft specification** (SPEC-002, not approved).
- **1 approved requirements specification** (SPEC-001 v1.0.0; approval recorded, checklist audit pending).
- **1 draft technical plan** (`plan.md`, not approved).
- **4 empty canonical product/architecture source files**; the approved UI/UX mockup is not verified as a canonical repository reference.
- **1 empty tasks placeholder** and **1 missing verification report**; ADRs are conditional and no substantive ADR exists.
- **Phase 1 — Foundation Inventory / Step 2: Document Reconciliation**: **Completed — Reviewed with Open Gaps**, approved by project maintainer on 2026-11-11. No gaps closed by this review.
- **2026-11-26:** GAP-01 and GAP-02 closed by issue #1 (documentation paths and status metadata only). GAP-03 … GAP-11 remain open.

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
- [ ] Decide the health route mapping between SPEC-001 `/health/*` and the Static Web Apps `/api/*` proxy (SPEC-002 OQ-209, GAP-12).
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
| DR-003 | Microsoft Azure replaces home self-hosting as the production target; deployment specified in SPEC-002 | Accepted — 2026-11-27 | Explicit maintainer decision in session; recorded as [ADR-001](adr/ADR-001-azure-deployment-target.md). |

### Document Reconciliation Matrix

| ID | Document | GitHub evidence | Review classification | Outstanding action |
|---|---|---|---|---|
| DOC-01 | Product Requirements | `docs/product/requirements.md` (0 bytes) | Partial Approved / Unverified | Reconcile product decisions with original source |
| DOC-02 | Backend Design | `docs/architecture/backend-design.md` (0 bytes) | Unverified | Verify architecture/stack from full design source |
| DOC-03 | Frontend Design | `docs/architecture/frontend-design.md` (0 bytes) | Partial Approved / Unverified | Preserve approved React/browser mockup; verify detailed choices |
| DOC-04 | Technical Design | `docs/architecture/technical-design.md` (0 bytes) | Unverified | Verify original Milestone 1 boundary |
| DOC-05 | SPEC-001 | `docs/specs/001-project-foundation/spec.md` (content) | Approved v1.1.0 (hosting amendment confirmed 2026-11-27, PR #19) | Keep approved scope; audit checklist separately |
| DOC-06 | Technical Plan | `docs/specs/001-project-foundation/plan.md` (content) | Draft | No approval; no implementation |
| DOC-07 | Requirements checklist | Existing file with unchecked items | Scope approval recorded; audit pending | Retain audit items |
| DOC-08 | SDD Document Register | Existing file; this review synchronized | Active | Track open gaps and future evidence |
| DOC-09 | Root README | Existing file; references aligned 2026-11-26 | Active — references aligned | None (GAP-01/GAP-02 closed by issue #1) |
| DOC-10 | `docs/README.md` | Rewritten 2026-11-26 as a link index | Navigation page (no status) | None; status lives only in this register |
| DOC-11 | UI/UX references | No canonical file verified | Approved mockup in chat; file unverified | Verify references without inventing screenshots |
| DOC-12 | ADR | `docs/adr/README.md` (0 bytes) | Not started / conditional | Only write ADR when warranted |
| DOC-13 | Tasks | `docs/specs/001-project-foundation/tasks.md` (0 bytes) | Not started | Deferred until plan approval |
| DOC-14 | ADR-001 Azure deployment target | `docs/adr/ADR-001-azure-deployment-target.md` (content) | Accepted 2026-11-27 | Maintainer to fill in rationale |
| DOC-15 | SPEC-002 Azure Deployment | `docs/specs/002-azure-deployment/spec.md` (content) | Draft v0.1.0 | Resolve OQ-201 … OQ-209; approve before any Azure spend |

### Remaining Gaps — GAP-01 and GAP-02 closed; all others OPEN

Each gap is tracked as a GitHub issue; see tracking issue
[#17](https://github.com/developzoneio/family-memories/issues/17) for the gap-to-issue mapping.

| Gap | Priority | Open issue | Completion evidence required later |
|---|---|---|---|
| GAP-01 | P0 | **Closed — 2026-11-26.** Incorrect links to legacy `specs/` path in existing documents | Root README, `docs/README.md`, checklist and plan section 4 now use the `docs/specs/` mapping ([#1](https://github.com/developzoneio/family-memories/issues/1)) |
| GAP-02 | P0 | **Closed — 2026-11-26.** README/starter documentation and historical metadata are inconsistent | Root README status synced with this register; `docs/README.md` holds no status; SPEC-001 branch name and approval checkbox corrected without a version change ([#1](https://github.com/developzoneio/family-memories/issues/1)) |
| GAP-03 | P0 | Backend Design has no substantive canonical content | Full design decisions reconciled with approved sources |
| GAP-04 | P0 | Frontend Design and approved mockup references not fully exported/verified | Detailed frontend and UI/UX source reconciliation |
| GAP-05 | P0 | TDD Milestone 1 scope (OQ-001) not verified against SPEC-001 | Explicit boundary agreement or documented discrepancy |
| GAP-06 | P1 | Backend stack choices (OQ-002) not verified | Source-backed .NET, database and migration decision |
| GAP-07 | P1 | Development OS, local infrastructure and CI choices (OQ-003–OQ-005) pending | Explicit approved choices/assumptions |
| GAP-08 | P1 | Product Requirements baseline is an empty placeholder | Product decisions exported and reviewed without inventing details |
| GAP-09 | P1 | SPEC-001 checklist audit is incomplete | Audit evidence for unchecked criteria |
| GAP-10 | P2 | UI/UX reference provenance and ADR location/use are unresolved | Verified references and conditional ADR policy |
| GAP-11 | Deferred | Tasks, implementation and acceptance verification are not started | Authorized later SDD gates; no work in this review |
| GAP-12 | P0 | Health route conflict (SPEC-002 OQ-209): SPEC-001 fixes `/health/live` and `/health/ready`, but Static Web Apps forwards only `/api/*` to a linked App Service | Maintainer decision recorded; SPEC-001 amended if the contract changes; resolved before SPEC-001 health endpoints are implemented |
| GAP-13 | P1 | SPEC-002 is a draft: Azure region, SKUs/budget, domain, code-deployment method, DB network access, migrations in Azure and monitoring are open (OQ-201 … OQ-208); Portal runbook not written; ADR-001 rationale not recorded | SPEC-002 approved, plan and runbook written, ADR-001 rationale filled in |

**Reconciliation finding:** The confirmed issues concern documentation locations, review/status records, and missing primary design sources. A substantive conflict between SPEC-001 functional requirements and an earlier full Technical Design cannot be asserted without the original design source. The technology suggestions in draft `plan.md` remain proposals, not approved decisions.

**Source limitations:** GitHub file existence and content were checked directly. Prior chat decisions were available through Project conversation context and a Project SDD snapshot; complete earlier Backend/Frontend/Technical Design transcripts were not independently validated during this review. Consequently, source-dependent technical details remain Unverified.

**Remediation boundary:** This synchronization records the approval and current evidence; it does not close GAP-01 through GAP-11, revise architecture, edit technical plan, fill empty placeholders, create files, or advance the workflow. (Later update: GAP-01/GAP-02 were closed on 2026-11-26 by issue #1; see Section 8.)

## 8. Change history

| Date | Version | Change | Decision / source |
|---|---|---|---|
| 2026-11-11 | 1.0.0 | Initial register generated; inventoried SPEC-001, plan, checklist, README; synchronized administrative approval metadata and flagged chat-only Backend/Frontend/TDD and pending deliverables. | User request to introduce an SDD-generated-document checklist; SPEC-001 approval stated in chat. |
| 2026-11-11 | 1.1.0 | Synchronized DR-001/DR-002 and Step 2 Final Review; verified remote file inventory, canonical mapping, matrix and open gaps. | Explicit project maintainer approvals in chat; GitHub remote branch inspection. |
| 2026-11-26 | 1.2.0 | Closed GAP-01/GAP-02: fixed legacy `specs/` paths (root README, `docs/README.md`, checklist, plan section 4 tree); rewrote `docs/README.md` as a navigation page (GOV-003); synced root README status; administrative SPEC-001 fixes (branch name, approval checkbox) with version kept at 1.0.0; linked tracking issue #17. | GitHub issue #1; maintainer decisions in session (navigation page, no spec version bump, fix plan tree in #1). |
| 2026-11-27 | 1.3.0 | Added ADR-001 (Azure replaces home self-hosting; accepted) and SPEC-002 Azure Deployment (draft v0.1.0). Amended SPEC-001 to v1.1.0 (§2, FR-014, §8, AT-011; pending confirmation through PR merge); updated draft plan (hosting context row, AT-011, R-005); added DR-003, GAP-12, GAP-13 and a Gate B item; superseded "home self-hosting" in confirmed context. | Maintainer decisions in session 2026-11-27: Azure replaces home; new SPEC-002; App Service + Static Web Apps + PostgreSQL Flexible Server + Key Vault; manual Portal provisioning. |
| 2026-11-27 | 1.3.1 | Recorded SPEC-001 v1.1.0 as approved: the maintainer merged PR #19, which is the confirmation step stated in 1.3.0. Updated the SPEC-001 header, SDD-001, DOC-05 and the root README; the scope-approval DoD box now applies to v1.1.0. No requirement change. Restored chronological order of history rows. | PR #19 merged 2026-11-27 by the maintainer; maintainer decision in session 2026-11-27. |

