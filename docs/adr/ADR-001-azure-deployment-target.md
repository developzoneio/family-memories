# ADR-001 — Production deployment target: Microsoft Azure (replaces home self-hosting)

> **Status:** Accepted — project maintainer, 2026-11-27 (decision stated in session)  
> **Date:** 2026-11-27  
> **Deciders:** Project maintainer  
> **Supersedes:** "Deployment target: self-hosted at home" in SPEC-001 v1.0.0 §2 and earlier chat-only design context  
> **Affects:** SPEC-001 (§2, §8, FR-014, AT-011), SPEC-002 (new), `plan.md`, Backend Design, Technical Design

## Context

Earlier Family Memories planning set the production target as **self-hosted at home** (SPEC-001 v1.0.0 §2). That
choice shaped several requirements: FR-014 and AT-011 refer to a "home deployment boundary" and NFR-002 forbids
router port forwarding.

The maintainer has decided to deploy to **Microsoft Azure** instead.

**Rationale:** The maintainer has not yet recorded detailed reasons. *Maintainer to add the main reasons (for example
availability, operations effort, cost or remote access) before this ADR is referenced by an approved plan.*

## Decision

1. **Microsoft Azure is the production deployment target.** Home self-hosting is dropped as a target.
2. **Hosting direction (selected by maintainer, detailed in SPEC-002):**

   | Component | Azure service |
   |---|---|
   | React frontend | Azure Static Web Apps (Standard plan, needed to link an App Service backend) |
   | ASP.NET Core API | Azure App Service on Linux, linked to the static web app under `/api` |
   | Database | Azure Database for PostgreSQL — Flexible Server |
   | Secrets | Azure Key Vault, read by App Service through Key Vault references and a managed identity |

3. **Provisioning method:** resources are created **manually in the Azure Portal**, following a runbook kept in this
   repository. Infrastructure as code is not adopted now.
4. **Local development is unchanged.** SPEC-001 still delivers a local-only foundation. Azure provisioning and
   deployment are specified separately in **SPEC-002** and are not part of SPEC-001.

## Consequences

**Positive**

- No home hardware, router configuration or home-network exposure to operate.
- Managed services take over OS patching, database backups and TLS certificates, which home hosting would have
  required the maintainer to run.
- The proposed SPEC-001 stack fits the target: Azure Database for PostgreSQL Flexible Server supports PostgreSQL 17
  (standard support until 2029-11-08), and App Service on Linux offers a .NET 10 (LTS) runtime stack.

**Negative / risks**

- **Public internet exposure.** An Azure-hosted app is reachable from the internet by default. No real family data
  may be deployed until an authentication and authorization specification is approved and implemented.
- **Family photos in a public cloud.** The privacy model must cover the Azure region (data residency), encryption,
  access control and who can administer the subscription.
- **Recurring cost.** The SWA Standard plan, App Service plan and PostgreSQL server cost money every month; a budget
  and cost alerts are needed.
- **Manual provisioning drifts.** Portal-created resources are hard to reproduce or audit. The runbook must record every
  setting that matters, and moving to infrastructure as code should be reconsidered if environments multiply.
- **Request limit through Static Web Apps.** Requests proxied to a linked backend are limited to 45 seconds. Large
  original-photo uploads will probably need a direct-to-storage design (for example Azure Blob Storage) in a later
  media specification.
- **Design sources to re-check.** Exports of the Backend Design and Technical Design (issues #3, #5) were written for
  home hosting and must be reconciled with this ADR.

## Follow-up

- SPEC-001 amended to v1.1.0 (hosting context, FR-014, AT-011, §8 exclusions).
- SPEC-002 *Azure Deployment* created as a draft: `docs/specs/002-azure-deployment/spec.md`.
- Azure Portal runbook: to be written under SPEC-002.

## References

- Azure Database for PostgreSQL version policy:
  https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/concepts-version-policy
- Deploy an ASP.NET web app to App Service: https://learn.microsoft.com/en-us/azure/app-service/quickstart-dotnetcore
- Static Web Apps with an App Service backend: https://learn.microsoft.com/en-us/azure/static-web-apps/apis-app-service
- Key Vault references in App Service: https://learn.microsoft.com/en-us/azure/app-service/app-service-key-vault-references
