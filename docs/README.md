# Family Memories — Spec-Driven Development

This package begins the SDD documentation repository. It contains the first *draft* specification, not implementation code.

## Structure

```text
specs/
└── 001-project-foundation/
    ├── spec.md
    └── checklists/
        └── requirements.md
```

## Process

1. **Specify** — Write measurable requirements and acceptance scenarios in `spec.md`.
2. **Clarify / approve** — Resolve open questions and approve the specification.
3. **Plan** — Create `plan.md` with architecture, technologies, dependencies and ADRs.
4. **Tasks** — Create `tasks.md` with small dependency-ordered tasks and associated tests.
5. **Implement** — Create code and tests; verify against the spec; review and merge.

Each distinct product capability receives its own numbered spec rather than growing an unrelated spec.

## Status

`001-project-foundation` — Draft v0.1.0, pending scope confirmation and review.
