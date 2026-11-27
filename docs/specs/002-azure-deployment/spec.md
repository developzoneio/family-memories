# SPEC-002 — Azure Deployment

> **Project:** Family Memories  
> **Milestone:** 2 — Azure deployment (proposed; follows SPEC-001)  
> **Status:** **Draft — not approved**  
> **Version:** 0.1.1  
> **Created:** 2026-11-27  
> **Specification owner:** Project maintainer  
> **Decision basis:** [ADR-001](../../adr/ADR-001-azure-deployment-target.md)

## 1. Intent

Run the Family Memories foundation from SPEC-001 on Microsoft Azure, so the application is reachable over HTTPS from
desktop and mobile browsers, with secrets kept out of the repository and a documented, repeatable way to provision,
deploy, check and recover the environment.

This specification defines observable outcomes. Exact SKUs, region, names and settings belong in a SPEC-002 `plan.md`
and the Azure Portal runbook.

## 2. Context

- **Decided (ADR-001, 2026-11-27):** Azure is the production target and replaces home self-hosting. Resources are
  created manually in the Azure Portal by following a runbook in this repository.
- **Selected hosting direction (ADR-001):** Azure Static Web Apps (Standard) for the React frontend; Azure App Service on
  Linux for the ASP.NET Core API, linked to the static web app under `/api`; Azure Database for PostgreSQL Flexible
  Server; Azure Key Vault for secrets.
- **Depends on SPEC-001:** a working frontend, API with `/api/health/live` and `/api/health/ready`, baseline migration and CI.
  Nothing can be deployed until SPEC-001 is implemented.

## 3. User stories (prioritized)

### US-201 — Provision the environment from a runbook (P1)

As the maintainer, I want a step-by-step Azure Portal runbook so I can create, or re-create, the environment without
relying on memory.

1. **Given** an Azure subscription and the runbook, **when** I follow it in order, **then** every required resource
   exists with the documented settings, and no step needs a value that is only in someone's head.
2. **Given** the environment exists, **when** I compare it with the runbook's settings checklist, **then** any
   difference can be detected.

### US-202 — Deploy a version of the application (P1)

As the maintainer, I want a documented way to deploy a specific commit of the frontend and API and apply database
migrations, so I know exactly what is running.

1. **Given** a commit that passed CI, **when** I follow the documented deployment procedure, **then** the frontend and
   API for that commit are served from Azure.
2. **Given** a deployment with a new migration, **when** I apply migrations using the documented procedure, **then** the
   schema is upgraded explicitly, never by destructive startup initialization.
3. **Given** a deployment fails, **when** I follow the rollback steps, **then** the previous version is restored.

### US-203 — Reach the application securely (P1)

As a family member, I want to open the application over HTTPS from my phone or computer.

1. **Given** the deployed environment, **when** I open the documented URL, **then** the shell loads over HTTPS and
   HTTP requests are redirected or refused.
2. **Given** the deployed environment, **when** I call the liveness and readiness endpoints at their documented Azure
   addresses, **then** they behave as in SPEC-001 FR-003 to FR-005 (route mapping: OQ-209, resolved).

### US-204 — Keep secrets and data safe (P1)

As the maintainer, I want secrets held in Azure and database access restricted.

1. **Given** the repository, **when** I review tracked files, **then** no Azure connection string, key, password or
   publish profile is present.
2. **Given** the API configuration in Azure, **when** I inspect app settings, **then** secrets are Key Vault
   references, not literal values.
3. **Given** the database server, **when** I review its network access, **then** it is not open to all internet
   addresses.

### US-205 — Observe, back up and control cost (P2)

As the maintainer, I want to know when the app is down, be able to restore the database, and avoid surprise bills.

1. **Given** the readiness endpoint fails, **when** monitoring runs, **then** I am alerted.
2. **Given** the database backup policy, **when** I follow the documented restore drill, **then** a point-in-time copy
   is restored to a separate server.
3. **Given** a monthly budget, **when** spending reaches the alert threshold, **then** I receive a notification.

## 4. Functional requirements

| ID | Requirement | Story |
|---|---|---|
| FR-201 | The repository MUST contain an Azure Portal runbook listing every resource, its required settings, and creation order. | US-201 |
| FR-202 | The runbook MUST include a settings checklist that can be used to audit an existing environment for drift. | US-201 |
| FR-203 | Deployment of the frontend and API MUST be documented and traceable to a specific Git commit. | US-202 |
| FR-204 | Database migrations in Azure MUST be applied by an explicit, documented step. | US-202 |
| FR-205 | A rollback procedure for the API, frontend and schema changes MUST be documented. | US-202 |
| FR-206 | The application MUST be served only over HTTPS. | US-203 |
| FR-207 | SPEC-001 liveness and readiness MUST be checkable in Azure with unchanged semantics, and the frontend's optional status check MUST work through the Static Web Apps origin. | US-203 |
| FR-208 | Runtime secrets MUST be stored in Azure Key Vault and read by the API through a managed identity. | US-204 |
| FR-209 | The database MUST NOT accept connections from all internet addresses. | US-204 |
| FR-210 | Readiness failures MUST raise an alert to the maintainer. | US-205 |
| FR-211 | Database backup retention and a restore procedure MUST be documented and tested once. | US-205 |
| FR-212 | A subscription or resource-group budget with an alert MUST be configured. | US-205 |

