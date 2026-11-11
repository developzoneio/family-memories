# SPEC-001 — Project Foundation & Local Development

> **Project:** Family Memories  
> **Milestone:** 1 — Foundation (proposed first increment)  
> **Feature branch:** `001-project-foundation`  
> **Status:** Draft — awaiting review  
> **Version:** 0.1.0  
> **Created:** 2026-11-11  
> **Specification owner:** Project maintainer

## 1. Intent

Establish a reproducible, secure-by-default foundation on which the Family Memories web application can be incrementally developed and tested. A developer should be able to obtain the source, configure the environment, start the baseline application, verify its dependencies, and receive rapid feedback when changes break that baseline.

This specification defines **observable outcomes**, not how to implement them. Detailed architecture, dependency versions, directory design, database technology, and deployment topology belong in `plan.md` and Architecture Decision Records (ADRs), and must remain consistent with the existing Frontend Design and Backend Design.

## 2. Confirmed project context

The following decisions are inherited from prior Family Memories planning, not newly decided by this specification:

- **Product:** private family photo-sharing web application.
- **Frontend:** React, usable in desktop and mobile browsers; this is not a native mobile app.
- **Deployment target:** self-hosted at home.
- **Expected scale:** medium.
- **Visibility model:** family-scoped content.
- **Photo behavior in the eventual product:** manual upload and support for original and optimized renditions.
- **Later product capabilities:** family timeline, albums/events, original-photo download, membership and access management.

**Working proposal to validate at planning:** ASP.NET Core/.NET backend. The exact .NET version, database engine, hosting strategy, CI provider, and source layout are *not approved by this specification*; reconcile them with existing technical designs before implementation.

## 3. Problem and expected outcome

Without a shared baseline, subsequent authentication, family, and media features can accumulate divergent environment requirements, manual setup steps, insecure defaults, and untestable integration assumptions.

**Success means:** an unfamiliar developer can follow the documented setup from a clean clone, start the frontend/backend/dependencies, view a usable responsive application shell, check API liveness and dependency readiness, run migrations and tests, and see comparable checks performed in CI.

## 4. User stories (prioritized)

### US-001 — Reproducible local startup (P1)

As a developer, I want a documented local startup process so I can begin working on the application without discovering undocumented prerequisites or configuration.

**Acceptance scenarios**

1. **Given** a clean checkout on a supported development environment and installed documented prerequisites, **when** I follow the quick-start steps and supply only required local configuration, **then** the web application, API and required local infrastructure become accessible at the documented addresses.
2. **Given** the application is stopped, **when** I start it again using the same documented process, **then** startup works without modifying tracked source files.
3. **Given** an essential prerequisite is absent or configuration is invalid, **when** I attempt startup, **then** the failure is explained by a documented diagnostic or readable error, rather than silent malfunction.

### US-002 — Observable backend state (P1)

As a developer/operator, I want to distinguish a running API process from an API ready to serve requests that require its dependencies.

**Acceptance scenarios**

1. **Given** the API process is serving HTTP, **when** I request `GET /health/live`, **then** I receive HTTP 200 and a minimal machine-readable status response that does not expose secrets.
2. **Given** the API and required database dependency are operational, **when** I request `GET /health/ready`, **then** I receive HTTP 200 with a minimal ready status.
3. **Given** the database is unavailable but the API process remains running, **when** I request `GET /health/ready`, **then** I receive HTTP 503; `GET /health/live` continues to report the process as live.
4. **Given** either health endpoint is called, **when** the response is returned, **then** it contains no credentials, database connection strings, internal stack traces, or sensitive infrastructure detail.

### US-003 — Safe, repeatable configuration and persistence (P1)

As a maintainer, I want a safe configuration and database initialization process so local development does not depend on committed secrets or undocumented manual database changes.

**Acceptance scenarios**

1. **Given** the repository is checked out, **when** I review tracked configuration, **then** I find configuration examples and setup guidance but no live credentials or private family images.
2. **Given** an empty supported local database, **when** I execute the documented initialization/migration process, **then** the baseline schema state is recorded and a second run is safe.
3. **Given** a successfully initialized persistent local database, **when** I stop and restart application services without explicitly resetting data, **then** the database state remains intact.
4. **Given** a required configuration value is absent, **when** a dependent service initializes, **then** it fails with an actionable error without printing the secret or connection string.

### US-004 — Responsive web application shell (P2)

As a family member evaluating early progress, I want a recognizably branded web shell that works in desktop and mobile browsers, without mistaking placeholder features for finished functionality.

**Acceptance scenarios**

1. **Given** a modern desktop browser at 1280 CSS-pixel viewport width, **when** I open the documented frontend URL, **then** a Family Memories shell loads without an application error.
2. **Given** a mobile browser at 360 CSS-pixel viewport width, **when** I open that URL, **then** primary shell content is usable without horizontal page overflow.
3. **Given** that core product capabilities have not been implemented, **when** I view or interact with their placeholders, **then** they are clearly labeled unavailable/coming soon and do not pretend to create or change family data.
4. **Given** the backend is unavailable, **when** the frontend attempts an optional backend-dependent status check, **then** the shell remains usable and shows a non-sensitive, understandable status/error.

