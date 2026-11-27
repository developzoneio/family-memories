# Family Memories — Documentation

This folder holds the Spec-Driven Development (SDD) documents for Family Memories.

> The **[SDD Document Register](SDD-DOCUMENT-REGISTER.md)** is the single source of truth for each document's status,
> version and approval. This page is navigation only and records no status of its own.

## Documents

| Area | Document | Purpose |
|---|---|---|
| Governance | [SDD-DOCUMENT-REGISTER.md](SDD-DOCUMENT-REGISTER.md) | Inventory, status, gates and open gaps for all SDD documents |
| Product | [product/requirements.md](product/requirements.md) | Product requirements and scope baseline |
| Product | [product/sources/family-memories-product-evidence.md](product/sources/family-memories-product-evidence.md) | Evidence export behind the product baseline (source record) |
| Architecture | [architecture/technical-design.md](architecture/technical-design.md) | Technical Design Document and Milestone 1 boundary |
| Architecture | [architecture/backend-design.md](architecture/backend-design.md) | Backend architecture and stack |
| Architecture | [architecture/frontend-design.md](architecture/frontend-design.md) | Frontend architecture and UI/UX constraints |
| Decisions | [adr/README.md](adr/README.md) | Architecture Decision Records |
| Decisions | [adr/ADR-001-azure-deployment-target.md](adr/ADR-001-azure-deployment-target.md) | Production deployment target: Azure |
| SPEC-001 | [specs/001-project-foundation/spec.md](specs/001-project-foundation/spec.md) | Project Foundation behavioral requirements |
| SPEC-001 | [specs/001-project-foundation/plan.md](specs/001-project-foundation/plan.md) | Technical implementation plan |
| SPEC-001 | [specs/001-project-foundation/tasks.md](specs/001-project-foundation/tasks.md) | Implementation task breakdown |
| SPEC-001 | [specs/001-project-foundation/checklists/requirements.md](specs/001-project-foundation/checklists/requirements.md) | Specification review checklist |
| SPEC-002 | [specs/002-azure-deployment/spec.md](specs/002-azure-deployment/spec.md) | Azure deployment requirements |

## Conventions

- Each product capability gets its own numbered folder under `docs/specs/` (DR-001).
- The SDD workflow (Specify → Approve → Plan → Tasks → Implement/verify) is described in the
  [root README](../README.md#sdd-workflow).
- Whenever a document is created, renamed, approved or superseded, update the register in the same change.
