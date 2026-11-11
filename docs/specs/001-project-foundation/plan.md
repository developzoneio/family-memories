# SPEC-001 — Technical Implementation Plan

> **Project:** Family Memories  
> **Milestone:** 1 — Project Foundation & Local Development  
> **Source of truth:** [`spec.md`](./spec.md) — SPEC-001, approved by project maintainer on 2026-11-11  
> **Status:** Planning draft v0.1 — technical stack/assumptions require alignment with prior Backend and Frontend Designs  
> **Last updated:** 2026-11-11  
> **Planning rule:** Do not implement product features excluded by SPEC-001. Changes to observable requirements must be made in `spec.md` first.

## 1. Goal and boundaries

Deliver a reproducible, privacy-preserving developer foundation that supports a family-private web application in later specs. A clean checkout on one documented development OS must launch a responsive React shell, ASP.NET Core API, and local database, support repeatable database migrations, expose distinct liveness and readiness endpoints, and pass local and pull-request CI checks.

In scope: project layout, developer bootstrap, configuration, health checks, empty/baseline database migration, web shell, tests, CI, and README. Out of scope: auth, family membership, photo upload or storage, timeline, albums, notifications, production deployment, and real family data. In particular, **do not build unauthenticated write APIs**.

## 2. Technology decisions — proposed, not yet ratified

These are engineering proposals, not decisions established by SPEC-001. Check them against the previous technical design; if that design differs, preserve the prior decision or document an explicit Architecture Decision Record (ADR).

| Area | Proposed choice | Rationale / restriction |
|---|---|---|
| Repository | GitHub monorepo | One PR validates backend, frontend and infra together. |
| Backend | ASP.NET Core on .NET 10 LTS | Supported LTS baseline as of Nov 2026; use existing approved .NET version if different. |
| Backend style | Modular-monolith-ready, minimal initial API | Avoid premature domain modules and abstractions in foundation scope. |
| Database | PostgreSQL 17, if not already selected | Relational store with local container support; honor earlier Backend Design. |
| Data layer | EF Core migrations with Npgsql, if PostgreSQL | Enables explicit, repeatable baseline migration. Match provider major versions to runtime. |
| Frontend | React + TypeScript + Vite | Responsive browser-first app, fast local developer feedback. Match existing Frontend Design. |
| Styling | Existing approved UI/style system | Do not substitute a new design library or mockup; implement only minimal approved shell. |
| Local infrastructure | Docker Compose for database; frontend/API run with toolchain | DB reproducibility and source-level debugging; no public router configuration. |
| Development OS | Windows 11 + WSL2 or Linux (select one primary target) | Acceptance requires one tested, documented environment. |
| CI | GitHub Actions | Pull-request checks without personal credentials. |
| Backend tests | xUnit and ASP.NET Core integration-test tooling | Tests for status semantics, readiness failure, and no sensitive output. |
| Frontend tests | Vitest / React Testing Library; Playwright browser smoke tests | Validate placeholder behavior, outage resilience and 360/1280 layouts. |

**Version policy:** lock SDK/toolchain versions in tracked manifests (`global.json`, frontend lockfile, image major/digest as appropriate); use current security patches. Do not infer precise packages from this draft until version compatibility is checked.

## 3. Architecture

```text
Desktop/mobile browser
        |
        v
React + Vite (local browser shell)
        | optional, read-only health request
        v
ASP.NET Core API (localhost)
        |  /health/live : process liveness only
        |  /health/ready: DB dependency check
        v
EF Core DbContext / database health checker
        |
        v
PostgreSQL container (named persistent volume)
```

For local development, bind DB and API to loopback when feasible. The Vite proxy should forward a same-origin path to the API, so frontend status checks do not require a wide-open CORS policy. No reverse proxy, TLS, router forwarding, or production networking is in SPEC-001.

### Backend responsibilities

- API process hosts `GET /health/live` and `GET /health/ready` only (plus non-sensitive development diagnostics if necessary).
- Liveness does **not** depend on the database; return 200 with a minimal JSON status while HTTP server runs.
- Readiness checks database connectivity, returns 200 when ready, 503 on failure. Do not expose raw database errors, hostnames, server/version metadata, or connection strings in the response.
- Logs may include correlation ID and bounded exception classification; redact sensitive values.
- Database schema changes occur through an explicit migration command, **not** destructive startup initialization.

### Frontend responsibilities