### US-005 — Automated baseline verification (P2)

As a maintainer, I want a repeatable verification command and CI checks so breakages in the initial foundation are detected before changes are merged.

**Acceptance scenarios**

1. **Given** a clean checkout with documented toolchain, **when** the documented validation command(s) execute, **then** frontend build, backend build, automated tests, and applicable formatting/lint checks produce an unambiguous pass/fail result.
2. **Given** a pull request, **when** CI runs, **then** the same minimum checks run without needing a developer's personal secret values.
3. **Given** an intentional test failure, **when** CI runs, **then** the check fails and identifies the failed stage.

## 5. Functional requirements

All MUST requirements are in scope for acceptance of SPEC-001.

| ID | Requirement | Related story |
|---|---|---|
| FR-001 | The repository MUST document prerequisites, setup, startup, shutdown, test, and troubleshooting procedures. | US-001 |
| FR-002 | A developer MUST be able to start the frontend, backend, and required local dependencies using documented, repeatable commands. No manually pre-provisioned paid/cloud service MUST be required for local acceptance. | US-001 |
| FR-003 | The backend MUST provide `GET /health/live`; an active API process returns HTTP 200 regardless of database readiness. | US-002 |
| FR-004 | The backend MUST provide `GET /health/ready`; it returns HTTP 200 when required dependencies are ready and HTTP 503 when any required dependency is not ready. | US-002 |
| FR-005 | Health responses MUST avoid credentials, stack traces, database names/hosts, and internal topology. | US-002 |
| FR-006 | The repository MUST provide safe configuration examples; runtime secrets and local personal/family data MUST remain untracked. | US-003 |
| FR-007 | The local development workflow MUST provide a documented, repeatable mechanism to initialize/upgrade the database to the project's baseline schema version. | US-003 |
| FR-008 | Normal service restarts MUST NOT delete local database data; an explicit reset mechanism MAY be provided with a destructive-action warning. | US-003 |
| FR-009 | The React frontend MUST display a responsive Family Memories shell at 360px and 1280px viewport widths. | US-004 |
| FR-010 | Unimplemented product operations MUST be visibly nonfunctional; the shell MUST NOT simulate successful photo uploads, invitations, or membership changes. | US-004 |
| FR-011 | Frontend/backend service failures MUST be diagnosable without leaking secrets or crashing the basic frontend shell. | US-001, US-004 |
| FR-012 | The repository MUST expose documented local validation commands for frontend, backend, and automated tests. | US-005 |
| FR-013 | CI MUST execute the defined baseline checks on changes proposed for merging and report a failing status on a failed check. | US-005 |
| FR-014 | Documentation MUST describe how local infrastructure relates to the intended self-hosted home deployment, but production deployment itself is not implemented in this specification. | US-001 |

## 6. Nonfunctional and security requirements

| ID | Requirement / verification criterion |
|---|---|
| NFR-001 | **Privacy first:** no sample real family member accounts, private photos, or actual secrets are included in source control, test fixtures, screenshots or logs. |
| NFR-002 | **Local-only by default:** the documented development configuration MUST NOT require public internet exposure or inbound router port forwarding. |
| NFR-003 | **Responsive baseline:** at 360px and 1280px CSS viewport widths, main navigation/shell remains readable and no horizontal page overflow occurs. |
| NFR-004 | **Diagnosability:** failed startup, failed database readiness, and automated-test failure must produce actionable non-sensitive diagnostics. |
| NFR-005 | **Reproducibility:** the documented setup must work from a clean checkout on at least one explicitly supported developer operating system, with tool versions/prerequisites stated. |
| NFR-006 | **No false readiness:** the API readiness endpoint cannot return HTTP 200 if a dependency required for database-backed features is unavailable. |

> This milestone does **not** authorize exposing an unauthenticated write API to the home network or the public internet. Future application endpoints require dedicated authentication/authorization specifications.

## 7. Observable contracts

These contracts are part of this specification; payload schemas beyond minimal status semantics will be finalized in the technical plan.

| Contract | Successful result | Unavailable result |
|---|---|---|
| `GET /health/live` | HTTP 200 when API HTTP process is operational | Connection failure if process is not serving |
| `GET /health/ready` | HTTP 200 when required dependencies are healthy | HTTP 503 if a required dependency fails |
| Frontend shell | Renders app branding and honest placeholders | Still renders when backend-dependent optional checks fail |
| Database initialization | Recorded baseline migration state; repeatable | Non-zero exit/actionable error if initialization fails |
| Local/CI validation | Zero exit/status on all required checks | Non-zero exit/status if any required check fails |

