# Family Memories — Product Requirements Baseline

> **Document ID:** DES-001  
> **Version:** 1.0.0  
> **Status:** **Approved v1.0.0** — project maintainer, 2026-11-27 (stated in session; confirmed by merging
> PR [#34](https://github.com/developzoneio/family-memories/pull/34))  
> **Created:** 2026-11-27  
> **Owner:** Project maintainer  
> **Tracking:** GitHub issue [#2](https://github.com/developzoneio/family-memories/issues/2) (DES-001, DOC-01, GAP-08)

## 1. Purpose and how to read this document

This document is the canonical product baseline for Family Memories: what the product is, who uses it, how privacy
works, which capabilities it has, what is out of scope, and the milestone outline. Numbered specifications under
`docs/specs/` turn these statements into testable requirements; this document does not authorize implementation.

Every statement carries one label:

| Label | Meaning |
|---|---|
| **Confirmed** | Backed by a source in Section 2: an explicit maintainer statement in an earlier conversation, or an approved or accepted repository document. |
| **Proposal** | Suggested by an assistant or by a draft document, and not explicitly accepted by the maintainer. Repeating it does not make it Confirmed. |
| **Open** | No decision found. Tracked in Section 12. Silence is not treated as a decision, in either direction. |
| **Superseded** | Decided once and later replaced. Kept in Section 13 for history only. |

A Confirmed high-level choice does not approve implementation details below it. Where only a high-level choice is
known, the details are listed as Open.

## 2. Sources

| Key | Source | Date | Notes |
|---|---|---|---|
| P | Earlier ChatGPT conversation *Phỏng vấn ý tưởng ứng dụng gia đình* (family application idea interview) | 2026-10-30 | Maintainer answers to the product interview. Several answers are option letters whose option text was not recovered (see OQ-P06 … OQ-P08). |
| U | Earlier ChatGPT conversation *Frontend Design* | 2026-11-10 | Maintainer requests for web and mobile-browser mockups, and the mockup approval. The mockup itself was not recovered. |
| S | Earlier ChatGPT conversation *Establish SDD Specification* | 2026-11-11 | Assistant-authored draft of SPEC-001. Supports **Proposal** labels only. |
| SPEC-001 | [SPEC-001 Project Foundation](../specs/001-project-foundation/spec.md) | Approved v1.1.0, 2026-11-27 | Approved by the maintainer (PR #19 merge). |
| ADR-001 | [ADR-001 Azure deployment target](../adr/ADR-001-azure-deployment-target.md) | Accepted, 2026-11-27 | Maintainer decision. |
| SPEC-002 | [SPEC-002 Azure Deployment](../specs/002-azure-deployment/spec.md) | Draft v0.1.0 | Not approved. Supports **Proposal** labels only. |
| PLAN-001 | [SPEC-001 technical plan](../specs/001-project-foundation/plan.md) | Draft v0.1 | Not approved. Supports **Proposal** labels only. |
| M | Maintainer decisions in the Claude Code session that drafted this document | 2026-11-27 | Answers to OQ-P02 … OQ-P06, OQ-P09 … OQ-P14 and OQ-P17, chosen from offered options. The option wording is quoted in the rows that cite M. |
| EV | [Product-evidence export](sources/family-memories-product-evidence.md) | 2026-11-27 | ChatGPT export with verbatim quotes for P, U and S. Evidence IDs such as PRD-F02 refer to this file. |

**Source limitation.** Sources P, U and S were recovered through the product-evidence export (EV), produced by
ChatGPT on 2026-11-27. ChatGPT reported that it could not reopen the complete
conversation archive: it worked from visible maintainer excerpts and one SDD file, and could not read the original
Backend Design sessions, the Technical Design Document, the interview option texts or the mockup images. Items marked
Confirmed from P or U therefore rest on quoted excerpts, and the maintainer's review of this document is what ratifies
them. The maintainer approved this baseline as v1.0.0 on 2026-11-27. Quotes below keep their original language.

## 3. Product vision

| ID | Statement | Label | Source |
|---|---|---|---|
| VIS-01 | Family Memories is a **private family photo-sharing web application**. | Confirmed | SPEC-001 §2; P: "B. Phạm vi hiển thị: family" |
| VIS-02 | Family members post photos day to day, in the spirit of a social feed ("Đăng ảnh hằng ngày giống Facebook" — post photos daily, like Facebook). The analogy does not imply Facebook feature parity. | Confirmed | P |
| VIS-03 | Family members follow a timeline of family activity, organize photos into albums by event, and can download original photos. Details are in Section 7. | Confirmed | P; SPEC-001 §2 |
| VIS-04 | The product is used in web browsers on computers and phones; it is not a native mobile app. | Confirmed | U; SPEC-001 §2 |
| VIS-05 | The underlying problem statement, target audience and success criteria. | Open | OQ-P01 |

## 4. Users and roles

| ID | Statement | Label | Source |
|---|---|---|---|
| USR-01 | Users are **members of a family**, and content is visible only within the family. | Confirmed | P: "B. Phạm vi hiển thị: family"; SPEC-001 §2 |
| USR-02 | The product has **membership and access management** as a later capability. | Confirmed | SPEC-001 §2 |
| USR-03 | Users must be authenticated, and access must be authorized, before the application handles real family data. Each application endpoint requires a dedicated authentication/authorization specification. | Confirmed | SPEC-001 §6; ADR-001 (Consequences) |
| USR-04 | There are two roles. **Admin** manages members, invitations and family settings. **Member** posts, views, creates albums and downloads. | Confirmed | M (OQ-P03: "Admin + Member") |
| USR-05 | An Admin can also do everything a Member can. The family has at least one Admin at all times. | Proposal | This document; follows from USR-04 |
| USR-06 | Finer-grained roles (for example a read-only viewer, a child role or a single owner above Admins) are not part of the first role model. They can be added later by a new decision. | Confirmed | M (OQ-P03; the Viewer and Owner options were not chosen) |
| USR-07 | How many Admins a family may have, how a Member becomes an Admin, and how the first Admin is created. | Open | OQ-P03 |

## 5. Family model and membership

| ID | Statement | Label | Source |
|---|---|---|---|
| FAM-01 | **One deployment serves exactly one family.** Multi-family hosting (multi-tenant) is not planned; it would need a new decision and its own specification. Because there is only one family, a person cannot belong to several families. | Confirmed | M (OQ-P02: "One family"). The earlier request for a recommendation (P: "Câu 1. Mô hình gia đình và quyền riêng tư => bạn gợi ý giúp tôi") is answered by this decision. |
| FAM-02 | The single family is set up once, when the deployment is initialized, together with its first Admin. There is no user-facing "create a family" feature. | Proposal | This document; follows from FAM-01 (S and SPEC-001 §8 mention "family creation") |
| FAM-03 | New members join through an **invite link or code** that an Admin generates and sends through any channel (for example Zalo or Messenger). The link **expires** and the Admin can **revoke** it. | Confirmed | M (OQ-P04: "Admin shares an invite link"); S and SPEC-001 §8 name invitations |
| FAM-04 | There is no open self-registration: an account can only be created through a valid invite link. | Proposal | This document; follows from FAM-03 |
| FAM-05 | Whether an invite link is single-use, how long it stays valid, the sign-in method, and account recovery. | Open | OQ-P04 |
| FAM-06 | Sub-groups within the family, such as households or branches. | Open | OQ-P02 |
| FAM-07 | When a member is removed or leaves, their account **loses access**, but the posts and photos they uploaded **stay** in the family's timeline and albums, still attributed to them. | Confirmed | M (OQ-P05: "Content stays") |
| FAM-08 | Whether a departed member's content can still be deleted later, and by whom (for example on the member's request or by an Admin). | Open | OQ-P05 |

## 6. Privacy and access model

| ID | Statement | Label | Source |
|---|---|---|---|
| PRV-01 | Content visibility is **family-scoped**: content is visible to the members of the family (the single family of the deployment, FAM-01) and to no one else by default. | Confirmed | P: "B. Phạm vi hiển thị: family"; SPEC-001 §2; M (OQ-P02) |
| PRV-02 | **No real family data** may be deployed to Azure until an authentication and authorization specification is approved and implemented. | Confirmed | ADR-001 (Consequences); SPEC-002 §9 |
| PRV-03 | No real family member accounts, private photos or secrets appear in source control, test fixtures, screenshots or logs. | Confirmed | SPEC-001 NFR-001 |
| PRV-04 | Because photos are stored in a public cloud, the privacy model must cover the **Azure region (data residency), encryption, access control, and who can administer the Azure subscription**. The specific answers are Open. | Confirmed (the need) / Open (the answers) | ADR-001 (Consequences); SPEC-002 OQ-201; OQ-P15 |
| PRV-05 | Content is **never shared outside the family**: there are no public links, guest links or guest accounts. Anyone who needs to see content must be invited as a member (FAM-03). This decision replaces whatever interview option C ("Câu 3. Cách thức chia sẻ và kiểm soát quyền truy cập => C") said; that option's text was not recovered. | Confirmed | M (OQ-P06: "Never, family only"); P |
| PRV-06 | Visibility finer than the family (per album, per post or per member). | Open | OQ-P06 |
| PRV-07 | Deletion and retention of content and accounts, backups and recovery expectations, and privacy of photo metadata such as location. | Open | OQ-P15 |

## 7. Capabilities

| ID | Capability | Label | Source | Details still Open |
|---|---|---|---|---|
| CAP-01 | **Manual photo upload** by family members. Accepted formats: **JPEG, PNG and HEIC** (iPhone photos). Maximum **25 MB per photo**. | Confirmed | P: "C. Upload: manual"; SPEC-001 §2; M (OQ-P12: "JPEG, PNG, HEIC; 25 MB") | Batch size and retry behavior (OQ-P12). |
| CAP-02 | Each photo is kept as an **original**, exactly as uploaded (including HEIC), and an **optimized rendition** in a format that browsers can display. | Confirmed | P: "A. Chất lượng ảnh: both"; SPEC-001 §2; M (OQ-P12) | Rendition sizes, output format, compression and thumbnails (OQ-P12). |
| CAP-03 | **Photo posts**: members post photos day to day, like a social feed. | Confirmed | P: "Đăng ảnh hằng ngày giống Facebook." | Whether a post has a caption, can hold several photos, and can be edited or deleted. |
| CAP-04 | **Family activity timeline** ("Xem dòng thời gian hoạt động của gia đình" — view the family activity timeline). | Confirmed | P; SPEC-001 §2 | Ordering, grouping, filtering and paging. |
| CAP-05 | **Albums by event** ("Tạo album ảnh theo sự kiện (sinh nhật, tốt nghiệp, du lịch...)" — create albums by event: birthdays, graduations, travel). | Confirmed | P; SPEC-001 §2 ("albums/events") | Editing, deleting, ordering, cover photo; whether an event is separate from an album. |
| CAP-06 | **Download original photos**, including to a phone ("Tải ảnh gốc về điện thoại"). | Confirmed | P; SPEC-001 §2 | Bulk download; who may download. |
| CAP-07 | **Membership and access management**, with the Admin and Member roles. | Confirmed | SPEC-001 §2; M (OQ-P03) | Admin count and promotion (USR-07); removal (FAM-07). |
| CAP-08 | **Authentication and authorization.** | Confirmed (required) | SPEC-001 §6; ADR-001 | Sign-in method and recovery (OQ-P04). |
| CAP-09 | **Invite links**: an Admin generates, sends and revokes expiring invite links. | Confirmed | M (OQ-P04) | Single use and validity period (FAM-05). |
| CAP-10 | **Photos only** in the first media specification. Video is a possible later capability, not a permanent non-goal. | Confirmed | M (OQ-P09: "Photos only now") | When, or whether, video is added. |
| CAP-11 | **Comments**: members can comment on a photo post. | Confirmed | M (OQ-P10) | Editing and deleting comments, and whether an Admin can remove them. |
| CAP-12 | **Reactions**: members can react to a photo post. | Confirmed | M (OQ-P10) | A single "like" or a small set of emoji. |
| CAP-13 | **Notifications** about new posts, comments and reactions, in-app first. | Confirmed | M (OQ-P11) | Email or push channels; member preferences. |
| CAP-14 | **Search and filter** photos by date, album or uploader. | Confirmed | M (OQ-P11) | Search scope and result ordering. |
| CAP-15 | Face recognition; printing or photo books; duplicate detection and moderation; automatic camera-roll sync. | Open | — | Not asked yet; neither included nor excluded (OQ-P11). |

## 8. Out of scope

| ID | Statement | Label | Source |
|---|---|---|---|
| OUT-01 | A **native mobile app** is not part of the product; phones use the web application in a mobile browser. This records the current design; no decision was found about a native app in the far future. | Confirmed | U: "I mean user will open the web app in mobile brower, not create the native app"; SPEC-001 §2 |
| OUT-02 | **Home self-hosting** is no longer a deployment target. | Confirmed | ADR-001 (see Section 13) |
| OUT-03 | The exclusions in SPEC-001 §8 and SPEC-002 §6 bound **those increments only**. Several excluded items are Confirmed later capabilities (for example uploads, albums and notifications); external sharing is now a product non-goal (OUT-07). | Confirmed | SPEC-001 §2, §8, §13; SPEC-002 §6 |
| OUT-04 | **Hosting several families in one deployment** is out of scope (FAM-01). | Confirmed | M (OQ-P02) |
| OUT-05 | **Tagging people** in photos or posts is out of scope for now. It was not chosen with comments and reactions, and can be revisited by a new decision. | Confirmed | M (OQ-P10) |
| OUT-06 | **Reading capture date and location from photo metadata** to sort or display photos, and **slideshows**, are out of scope for now. They were offered with notifications and search and not chosen; they can be revisited by a new decision. | Confirmed | M (OQ-P11) |
| OUT-07 | **Sharing outside the family** (public links, guest links, guest accounts) is a product non-goal (PRV-05). | Confirmed | M (OQ-P06) |
| OUT-08 | Any other permanent product exclusion. None was recorded; features without a decision stay Open (CAP-15) rather than out of scope. Video is deferred, not excluded (CAP-10). | Open | — |

## 9. Quality expectations and constraints

| ID | Statement | Label | Source |
|---|---|---|---|
| QLT-01 | The system is sized for **medium scale** ("Quy mô: medium"), defined as **up to 50 members** in the one family and **about 10,000 photos a year**, with few members online at the same time. | Confirmed | P; SPEC-001 §2; M (OQ-P13: "Up to 50 members, ~10k photos/yr") |
| QLT-01a | At typical phone photo sizes this is roughly **40–60 GB of originals a year**, plus the optimized renditions. This is a planning estimate, not a measured figure. | Proposal | This document; derived from QLT-01 |
| QLT-02 | The frontend is built with **React** ("Frontend: react"). | Confirmed | P; SPEC-001 §2 |
| QLT-03 | The UI is **responsive** and usable in desktop and mobile browsers. For the foundation shell this is tested at 360 and 1280 CSS px. | Confirmed | U; SPEC-001 NFR-003 |
| QLT-04 | Production runs on **Microsoft Azure**: Static Web Apps (frontend), App Service on Linux (API), Azure Database for PostgreSQL Flexible Server, Key Vault (secrets), provisioned manually in the Portal. | Confirmed | ADR-001 |
| QLT-05 | Azure has a recurring monthly cost, so a budget and cost alerts are needed. The interview answer on storage and operating cost was option A ("Câu 4. Lưu trữ hình ảnh và chi phí vận hành => A"), whose text was not recovered. | Confirmed (the need) / Open (budget, option A) | ADR-001 (Consequences); P; OQ-P07 |
| QLT-06 | Large original-photo uploads will probably need direct-to-storage upload (for example Azure Blob Storage), because requests proxied through Static Web Apps are limited to 45 seconds. To be decided in a media specification. | Proposal | ADR-001 (Consequences) |
| QLT-07 | The backend is built with ASP.NET Core/.NET. | Proposal | SPEC-001 §2 ("working proposal"); S |
| QLT-08 | The UI is in **Vietnamese** at launch. All UI text is kept in translation resources so that English (or another language) can be added later without code changes. | Confirmed | M (OQ-P14: "Vietnamese first, i18n-ready") |
| QLT-09 | Supported browsers and devices, performance targets and accessibility (including for older relatives). | Open | OQ-P14 |

## 10. UI/UX baseline

| ID | Statement | Label | Source |
|---|---|---|---|
| UX-01 | Mockups for the web application and for the mobile-browser responsive view were requested and **approved by the maintainer** on 2026-11-10 ("tôi duyệt thiết kế mockup của bạn" — I approve your mockup design). | Confirmed | U |
| UX-02 | The approved mockup is not stored in this repository, and its location (file, image or link) is unknown. Its visual style must not be recreated from memory. | Open | Register DES-005, GAP-10; OQ-P16 |
| UX-03 | The interview answer on the phone experience was option D ("Câu 5. Trải nghiệm sử dụng trên điện thoại => D"), whose text was not recovered. | Open | P; OQ-P08 |
| UX-04 | The main navigation has **Timeline**, **Albums** and **Family** sections. | Proposal | SPEC-001 §10 (shell *may* show these placeholders); PLAN-001 |

## 11. Milestone outline

| ID | Milestone | Label | Source |
|---|---|---|---|
| MS-01 | **Milestone 1 — Project Foundation** (SPEC-001): reproducible local development, health checks, baseline database, responsive shell, tests and CI. No product features and no real family data. | Confirmed | SPEC-001 (approved v1.1.0) |
| MS-02 | **Milestone 2 — Azure Deployment** (SPEC-002): one Azure environment, runbook, HTTPS, secrets, alerts, backup drill, budget alert. Follows SPEC-001; no real family data. | Proposal | SPEC-002 (draft v0.1.0) |
| MS-03 | Each later user-facing capability (authentication, albums, uploads and so on) gets its **own numbered specification**. | Confirmed | SPEC-001 §13 |
| MS-04 | Authentication and family membership must come before any real family data is deployed. | Confirmed | ADR-001; SPEC-002 §9 |
| MS-05 | Order after Milestone 2: **M3** authentication, family and invite links; **M4** photo upload and renditions, including the storage design; **M5** photo posts and timeline, with comments and reactions; **M6** event albums; **M7** original-photo download. Real family data can be used from M4 onward, once M3 is in place (PRV-02). Each milestone still needs its own approved specification (MS-03). | Confirmed | M (OQ-P17: "Auth → Upload → Timeline → Albums → Download"); S (deferred list) |
| MS-06 | Where notifications (CAP-13), search and filter (CAP-14) and a possible video capability (CAP-10) fit after M7 or inside M5–M7. | Open | OQ-P17 |

## 12. Open questions

| ID | Question | Related |
|---|---|---|
| OQ-P01 | What problem does the product solve, for whom, and how is success measured? | VIS-05 |
| OQ-P02 | **Partly resolved 2026-11-27:** one deployment serves one family (FAM-01). Still open: are there sub-groups such as households or branches? | FAM-01, FAM-06 |
| OQ-P03 | **Partly resolved 2026-11-27:** roles are Admin and Member (USR-04). Still open: how many Admins, how a Member becomes an Admin, and how the first Admin is created. | USR-04 … USR-07 |
| OQ-P04 | **Partly resolved 2026-11-27:** members join through an Admin-generated, expiring, revocable invite link (FAM-03). Still open: is the link single-use, how long is it valid, which sign-in method is used, and how is an account recovered? | FAM-03 … FAM-05 |
| OQ-P05 | **Partly resolved 2026-11-27:** a departed member's content stays, attributed to them (FAM-07). Still open: can that content be deleted later, and by whom? | FAM-07, FAM-08 |
| OQ-P06 | **Partly resolved 2026-11-27:** no sharing outside the family (PRV-05). Still open: is visibility finer than the family needed (per album, per post)? The text of interview option C is only of historical interest now. | PRV-05, PRV-06 |
| OQ-P07 | What did interview option A (photo storage and operating cost) say? What is the monthly budget? | QLT-05 |
| OQ-P08 | What did interview option D (phone experience) say? | UX-03 |
| OQ-P09 | **Resolved 2026-11-27:** photos only in the first media specification; video possibly later (CAP-10). | CAP-10 |
| OQ-P10 | **Resolved 2026-11-27:** comments and reactions are in scope (CAP-11, CAP-12); tagging people is out of scope for now (OUT-05). | CAP-11, CAP-12, OUT-05 |
| OQ-P11 | **Partly resolved 2026-11-27:** notifications and search are in scope (CAP-13, CAP-14); photo date/location metadata and slideshows are out for now (OUT-06). Still open: face recognition, printing, duplicate detection, camera-roll sync. | CAP-13 … CAP-15, OUT-06 |
| OQ-P12 | **Partly resolved 2026-11-27:** JPEG, PNG and HEIC, up to 25 MB per photo (CAP-01). Still open: how many photos per upload, and which rendition sizes and output format are produced? | CAP-01, CAP-02 |
| OQ-P13 | **Resolved 2026-11-27:** up to 50 members and about 10,000 photos a year (QLT-01). | QLT-01, QLT-01a |
| OQ-P14 | **Partly resolved 2026-11-27:** Vietnamese UI at launch, ready for translation (QLT-08). Still open: which browsers and devices are supported, and what accessibility level is required? | QLT-08, QLT-09 |
| OQ-P15 | Which Azure region holds the data? What are the rules for encryption, deletion, retention, backups and metadata privacy? Who administers the Azure subscription? | PRV-04, PRV-07; SPEC-002 OQ-201 |
| OQ-P16 | Where is the approved mockup, and can it be added to the repository? | UX-02; DES-005 |
| OQ-P17 | **Partly resolved 2026-11-27:** M3 auth → M4 upload → M5 timeline → M6 albums → M7 download (MS-05). Still open: where notifications, search and video fit. | MS-05, MS-06 |

## 13. Superseded decisions

| Decision | Replaced by | Source |
|---|---|---|
| Production is self-hosted at home ("Deployment: home"). | Microsoft Azure, 2026-11-27. | P; ADR-001 |

## 14. Change history

| Date | Version | Change |
|---|---|---|
| 2026-11-27 | 0.1.0 | First baseline, drafted from the 2026-11-27 product-evidence export (EV: sources P, U, S, committed under `sources/`) and the approved or accepted repository documents. Includes maintainer decisions M on OQ-P02 (one family per deployment), OQ-P03 (Admin and Member roles), OQ-P04 (invite links) and OQ-P09 (photos only for now). Pending maintainer review. |
| 2026-11-27 | 0.1.0 | Second round of maintainer decisions M, before review: OQ-P05 (a departed member's content stays), OQ-P10 (comments and reactions in scope, tagging out for now), OQ-P12 (JPEG, PNG, HEIC up to 25 MB) and OQ-P14 (Vietnamese UI, translation-ready). Version unchanged because 0.1.0 has not been reviewed yet. |
| 2026-11-27 | 0.1.0 | Third round of maintainer decisions M, before review: OQ-P06 (no sharing outside the family), OQ-P11 (notifications and search in; photo date/location metadata and slideshows out for now), OQ-P13 (up to 50 members, about 10,000 photos a year) and OQ-P17 (milestones M3 auth → M4 upload → M5 timeline → M6 albums → M7 download). |
| 2026-11-27 | 1.0.0 | Approved by the maintainer after review of PR #34. No content change from the reviewed draft. Open questions remain open and move to the specifications of the milestones they affect. |