## 5. Nonfunctional and security requirements

| ID | Requirement |
|---|---|
| NFR-201 | **No real family data before authentication:** no real family photos or personal data may be stored in Azure until an approved authentication/authorization specification is implemented and deployed. |
| NFR-202 | **No secrets in Git:** connection strings, keys, passwords and publish profiles never enter source control, CI logs or screenshots. |
| NFR-203 | **Least privilege:** the API identity has only the roles it needs (for example read access to Key Vault secrets). |
| NFR-204 | **Data residency:** the Azure region is chosen and recorded explicitly. |
| NFR-205 | **Reproducibility:** someone other than the original author can recreate the environment from the runbook. |
| NFR-206 | **Local development unaffected:** SPEC-001 local workflow keeps working without an Azure account. |

## 6. Boundary and non-goals

**Included:** one Azure environment, Portal runbook, deployment and rollback procedure, HTTPS, Key Vault secrets,
database network restriction, health alerting, backup/restore drill, budget alert.

**Excluded:** authentication and family membership (own spec), photo upload and Azure Blob Storage (media spec),
infrastructure as code, multiple environments (staging), custom domain (unless decided in OQ-203), and migration of
real family data.

## 7. Acceptance tests

| Test ID | Evidence required | Covers |
|---|---|---|
| AT-201 | A second person, or the maintainer in a fresh resource group, follows the runbook and creates a working environment | FR-201, NFR-205 |
| AT-202 | The settings checklist is run against the live environment and finds no drift | FR-202 |
| AT-203 | A known commit is deployed; the running version is identifiable as that commit | FR-203 |
| AT-204 | The migration step runs twice against Azure; the second run is a no-op | FR-204 |
| AT-205 | Rollback to the previous version is performed once and the app works | FR-205 |
| AT-206 | HTTP access is redirected or refused; HTTPS works | FR-206 |
| AT-207 | Liveness and readiness return SPEC-001 results at their documented Azure addresses; stopping the database gives 503 on ready; the shell's status check works through the SWA origin | FR-207 |
| AT-208 | App settings show Key Vault references; repository and CI logs contain no secrets | FR-208, NFR-202 |
| AT-209 | A connection attempt from an unlisted address to the database fails | FR-209 |
| AT-210 | Forcing a readiness failure produces an alert | FR-210 |
| AT-211 | A point-in-time restore to a separate server succeeds | FR-211 |
| AT-212 | The budget and alert threshold are visible in Cost Management | FR-212 |

## 8. Open questions

| ID | Question | Owner |
|---|---|---|
| OQ-201 | Which Azure region? (data residency, latency for family members, cost) | Maintainer |
| OQ-202 | Which tiers/SKUs for App Service plan and PostgreSQL Flexible Server, and what monthly budget? | Maintainer |
| OQ-203 | Default `*.azurestaticapps.net` URL or a custom domain? | Maintainer |
| OQ-204 | How is code deployed: GitHub Actions deployment, Portal Deployment Center, or manual upload? (Resources are provisioned manually either way; relates to SPEC-001 OQ-005.) | Maintainer |
| OQ-205 | Database network access: firewall rules for App Service outbound addresses, or private access through a virtual network? | Plan |
| OQ-206 | How are migrations run against Azure: from a CI job, from the maintainer's machine through a temporary firewall rule, or a migration bundle? | Plan |
| OQ-207 | Monitoring: App Service health check and Azure Monitor alerts, Application Insights, or both? | Plan |
| OQ-209 | **Resolved 2026-11-27 (issue #3):** option (b). SPEC-001 v1.2.0 moves the health routes to `/api/health/live` and `/api/health/ready`; all API routes live under `/api`, and the App Service health check probes `/api/health/live`. Original question: SPEC-001 FR-003/FR-004 fix the health routes at `/health/live` and `/health/ready`, but Static Web Apps forwards only `/api/*` to a linked App Service and passes the full path unchanged. Options: (a) the API also serves `/api/health/*`; (b) amend SPEC-001 so all API routes, including health, live under `/api`; (c) probe health on the App Service directly and use `/api` only for the frontend status check. Decide **before SPEC-001 is implemented**, because it changes an approved contract. | Maintainer |
| OQ-208 | Static Web Apps limits a linked-backend request to 45 seconds. How will future large photo uploads avoid it (for example direct upload to Blob Storage)? Record for the media spec. | Plan / media spec |

## 9. Dependencies

- SPEC-001 implemented and verified (AT-001 to AT-011).
- ADR-001 accepted (done 2026-11-27).
- An authentication/authorization specification is approved before any real family data is deployed (NFR-201).

## 10. Change control

This is a draft. It does not authorize creating Azure resources or spending money. Approval changes `Status` to
**Approved** with date and reviewer, and is followed by a SPEC-002 `plan.md` and the Portal runbook.