- Render the approved Family Memories visual language at 360 and 1280 CSS px; include navigation/placeholders for Timeline, Albums, and Family, visibly labeled *Coming soon* or disabled.
- Optionally display API status using a read-only request; network failure must not prevent shell rendering.
- Do not simulate successful uploads, invitations, registration, or mutations. No family photographs or real personal information in fixtures.

## 4. Proposed repository structure

```text
family-memories/
├── README.md
├── AGENTS.md                          # optional Codex guidance
├── .gitignore
├── .editorconfig
├── global.json                        # pin .NET SDK, if using .NET
├── FamilyMemories.sln
├── src/
│   ├── backend/
│   │   ├── FamilyMemories.Api/
│   │   └── FamilyMemories.Infrastructure/  # DbContext/migrations if needed
│   └── frontend/                       # React + TypeScript
├── tests/
│   ├── backend/FamilyMemories.Api.Tests/
│   └── frontend/                      # may live under frontend per toolchain
├── infra/
│   └── compose.dev.yml                # database only; durable volume
├── scripts/
│   ├── verify.sh
│   └── verify.ps1                      # when Windows native is supported
├── .github/workflows/ci.yml
└── specs/
    └── 001-project-foundation/
        ├── spec.md                     # approved behavioral requirements
        ├── plan.md                     # this document
        └── checklists/requirements.md
```

The structure is illustrative until compared with the existing technical designs. Keep the number of projects minimal for this increment; do not add domain services, message queues, Redis, media services or object storage merely in anticipation of future specs.

## 5. Observable endpoints and failure modes

| Method / route | Normal response | Dependency unavailable | Behavior |
|---|---|---|---|
| `GET /health/live` | HTTP 200, `{ "status": "healthy" }` | Still HTTP 200 if API itself serves HTTP | Checks process only |
| `GET /health/ready` | HTTP 200, `{ "status": "healthy" }` | HTTP 503, `{ "status": "unhealthy" }` | Requires successful database check |

Responses must be small, machine-readable, and constant-shape. All payloads must exclude credentials, hostnames, connection strings, stack traces, database names, and internal topology. Avoid exposing detailed exception messages through frontend status widgets.

## 6. Database and configuration lifecycle

1. Provide `infra/compose.dev.yml` with a PostgreSQL instance, health check and named persistent data volume. Use non-production sample credentials only in local examples. Never commit actual personal secrets.
2. Commit a sample env file and a local env loading convention (`.env.example` / environment variables / .NET user secrets), but ignore `.env` and personal configs. Never commit family data.
3. Start DB via the documented Compose command and wait for readiness.
4. Apply baseline EF Core migration explicitly, e.g. a documented `dotnet ef database update` command with the correct startup and migrations projects; the first run creates schema history, later runs are no-ops.
5. Restart API and DB **without deleting the volume**; migration history persists. Distinguish normal shutdown from an explicitly destructive data reset.
6. Missing required values produce non-sensitive, actionable diagnostics and non-zero failure, not a silent invalid configuration.

The initial migration should be **minimal**: no future family, identity, photo, album or membership tables until the relevant specification is approved.

## 7. Local developer workflow (target state)

The README will list exact prerequisites and versions for the selected development OS, then provide tested commands equivalent to:

```bash
# from repository root
docker compose -f infra/compose.dev.yml up -d
# apply baseline DB migration using documented dotnet ef command
dotnet run --project src/backend/FamilyMemories.Api
# in a second terminal
cd src/frontend && npm ci && npm run dev
```

Ports/URLs are provisional until implementation; suggested loopback defaults: UI `http://localhost:5173`, API `http://localhost:5080`, database `127.0.0.1:5432`. Validate that ports do not conflict with prior design. Document how to inspect service health, stop containers **without `-v`**, diagnose missing Docker/SDK/Node, and run `scripts/verify.sh` (or equivalent supported-platform command).

## 8. Test design and requirement traceability

| Acceptance test | Planned evidence / automation | Key requirement IDs |
|---|---|---|
| AT-001 | Clean-clone quick-start walkthrough on supported OS; check UI/API URLs | FR-001, FR-002, NFR-005 |
| AT-002 | API integration tests: live=200, ready=200 with DB available | FR-003, FR-004 |
| AT-003 | Stop DB only; assert ready=503 while live=200; restore DB afterward | FR-003, FR-004, NFR-006 |
| AT-004 | Assert health/error payloads and logs do not contain secrets or infra details | FR-005, FR-011, NFR-004 |
| AT-005 | Apply migration twice; verify migration history and persistent state across restart | FR-007, FR-008 |
| AT-006 | `git ls-files` review + secret detection; no personal media/secret fixtures | FR-006, NFR-001 |
| AT-007 | Playwright desktop 1280px + mobile 360px; assert shell visible and zero horizontal overflow | FR-009, NFR-003 |
| AT-008 | Test placeholder labels/disabled actions; no simulated writes | FR-010 |
| AT-009 | Backend-off browser test; shell stays visible and shows safe status | FR-011 |
| AT-010 | Backend build/test/format, frontend lint/typecheck/test/build, browser smoke, CI failure injection | FR-012, FR-013 |
| AT-011 | Docs review: no public port-forwarding required; self-hosted home target clearly future work | FR-014, NFR-002 |

