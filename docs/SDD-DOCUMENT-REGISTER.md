# Family Memories — SDD Document Register & Generation Checklist

> **Document ID:** SDD-REG-001  
> **Version:** 1.0.0  
> **Last updated:** 2026-11-11  
> **Owner:** Project maintainer  
> **Status:** Active — living document  
> **Canonical repository path:** `docs/SDD-DOCUMENT-REGISTER.md`

## 1. Purpose and rules

This document is the **single inventory and generation checklist** for Family Memories' Spec-Driven Development (SDD) artifacts. It answers:

1. Which documents **exist as actual files**?
2. Which documents are **approved, draft, outdated, or missing**?
3. Which documents must be created or reviewed **before the next SDD phase**?
4. How must ChatGPT and Codex CLI update the inventory whenever they generate, rename, approve, or supersede a document?

**Critical distinction:** a design discussed in ChatGPT is **not** a repository document. Codex CLI cannot be expected to read decisions that exist only in previous chat sessions. A document is marked `Exists` below only if a file was verified among the generated artifacts available in this session. **Presence in the user's local Git repository has not been verified.** Paths are the intended **canonical paths inside the repository**, not proof that those files have been committed.

### Document lifecycle

- **File presence:** `Exists (generated)` / `Missing` / `Conditional` / `Chat only`.
- **Review state:** `Approved` / `Draft` / `Pending review` / `Not started` / `N/A` / `Superseded`.
- **Repository state:** `Unverified` until a local checkout or GitHub repository is inspected.
- Approval is a **human decision**; generating a document does not approve it.
- A required file must not be marked `Exists` solely because its name is listed in a plan.
- Keep document **status**, **version**, and **last-updated date** in sync with this register. Record discrepancies transparently until resolved.

## 2. Current artifact inventory (as of 2026-11-11)

### A. SDD governance and Milestone 1

| ID | Document | Intended repository path | File presence | Review state | Notes / next action |
|---|---|---|---|---|---|
| GOV-001 | Project SDD README | `README.md` | Exists (generated) | Updated | Lists current artifacts and directs readers to this register. |
| GOV-002 | **SDD Document Register** | `docs/SDD-DOCUMENT-REGISTER.md` | **Exists (generated)** | Active | This file. Update as part of every documentation change. |
| SDD-001 | SPEC-001 requirements | `specs/001-project-foundation/spec.md` | Exists (generated) | **Approved, 2026-11-11** | Maintainer approved in chat; header synced to approved baseline without changing requirements. |
| SDD-002 | SPEC-001 review checklist | `specs/001-project-foundation/checklists/requirements.md` | Exists (generated) | Approval recorded; audit open | Maintainer approval recorded; unverified line-item checks intentionally remain unchecked. |
| SDD-003 | SPEC-001 technical plan | `specs/001-project-foundation/plan.md` | Exists (generated) | **Draft — not approved** | Plan created in this chat; reconcile against exported designs, then obtain approval. This plan was **not included in the original starter ZIP**; included in the refreshed package accompanying this register. |
| SDD-004 | SPEC-001 implementation tasks | `specs/001-project-foundation/tasks.md` | **Missing** | Not started | Generate **after** plan approval; reference requirement/acceptance-test IDs. |
| SDD-005 | Implementation verification report | `specs/001-project-foundation/verification.md` | **Missing** | Not started | Generate after code and tests are executed; include AT-001 to AT-011 evidence, failures and exceptions. |
| ADR-001 | Architecture Decision Records | `docs/architecture/adr/` | Conditional | Not started | Create ADR files **only for actual architectural decisions requiring a durable rationale**, e.g., changes from an earlier approved design. Do not generate empty placeholders. |

### B. Product, frontend and backend design sources

| ID | Document | Intended repository path | File presence | Review state | Why it matters |
|---|---|---|---|---|---|
| DES-001 | Product Requirements / Product Scope baseline | `docs/product/product-requirements.md` | **Chat only** | Needs export/review | Product decisions discussed previously; no canonical PRD file verified. Optional for approving this foundation plan if the relevant scope is already captured in SPEC-001, but important for future feature specs. |
| DES-002 | **Backend Design** | `docs/architecture/backend-design.md` | **Chat only** | Needs export/review | Previous backend design sessions exist in chat context, but **no actual design file is present**. Export approved architecture and stack before ratifying `plan.md`. |
| DES-003 | **Frontend Design** | `docs/architecture/frontend-design.md` | **Chat only** | Needs export/review | React and mobile-browser UX decisions were discussed and mockup accepted, but **no actual design file is present**. Export technologies, layout and UI conventions. |
| DES-004 | **Technical Design Document (TDD)** | `docs/architecture/technical-design.md` | **Chat only** | Needs export/review | Milestone 1 boundaries and cross-cutting architecture must be reconciled with SPEC-001. |
| DES-005 | UI/UX mockup specification or references | `docs/design/ui-ux-reference.md` | **Chat only** | Needs export/review | The approved desktop/mobile browser mockups were discussed in chat. Create file-based acceptance references when implementing shell styling; do not claim screenshots exist in Git. |

