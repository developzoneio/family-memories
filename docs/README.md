# Family Memories — Documentation

This folder holds the Spec-Driven Development (SDD) documents for Family Memories.

> The **[SDD Document Register](SDD-DOCUMENT-REGISTER.md)** is the single source of truth for each document's status,
> version and approval. This page is navigation only and records no status of its own.

## Documents

| Area | Document | Purpose |
|---|---|---|
| Governance | [SDD-DOCUMENT-REGISTER.md](SDD-DOCUMENT-REGISTER.md) | Inventory, status, gates and open gaps for all SDD documents |
| Product | [product/requirements.md](product/requirements.md) | Product requirements and scope baseline |
| Architecture | [architecture/technical-design.md](architecture/technical-design.md) | Technical Design Document and Milestone 1 boundary |
| Architecture | [architecture/backend-design.md](architecture/backend-design.md) | Backend architecture and stack |
| Architecture | [architecture/frontend-design.md](architecture/frontend-design.md) | Frontend architecture and UI/UX constraints |
| Decisions | [adr/README.md](adr/README.md) | Architecture Decision Records |
| SPEC-001 | [specs/001-project-foundation/spec.md](specs/001-project-foundation/spec.md) | Project Foundation behavioral requirements |
| SPEC-001 | [specs/001-project-foundation/plan.md](specs/001-project-foundation/plan.md) | Technical implementation plan |
| SPEC-001 | [specs/001-project-foundation/tasks.md](specs/001-project-foundation/tasks.md) | Implementation task breakdown |
| SPEC-001 | [specs/001-project-foundation/checklists/requirements.md](specs/001-project-foundation/checklists/requirements.md) | Specification review checklist |

## Conventions

- Each product capability gets its own numbered folder under `docs/specs/` (DR-001).
- The SDD workflow (Specify → Approve → Plan → Tasks → Implement/verify) is described in the
  [root README](../README.md#sdd-workflow).
- Whenever a document is created, renamed, approved or superseded, update the register in the same change.
