# Family Memories — Spec-Driven Development

This repository uses SDD. Review the **[SDD Document Register](docs/SDD-DOCUMENT-REGISTER.md)** before generating or editing project documentation. The register tracks real files, draft/approved status, missing design sources and next actions.

## Current documents

```text
docs/
├── README.md                       # navigation page for docs/
├── SDD-DOCUMENT-REGISTER.md        # living documentation inventory (status source of truth)
├── specs/
│   └── 001-project-foundation/
│       ├── spec.md                 # SPEC-001 v1.0.0, approved 2026-11-11
│       ├── plan.md                 # draft v0.1; not approved
│       ├── tasks.md                # empty placeholder; deferred until plan approval
│       └── checklists/
│           └── requirements.md     # approval recorded; audit items remain open
├── architecture/
│   ├── backend-design.md           # empty placeholder
│   ├── frontend-design.md          # empty placeholder
│   └── technical-design.md         # empty placeholder
├── product/
│   └── requirements.md             # empty placeholder
└── adr/
    └── README.md                   # empty placeholder
```

See the register for the authoritative status of each file.

## SDD workflow

1. **Specify** — Write observable requirements in `spec.md`.
2. **Approve** — Maintainer reviews scope and records approval.
3. **Plan** — Generate and approve `plan.md`, reconciling actual backend/frontend/TDD design documents.
4. **Tasks** — Generate `tasks.md` from an approved plan with FR/AT traceability.
5. **Implement / verify** — Build, test, document acceptance evidence and update the register.

Whenever a document is generated, renamed, approved, or superseded, **update `docs/SDD-DOCUMENT-REGISTER.md` in the same change**. This does not happen automatically without a tool/agent following the policy.

## Current Milestone 1 state (2026-11-26)

- SPEC-001 v1.0.0: **Approved** by maintainer in chat (2026-11-11).
- `plan.md`: **Draft v0.1**; .NET/database/toolchain proposals require reconciliation.
- Product Requirements, Backend Design, Frontend Design and Technical Design Document: **placeholder files exist
  but are empty (0 bytes)**; content has not been exported yet.
- `tasks.md`: **Not started** (empty placeholder). Do not implement code from the draft plan.
- Work is tracked in the GitHub milestone *Milestone 1 - Project Foundation (SPEC-001)*; see tracking issue
  [#17](https://github.com/developzoneio/family-memories/issues/17).
