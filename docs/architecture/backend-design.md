# Family Memories — Backend Design

> **Document ID:** DES-002  
> **Version:** 1.0.0  
> **Status:** **Approved v1.0.0** — project maintainer, 2026-11-27 (stated in session; confirmed by merging
> PR [#35](https://github.com/developzoneio/family-memories/pull/35))  
> **Created:** 2026-11-27  
> **Owner:** Project maintainer  
> **Tracking:** GitHub issue [#3](https://github.com/developzoneio/family-memories/issues/3) (DES-002, DOC-02, GAP-03,
> GAP-06, GAP-12; SPEC-001 OQ-002)

## 1. Purpose and how to read this document

This document is the backend architecture baseline for Family Memories: the technology stack, the solution structure,
the cross-cutting rules every backend change follows, and the direction for later capabilities. It does **not** design
individual features. API endpoints, tables and workflows for authentication, media, posts, albums and notifications
belong in the specification of the milestone that delivers them (Product Requirements MS-05).

Every statement carries one label, with the same meaning as in the
[Product Requirements baseline](../product/requirements.md):

| Label | Meaning |
|---|---|
| **Confirmed** | Backed by a source in Section 2: an explicit maintainer decision, or an approved or accepted repository document. |
| **Proposal** | Suggested by this document or by a draft, and not explicitly decided by the maintainer. |
| **Open** | Not decided. Tracked in Section 15, usually with the milestone that must decide it. |

## 2. Sources

| Key | Source | Date | Notes |
|---|---|---|---|
| M | Maintainer decisions in the Claude Code session that drafted this document | 2026-11-27 | Answers chosen from offered options (quoted in the rows that cite M). |
| CS | Maintainer coding standards (the maintainer's global engineering rules) | Current | Summarized in Section 12. The maintainer chose to adopt them as project rules. |
| DES-001 | [Product Requirements baseline](../product/requirements.md) | Approved v1.0.0, 2026-11-27 | Product scope that drives this design. |
| ADR-001 | [ADR-001 Azure deployment target](../adr/ADR-001-azure-deployment-target.md) | Accepted, 2026-11-27 | Hosting services, including the ASP.NET Core API and PostgreSQL Flexible Server. |
| SPEC-001 | [SPEC-001 Project Foundation](../specs/001-project-foundation/spec.md) | Approved v1.1.0; amended to v1.2.0 by this change | Foundation behavior, including the health contract. |
| SPEC-002 | [SPEC-002 Azure Deployment](../specs/002-azure-deployment/spec.md) | Draft v0.1.0 | Supports **Proposal** labels only. |
| PLAN-001 | [SPEC-001 technical plan](../specs/001-project-foundation/plan.md) | Draft v0.1 | Supports **Proposal** labels only. |
| VER | Official lifecycle pages, checked 2026-11-27 | 2026-11-27 | [.NET support policy](https://dotnet.microsoft.com/en-us/platform/support/policy/dotnet-core); [PostgreSQL 18 GA on Azure Flexible Server](https://techcommunity.microsoft.com/blog/adforpostgresql/postgresql-18-now-ga-on-azure-postgres-flexible-server/4469802); [Azure PostgreSQL January 2026 release notes](https://learn.microsoft.com/en-us/azure/postgresql/release-notes-maintenance/2026-january); [Npgsql EF Core 10.0 release notes](https://www.npgsql.org/efcore/release-notes/10.0.html). |

**Earlier Backend Design sessions.** Three earlier ChatGPT conversations (*Đề xuất Backend Design*, *Cập nhật Backend
Design* and the consolidated *Backend Design*, 2026-11-10) could not be recovered (product-evidence export, PRD-J14,
PRD-K09). The maintainer chose to decide the backend afresh in session instead of recovering them. This document
therefore **replaces** those earlier designs; nothing from them is carried over.

## 3. Design drivers

| ID | Driver | Label | Source |
|---|---|---|---|
| DRV-01 | One deployment serves **one family**; no multi-tenancy. | Confirmed | DES-001 FAM-01 |
| DRV-02 | Two roles, **Admin** and **Member**; members join through expiring, revocable invite links. | Confirmed | DES-001 USR-04, FAM-03 |
| DRV-03 | **Medium scale:** up to 50 members and about 10,000 photos a year, with few members online at once. | Confirmed | DES-001 QLT-01 |
| DRV-04 | Photos only (JPEG, PNG, HEIC, up to 25 MB); each kept as an unchanged original plus an optimized rendition. | Confirmed | DES-001 CAP-01, CAP-02, CAP-10 |
| DRV-05 | Content is **never shared outside the family**; no real family data in Azure before authentication exists. | Confirmed | DES-001 PRV-02, PRV-05 |
| DRV-06 | Production on Azure App Service (Linux), behind Azure Static Web Apps, which forwards only `/api/*` to the API. Requests through Static Web Apps time out after 45 seconds. | Confirmed | ADR-001 |
| DRV-07 | The backend is maintained by a very small team, so operational and structural simplicity beats flexibility. | Proposal | This document; follows from DRV-03 |

## 4. Technology stack

| ID | Area | Decision | Label | Source |
|---|---|---|---|---|
| STK-01 | Runtime | **.NET 10 (LTS)**, supported until 2028-11-14. Pin the SDK in `global.json`. | Confirmed | M ("dùng .NET 10"); VER |
| STK-02 | Web framework | **ASP.NET Core** on .NET 10. | Confirmed | ADR-001 (Decision); M |
| STK-03 | Database engine | **PostgreSQL 18**: Azure Database for PostgreSQL Flexible Server in Azure (GA since January 2026, all public regions), a PostgreSQL 18 container locally. | Confirmed | M ("PG 18 + EF Core 10 migrations"); ADR-001; VER |
| STK-04 | Fallback engine | The maintainer allowed Microsoft SQL Server **only if PostgreSQL could not be used**. PostgreSQL 18 is available on Azure and supported by the data provider, so SQL Server is **not adopted**. | Confirmed | M; VER |
| STK-05 | Data access | **EF Core 10** with the **Npgsql** provider (`Npgsql.EntityFrameworkCore.PostgreSQL` 10.x). | Confirmed | M; VER |
| STK-06 | Schema changes | **EF Core migrations only.** Migrations are applied by an explicit command, never automatically at application startup. | Confirmed | M; SPEC-001 FR-007 |
| STK-07 | Tests | xUnit for unit and integration tests; ASP.NET Core `WebApplicationFactory` for API tests; Testcontainers for a disposable PostgreSQL 18 database. | Proposal | PLAN-001 §2 (xUnit, integration tooling); this document (Testcontainers) |
| STK-08 | Local database | PostgreSQL 18 in Docker Compose with a named volume. | Proposal | PLAN-001 §2, §6; SPEC-001 OQ-004 |

## 5. Architecture style and solution structure

| ID | Statement | Label | Source |
|---|---|---|---|
| ARC-01 | The backend is **one deployable application** (a monolith) structured with **Clean Architecture** layers. | Confirmed | M ("Clean Architecture layers"); ADR-001 (one App Service API) |
| ARC-02 | **Dependency rule:** dependencies point inward only. Domain depends on nothing; Application depends on Domain; Infrastructure implements Application interfaces; Api is the composition root that references Application and Infrastructure. | Confirmed | M (inherent to Clean Architecture) |
| ARC-03 | Four production projects: `FamilyMemories.Domain`, `FamilyMemories.Application`, `FamilyMemories.Infrastructure`, `FamilyMemories.Api`. | Proposal | This document |
| ARC-04 | Feature modules (Membership, Media, Posts, Albums, Notifications) are **folders and namespaces inside each layer**, not separate projects. A module may become its own project later only if it needs a hard boundary. | Proposal | This document |
| ARC-05 | Use cases are plain handler or service classes in Application, registered with dependency injection. **No mediator library** (for example MediatR, which moved to a commercial license in 2025): at this scale direct calls are simpler. | Proposal | This document |
| ARC-06 | HTTP endpoints use **ASP.NET Core Minimal APIs**, grouped per module with route groups. Endpoints translate HTTP to use-case calls and contain no business rules. | Proposal | This document; PLAN-001 §2 ("minimal initial API") |
| ARC-07 | In Milestone 1, Domain and Application stay **empty apart from structure**. The only behavior is the health endpoints and the database connection, as SPEC-001 requires. | Proposal | SPEC-001 §8; PLAN-001 R-004 |
| ARC-08 | Test projects: `FamilyMemories.UnitTests` (Domain and Application) and `FamilyMemories.IntegrationTests` (Api and Infrastructure against PostgreSQL). | Proposal | This document; PLAN-001 §4 |

```text
src/backend/
├── FamilyMemories.Domain/           # entities, value objects, domain exceptions; no dependencies
├── FamilyMemories.Application/      # use cases, interfaces (ports); depends on Domain
├── FamilyMemories.Infrastructure/   # EF Core DbContext, migrations, Identity, storage; implements Application
└── FamilyMemories.Api/              # Minimal API endpoints, health checks, DI composition root
tests/backend/
├── FamilyMemories.UnitTests/
└── FamilyMemories.IntegrationTests/
```

```text
Browser ──> Azure Static Web Apps ──/api/*──> FamilyMemories.Api
                                                │  references
                                  ┌─────────────┴─────────────┐
                                  v                           v
                    FamilyMemories.Application ◄── FamilyMemories.Infrastructure ──> PostgreSQL 18
                                  │                (implements interfaces)
                                  v
                       FamilyMemories.Domain
```

## 6. API conventions

| ID | Statement | Label | Source |
|---|---|---|---|
| API-01 | Every browser-reachable endpoint lives under **`/api`**, because Static Web Apps forwards only `/api/*` to the linked API. The same paths are used locally (through the Vite dev proxy) and in Azure. | Confirmed | ADR-001; SPEC-002 OQ-209; M |
| API-02 | Health endpoints are **`GET /api/health/live`** and **`GET /api/health/ready`**. This replaces `/health/live` and `/health/ready` and amends SPEC-001 FR-003/FR-004 (v1.2.0). The App Service health check uses `/api/health/live`. | Confirmed | M ("/api/health/live and /api/health/ready") |
| API-03 | Liveness runs no dependency checks. Readiness checks the database. Payloads stay minimal (`{ "status": "healthy" }` / `{ "status": "unhealthy" }`) and expose no hosts, names, versions or errors. Built on ASP.NET Core health checks. | Confirmed (behavior) / Proposal (mechanism) | SPEC-001 FR-003 … FR-005, §7; this document |
| API-04 | Paths are grouped by module, for example `/api/membership/...` and `/api/media/...`. JSON uses camelCase (the ASP.NET Core default). | Proposal | This document |
| API-05 | Errors are returned as **Problem Details** (RFC 9457) with no stack traces or internal details. | Proposal | This document; SPEC-001 FR-005, FR-011 |
| API-06 | No API versioning for now: the React app is the only client and ships together with the API. | Proposal | This document |

## 7. Data and persistence

| ID | Statement | Label | Source |
|---|---|---|---|
| DAT-01 | One application database on PostgreSQL 18, accessed through one EF Core `DbContext` in Infrastructure. | Proposal | This document |
| DAT-02 | Each module owns its tables in its own PostgreSQL schema (for example `membership`, `media`), so module boundaries are visible in the database. | Proposal | This document |
| DAT-03 | Identifiers are UUID version 7, generated in the application (`Guid.CreateVersion7()`), so they sort by creation time. | Proposal | This document; VER (PostgreSQL 18 also offers `uuidv7()`) |
| DAT-04 | Timestamps are stored as UTC `timestamptz` and read through `TimeProvider` so that tests can control time. | Proposal | This document |
| DAT-05 | Locally, migrations run with a documented `dotnet ef database update` command. For Azure, migrations are packaged as an **EF Core migration bundle** and run as an explicit deployment step; where it runs from is SPEC-002 OQ-206. | Confirmed (explicit, never at startup) / Proposal (bundle) | M; SPEC-001 FR-007; SPEC-002 OQ-206 |
| DAT-06 | The baseline migration in Milestone 1 creates **no product tables** (family, identity, photos, albums). Each later specification adds its own tables. | Proposal | PLAN-001 §6; SPEC-001 §8 |
| DAT-07 | Restarting the API or the database never deletes data; a reset is an explicit, clearly destructive command. | Confirmed | SPEC-001 FR-008 |

## 8. Authentication and authorization (direction for M3)

| ID | Statement | Label | Source |
|---|---|---|---|
| AUT-01 | Authentication uses **ASP.NET Core Identity inside the application**, with accounts stored in the application's PostgreSQL database. No external identity provider and no extra Azure service. | Confirmed | M ("ASP.NET Core Identity in-app") |
| AUT-02 | The browser session is a **secure, HttpOnly cookie** issued by the API. Because the frontend and `/api` share one origin through Static Web Apps, no CORS policy is needed. | Proposal | This document; follows from API-01 |
| AUT-03 | Authorization is role-based with the two roles **Admin** and **Member**, expressed as ASP.NET Core authorization policies. Every endpoint except health requires an authenticated member. | Confirmed (roles) / Proposal (mechanism) | DES-001 USR-04; SPEC-001 §6 |
| AUT-04 | Invite links carry a random token. Only a hash of the token is stored; the link expires and an Admin can revoke it. | Confirmed (expiry, revocation) / Proposal (hashing) | DES-001 FAM-03; this document |
| AUT-05 | No endpoint that writes data is exposed without authentication. | Confirmed | SPEC-001 §6; PLAN-001 §1 |
| AUT-06 | Sign-in method, password rules, multi-factor or passkeys, account recovery and CSRF protection for cookie requests. | Open | OQ-B01, OQ-B02 (M3 specification) |

## 9. Media, background work and other capabilities (direction for M4 and later)

| ID | Statement | Label | Source |
|---|---|---|---|
| MED-01 | Photo files are stored in **Azure Blob Storage** in a private container, not in the database. Blob Storage is not yet one of the ADR-001 services, so the M4 specification must add it through an ADR or an ADR-001 update. | Proposal | ADR-001 (Consequences); SPEC-002 OQ-208 |
| MED-02 | The browser uploads originals **directly to Blob Storage** with a short-lived, write-only shared access signature issued by the API, avoiding the 45-second Static Web Apps limit. | Proposal | ADR-001 (Consequences); SPEC-002 OQ-208 |
| MED-03 | Originals are stored unchanged; optimized renditions are created **asynchronously** after upload. The image library must decode HEIC; library choice, rendition sizes and output format are decided in M4. | Confirmed (originals unchanged) / Proposal (asynchronous) / Open (library, sizes) | DES-001 CAP-02; OQ-B03 |
| MED-04 | Background work (renditions, notifications) runs **inside the API process** as a hosted background service that reads a job table in PostgreSQL. No message broker and no Azure Functions at this scale. | Proposal | This document; DRV-03, DRV-07 |
| MED-05 | Notifications are stored in PostgreSQL and shown in-app. Whether they are pushed in real time (for example SignalR) or fetched by polling is decided in the notifications specification. | Confirmed (in-app) / Open (delivery) | DES-001 CAP-13; OQ-B08 |
| MED-06 | Search and filter (by date, album or uploader) are plain PostgreSQL queries; no separate search engine. | Proposal | DES-001 CAP-14; DRV-03 |

## 10. Configuration, secrets and logging

| ID | Statement | Label | Source |
|---|---|---|---|
| CFG-01 | All configuration is read through the .NET configuration system, so environment variables and App Service settings override files without code changes. | Proposal | PLAN-001 R-005 |
| CFG-02 | Configuration is bound to typed options and **validated at startup**; a missing or invalid value stops the API with an actionable message that contains no secret. | Proposal | PLAN-001 §6; SPEC-001 FR-006, FR-011 |
| CFG-03 | Secrets are never committed. Locally they live in .NET user secrets or an untracked `.env`; in Azure they come from **Key Vault references** read through a managed identity. | Confirmed | SPEC-001 FR-006, NFR-001; ADR-001 |
| LOG-01 | Logging uses `Microsoft.Extensions.Logging` with structured message templates and a correlation ID per request. | Proposal | PLAN-001 §3 |
| LOG-02 | Logs never contain secrets, tokens, connection strings or **personal content** (names, emails, captions, photo data). When an error is logged with "the values that caused it" (CS), those values are **identifiers** such as member or photo IDs. | Confirmed (no secrets or personal data) / Proposal (identifiers rule) | SPEC-001 NFR-001, FR-005; CS; this document |
| LOG-03 | Monitoring in Azure (App Service health check, Azure Monitor alerts, Application Insights). | Open | SPEC-002 OQ-207 |

## 11. Error handling

| ID | Statement | Label | Source |
|---|---|---|---|
| ERR-01 | Business errors are signalled with **custom domain exceptions** only, for example `InviteLinkExpiredException`. No `throw new Exception(...)` and no `Result<T>` types. | Confirmed | CS |
| ERR-02 | Domain exceptions derive from a small set of abstract base classes in Domain (for example not found, conflict, forbidden, validation), and **one** ASP.NET Core exception handler in Api maps each base class to an HTTP status and a Problem Details body. Unknown exceptions become HTTP 500 with no details. | Proposal | This document |
| ERR-03 | `try`/`catch` is used at the **smallest scope** around the call that can fail, never around a whole flow, and the log entry includes the values that caused the failure (see LOG-02). | Confirmed | CS |

## 12. Engineering conventions

The maintainer's coding standards are project rules for all C# code. Summary:

| ID | Rule | Label | Source |
|---|---|---|---|
| CON-01 | Negation is written `== false` (`if (isValid == false)`); `TryParse`/`TryGetValue` results are compared with `== true`. | Confirmed | CS |
| CON-02 | `if` blocks always use braces, even for one statement. | Confirmed | CS |
| CON-03 | Maximum line length 120 characters; indentation 4 spaces, no tabs. | Confirmed | CS |
| CON-04 | No static classes with static methods; use a `static readonly` instance instead. | Confirmed | CS |
| CON-05 | **Exception to CON-04:** C# requires extension methods to be declared in static classes. Static classes are therefore allowed **only** to hold extension methods, such as service registration (`AddInfrastructure`) and endpoint mapping (`MapMembershipEndpoints`). | Confirmed | M (OQ-B09, 2026-11-27) |
| CON-06 | Naming: PascalCase for types and public members; `I` prefix for interfaces; `_camelCase` for private fields; camelCase for parameters and locals; `ALL_UPPER_CASE` for constants; `Exception` suffix for exceptions; `is`/`was`/`has` prefix for booleans; plural names for collections. | Confirmed | CS |
| CON-07 | Member order: public, then protected, then private; within each, constants, then static, then instance. Private fields in the order settings/options, logger, cache, data access, business logic, other. | Confirmed | CS |
| CON-08 | Size limits: a class at most 1,000 lines; a method at most 100 lines, aiming for 30–50. | Confirmed | CS |
| CON-09 | Comments sit on their own line, start with an uppercase letter and are written in English; no comments at the end of a code line. | Confirmed | CS |
| CON-10 | The rules that tools can check (formatting, braces, line length, naming) are enforced with `.editorconfig` and `dotnet format --verify-no-changes` in CI. | Proposal | This document; SPEC-001 FR-013 |

## 13. Scale and deliberate simplicity

| ID | Statement | Label | Source |
|---|---|---|---|
| SCL-01 | One App Service instance and one PostgreSQL server are enough for DRV-03; the design does not need horizontal scaling. | Proposal | DRV-03 |
| SCL-02 | Not adopted: microservices, a message broker, a distributed cache (for example Redis), a separate search engine, a mediator library, multi-tenancy, infrastructure as code. | Confirmed (multi-tenancy, infrastructure as code) / Proposal (the rest) | DES-001 OUT-04; ADR-001; this document |

## 14. Superseded and changed decisions

| Before | Now | Source |
|---|---|---|
| Health routes `/health/live` and `/health/ready` (SPEC-001 v1.1.0). | `/api/health/live` and `/api/health/ready` (SPEC-001 v1.2.0). | M; API-02 |
| PostgreSQL 17 proposed in the draft plan. | PostgreSQL 18. | M; STK-03 |
| Two projects (Api, Infrastructure) proposed in the draft plan. | Four Clean Architecture projects. | M; ARC-01, ARC-03 |
| Earlier ChatGPT Backend Design sessions (not recovered). | This document. | M; Section 2 |

## 15. Open questions

| ID | Question | Decide in |
|---|---|---|
| OQ-B01 | Sign-in method (email and password, passkeys, ...), password rules, multi-factor authentication and account recovery. | M3 specification (DES-001 OQ-P04) |
| OQ-B02 | CSRF protection for cookie-authenticated requests (antiforgery tokens or a required custom header with strict SameSite cookies). | M3 specification |
| OQ-B03 | Image library that decodes HEIC on Linux, rendition sizes, output format and compression. | M4 specification (DES-001 OQ-P12) |
| OQ-B04 | Adding Blob Storage to the Azure design (ADR), container layout, and how the browser reads photos (short-lived read signatures or streaming through the API). | M4 specification |
| OQ-B05 | Final background-job mechanism and retry policy. | M4 specification |
| OQ-B06 | How the API authenticates to PostgreSQL in Azure: password from Key Vault or Microsoft Entra managed identity. | SPEC-002 |
| OQ-B07 | Where Azure migrations run from. | SPEC-002 OQ-206 |
| OQ-B08 | Real-time notification delivery or polling. | Notifications specification |
| OQ-B09 | **Resolved 2026-11-27:** static classes are allowed only to hold extension methods (CON-05). | — |

## 16. Change history

| Date | Version | Change |
|---|---|---|
| 2026-11-27 | 0.1.0 | First baseline from maintainer decisions in session (.NET 10; PostgreSQL 18 with EF Core 10 migrations; Clean Architecture; ASP.NET Core Identity; `/api/health/*` routes; extension-method exception CON-05), the maintainer's coding standards, ADR-001, SPEC-001 and the approved Product Requirements. Pending maintainer review. |
| 2026-11-27 | 1.0.0 | Approved by the maintainer after review of PR #35. No content change from the reviewed draft. Open questions OQ-B01 … OQ-B08 move to the specifications named in Section 15. |