For integration tests, use a disposable test database or container and isolate test state. Avoid relying on any maintainer's real data, production server or secrets.

## 9. CI quality gate

Trigger GitHub Actions on pull requests to the primary branch. At minimum:

- Check out code, restore pinned .NET and Node dependencies.
- Build and test .NET projects; enforce chosen formatting rules.
- `npm ci`, lint/typecheck, test and build frontend.
- Provision an ephemeral test PostgreSQL service for readiness and migration integration tests; do not use a developer's credentials.
- Run responsive browser tests at 360px and 1280px, or ensure a CI job executes them as part of acceptance.
- A failed test/build step fails the workflow. Capture meaningful non-sensitive logs.

Provide one documented local verification entry point. If CI runs separate jobs, list the exact commands that correspond to the local gate.

## 10. Delivery slices (input to future `tasks.md`)

1. **Repository and toolchains:** structure, pinned runtimes, ignores and basic docs.
2. **Local database:** Compose, safe config, migration baseline, persistence.
3. **Backend service:** health endpoints, dependency failure behavior, tests.
4. **Responsive frontend:** shell, placeholders, optional safe health status and browser tests.
5. **Verification and CI:** local quality script, GitHub Actions, clean-start walkthrough, final spec traceability.

These are planning slices, **not executable tasks**. Generate `tasks.md` only after the plan has been reviewed and its open decisions closed.

## 11. Risks, mitigations and open decisions

| ID | Risk / pending decision | Proposed mitigation / approval required |
|---|---|---|
| OQ-001 | Existing Milestone 1 TDD may include authentication or family management | Keep SPEC-001 foundation-only; propose separate specs for additional capabilities. Compare against TDD before plan approval. |
| OQ-002 | .NET, database, data access, styling may conflict with earlier designs | Review existing Backend and Frontend Design, record actual approved stack; if changing, create ADR. |
| OQ-003 | Primary developer OS not designated | Choose Windows/WSL2 or Linux; validate clean checkout and tool prerequisites. |
| OQ-004 | Container vs native local DB undecided | Proposed Docker Compose DB, native SDK dev servers; approve or replace consistently. |
| OQ-005 | CI provider unconfirmed | Proposed GitHub Actions for GitHub repo; approve or replace. |
| R-001 | API reports ready while DB unavailable | Readiness integration test with DB stopped; process-only liveness. |
| R-002 | Commit of secrets or private photos | `.gitignore`, examples only, secret scan and fixture audit. |
| R-003 | CI passes while clean-machine startup fails | Run separate documented clean-checkout acceptance on supported OS. |
| R-004 | Overengineering foundation with future product modules | Defer domain model, authorization and object storage to subsequent specs. |

### Approval gate for this plan

Before assigning `plan.md` status **Approved**, the maintainer should:

- [ ] Confirm existing Backend/Frontend Design and Milestone 1 TDD have been consulted.
- [ ] Ratify the technology and version choices or attach ADRs explaining deviations.
- [ ] Designate supported local development OS and exact reproducible commands.
- [ ] Approve the local container and CI approach.
- [ ] Confirm every FR/NFR and AT has test/design coverage without scope creep.

## 12. Definition of ready for implementation

`plan.md` is approved; dependencies and versions are pinned in the follow-on implementation; `tasks.md` includes scoped, verifiable tasks linked to FR/NFR and AT IDs; coding work starts on a dedicated feature branch or pull request. Do not treat plan approval as acceptance of implementation: all AT-001 through AT-011 must still be demonstrated.

## 13. References

- [`spec.md`](./spec.md) — SPEC-001 approved behavioral requirements.
- Existing Family Memories Frontend Design / Backend Design / Technical Design Document (not attached to this planning draft; **must be reconciled**).
- Official .NET lifecycle: https://learn.microsoft.com/en-us/dotnet/core/releases-and-support
- Official PostgreSQL release policy: https://www.postgresql.org/support/versioning/