Health payloads SHOULD use a minimal shape such as `{ "status": "healthy" }` or `{ "status": "unhealthy" }`; do not treat this illustrative JSON as a full versioned API schema.

## 8. Boundary and non-goals

**Included:** project bootstrap, local development, API health/readiness, database initialization/migrations, responsive shell, configuration safety, minimal test harness, CI verification, and operational setup documentation.

**Excluded:** login, user registration, family creation/invites, role enforcement, timeline/posts, albums, media upload/optimization/download, object storage integration, notifications, external sharing, backup automation, domain/TLS/reverse-proxy configuration, production release, and real family data migration.

The exclusion of media and authorization features does **not** weaken the project's family-private product requirement: no actual family content is managed in this foundation increment.

## 9. Verification matrix

| Test ID | Evidence required | Covers |
|---|---|---|
| AT-001 | From a clean checkout, follow README and open frontend/API at documented addresses | FR-001, FR-002, NFR-005 |
| AT-002 | Invoke live and ready endpoints with healthy DB; both return HTTP 200 | FR-003, FR-004 |
| AT-003 | Stop DB only; ready returns HTTP 503 while live continues HTTP 200 | FR-003, FR-004, NFR-006 |
| AT-004 | Inspect health/error outputs for secrets and infra details; none present | FR-005, FR-011, NFR-004 |
| AT-005 | Run baseline migration twice; second succeeds; restart retains data | FR-007, FR-008 |
| AT-006 | Validate tracked files for credential placeholders, not real secrets/personal media | FR-006, NFR-001 |
| AT-007 | Browser smoke test at 360px and 1280px; no horizontal overflow | FR-009, NFR-003 |
| AT-008 | Verify unimplemented operations are plainly disabled/labeled and don't persist data | FR-010 |
| AT-009 | Stop backend; verify frontend shell remains viewable and status is understandable | FR-011 |
| AT-010 | Run documented local checks and CI; introduce intentional failed test and observe CI fail | FR-012, FR-013 |
| AT-011 | Verify dev setup requires no public router forwarding and README explains future home-hosted deployment boundary | FR-014, NFR-002 |

## 10. Dependencies and assumptions

- The project maintainer will designate at least one supported development OS for the quick start.
- Existing Frontend Design and Backend Design remain the architecture source of truth unless a deliberate, documented ADR supersedes them.
- A relational database and schema migration tool are *proposed* for the foundation; use the DB technology already selected in the Backend Design, if any.
- Continuous integration provider and local container/runtime details are selected in the technical plan.
- The application shell may show placeholders for Timeline, Albums and Family but cannot claim these features are implemented.

## 11. Open questions before technical planning

| ID | Question | Consequence | Owner |
|---|---|---|---|
| OQ-001 | What is the exact Milestone 1 scope in the existing Technical Design Document? Does it include authentication or family management? | If yes, split into additional focused specs rather than expanding this foundation spec indiscriminately. | Project maintainer |
| OQ-002 | What .NET version, database engine, and migration strategy were already approved in Backend Design? | Technical plan must conform instead of introducing a conflicting stack. | Project maintainer |
| OQ-003 | Which primary development environment (Windows/WSL2, macOS, Linux) is supported first? | Quick-start validation environment. | Project maintainer |
| OQ-004 | Will local infrastructure run using containers or native dependencies? | Determines repeatable commands, ports, and data lifecycle. | Technical plan |
| OQ-005 | Which CI provider will run the pull-request quality gate? | Defines pipeline implementation. | Technical plan |

These questions do not prevent reviewing the behavioral acceptance criteria. They MUST be resolved or documented as approved assumptions before `plan.md` is finalized.

## 12. Definition of Done

SPEC-001 is complete only when:

- [ ] Scope and acceptance scenarios are reviewed and approved.
- [ ] All open questions that block implementation are resolved or recorded in ADRs.
- [ ] Every MUST requirement (FR/NFR) has test evidence, a review artifact, or an explicitly approved exception.
- [ ] A clean-checkout setup demonstration passes (`AT-001`).
- [ ] Health/readiness, DB restart, config-safety, and responsive-shell tests pass (`AT-002` to `AT-009`).
- [ ] Local validation and CI behave as specified (`AT-010`).
- [ ] The README distinguishes development from production deployment (`AT-011`).
- [ ] Architecture and implementation are documented in `plan.md`; executable task decomposition in `tasks.md`.
- [ ] A reviewable pull request references `SPEC-001` and includes verification results.

## 13. Change control

- Changes to observable behavior require an update to this specification and its acceptance scenarios **before** implementation changes.
- Technical choices that preserve requirements belong in `plan.md` / ADRs.
- New user-facing capabilities (authentication, albums, uploads, etc.) require their own numbered specification(s).
- Approval changes `Status` to **Approved** and records the approval date/reviewer in the PR; until then this document is a proposal, not authorization to implement.