**Confirmed from prior project discussions, not from files:** React frontend, home self-hosting, medium scale, family-scoped privacy, manual image upload, support for original and optimized image renditions. Exact backend version, DB engine, CSS/UI library, local OS, and CI provider remain **planning decisions pending reconciliation**, not settled by this register.

### Snapshot / status counts

- **5 verified generated documents** in the repository-ready package assembled for this session: `README.md`, `spec.md`, `checklists/requirements.md`, `plan.md`, and this register. Their **presence in local Git remains unverified**.
- **1 approved requirements specification** (`SPEC-001`, approved in chat; generated file metadata reconciled).
- **1 draft technical plan** (`plan.md`, no approval yet).
- **5 chat-only design/product references** need files or an explicit documented decision not to export.
- **2 milestone deliverables missing** (`tasks.md`, `verification.md`); ADRs conditional.

## 3. Milestone 1 readiness checklist

### Gate A — Requirements (Specify / Approve)

- [x] Generate SPEC-001 functional and nonfunctional requirements with acceptance tests.
- [x] Maintainer approves SPEC-001 in chat (2026-11-11).
- [x] Update the generated `spec.md` approval metadata and review checklist without changing substantive scope. (Git commit still unverified.)
- [ ] Confirm these files and this register are committed in the repository.

### Gate B — Architecture (Plan)

- [ ] Generate `docs/architecture/backend-design.md` from the prior approved Backend Design decisions; label any inferred choices as proposals.
- [ ] Generate `docs/architecture/frontend-design.md` from prior Frontend Design decisions and approved mockup context.
- [ ] Generate `docs/architecture/technical-design.md` or explicitly document where the Milestone 1 TDD decisions are captured.
- [ ] Reconcile scope conflict (SPEC-001 foundation versus any broader Milestone 1 in the TDD).
- [ ] Resolve or explicitly approve assumptions for SPEC-001 open questions **OQ-001 … OQ-005**: scope, backend stack, primary development OS, local infrastructure, CI.
- [ ] Review and finalize `specs/001-project-foundation/plan.md` against the above design files.
- [ ] Maintainer approves `plan.md` and records date/version.

### Gate C — Task planning (Tasks)

- [ ] Generate `specs/001-project-foundation/tasks.md` from the **approved** plan.
- [ ] Ensure each executable task traces to an FR/NFR and/or AT ID.
- [ ] Verify dependencies and task order; do not add features excluded from SPEC-001.

### Gate D — Implementation and acceptance

- [ ] Implement the foundation using the approved plan and tasks.
- [ ] Run/document acceptance scenarios **AT-001 … AT-011**.
- [ ] Generate `verification.md` with pass/fail evidence and remaining gaps.
- [ ] Review/merge changes after checks pass and update this register.

**Current gate:** **B — Architecture (Plan)**. Do **not** direct Codex to read non-existent Backend/Frontend/TDD files, and do **not** treat draft `plan.md` as permission to implement.

## 4. Dependencies between documents

```text
Prior design decisions in chat
        │
        ├── [Missing] Backend Design file ───┐
        ├── [Missing] Frontend Design file ──┼──> Reconcile [Draft] plan.md
        └── [Missing] TDD file ──────────────┘              │
                                                            v
[Approved in chat] SPEC-001 spec.md ───────────────> [Approved] plan.md
                                                            │
                                                            v
                                                       tasks.md (missing)
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
4. **Update metadata** at the top of this register: version and last-updated date. Add a concise entry to Section 7.
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

## 7. Change history

| Date | Version | Change | Decision / source |
|---|---|---|---|
| 2026-11-11 | 1.0.0 | Initial register generated; inventoried SPEC-001, plan, checklist, README; synchronized administrative approval metadata and flagged chat-only Backend/Frontend/TDD and pending deliverables. | User request to introduce an SDD-generated-document checklist; SPEC-001 approval stated in chat. |

