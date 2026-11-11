# Family Memories — Spec-Driven Development

This repository uses SDD. Review the **[SDD Document Register](docs/SDD-DOCUMENT-REGISTER.md)** before generating or editing project documentation. The register tracks real files, draft/approved status, missing design sources and next actions.

## Current documents

```text
docs/
└── SDD-DOCUMENT-REGISTER.md        # living documentation inventory
specs/
└── 001-project-foundation/
    ├── spec.md                     # approved 2026-11-11
    ├── plan.md                     # draft; not approved
    └── checklists/
        └── requirements.md         # approval recorded; audit items may remain open
```

## SDD workflow

1. **Specify** — Write observable requirements in `spec.md`.
2. **Approve** — Maintainer reviews scope and records approval.
3. **Plan** — Generate and approve `plan.md`, reconciling actual backend/frontend/TDD design documents.
4. **Tasks** — Generate `tasks.md` from an approved plan with FR/AT traceability.
5. **Implement / verify** — Build, test, document acceptance evidence and update the register.

Whenever a document is generated, renamed, approved, or superseded, **update `docs/SDD-DOCUMENT-REGISTER.md` in the same change**. This does not happen automatically without a tool/agent following the policy.

## Current Milestone 1 state (2026-11-11)

- SPEC-001: **Approved** by maintainer in chat.
- `plan.md`: **Draft**; .NET/database/toolchain proposals require reconciliation.
- Backend Design, Frontend Design and Technical Design Document: **not yet exported to canonical local Markdown files**.
- `tasks.md`: **Not started**. Do not implement code from the draft plan.
