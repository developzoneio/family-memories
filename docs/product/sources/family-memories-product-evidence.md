# Family Memories — Product decision evidence export

**Export date:** 2026-11-27 (Asia/Ho_Chi_Minh)  
**Purpose:** Evidence for GitHub issue #2 — DES-001 / DOC-01 / GAP-08; input to `docs/product/requirements.md`. This is not the requirements document or a new design.

## Access limitation and source inventory

**Coverage is incomplete.** I could not enumerate or reopen the complete Project chat archive. I searched the accessible Project file index across product, membership, privacy, UI/UX, backend, frontend, technical design, SDD, roadmap, and deployment topics, and listed Project files including generated artifacts. Only `Establish SDD Specification.txt` was returned. I inspected that complete file (88 lines), also present as the uploaded Project attachment. No other Project files were returned. The historical conversations below are represented by visible maintainer-message excerpts, not complete transcripts. Their exact visible wording is quoted, but could not be independently checked against the original chat threads. No external research or GitHub repository content was used; the requested scope is Project evidence.

| Source key | Conversation title or file | Approximate date | Coverage |
|---|---|---|---|
| P | Phỏng vấn ý tưởng ứng dụng gia đình (Family application idea interview) | 2026-10-30 | Visible maintainer excerpts: feature selections, lettered choices, later product and technical selections. Individual follow-up timestamps unavailable. |
| U | Frontend Design | 2026-11-10 | Visible maintainer excerpts: web mockup request, mobile browser clarification, mockup approval and request for technology recommendations. No assistant mockup or recommendation accessible. |
| B | Backend Design | 2026-11-10 | Visible maintainer excerpt requesting consolidation of two earlier backend sessions. Consolidated design and assistant response unavailable. |
| R | Create GitHub Repository | 2026-11-11 | Visible maintainer excerpt requesting guidance to create a repository for source code and documents. |
| S | Establish SDD Specification (file: `Establish SDD Specification.txt`) | 2026-11-11 (date in draft) | Complete accessible assistant-authored SDD response, lines 1–88; not the complete chat, not the linked specification or ZIP. |
| E | Current product-evidence export request (this conversation) | 2026-11-27 | Direct maintainer instruction establishing the Azure change; other “already known” statements are verification leads rather than independent historical proof. |

**Referenced but unreadable:** `Đề xuất Backend Design`, `Cập nhật Backend Design` (mentioned in B; dates unavailable); the detailed Technical Design Document requested in P; original product interview answer choices and preceding problem statement; actual desktop/mobile mockups and Frontend Design assistant response; original SDD conversation beyond S; the SDD starter ZIP, full SPEC-001 Markdown and review checklist linked in S; original ADR-001 and any other Project conversations not surfaced. No claim that all Project history has been searched successfully is made.

**Classification conventions:**

- **Confirmed:** explicit maintainer statement or acceptance visible in the accessible excerpts (or current explicit instruction for Azure). Original historical chat verification is still outstanding. A visible verbatim excerpt is distinguished from an assistant's recap; no recap alone establishes confirmation.
- **Proposal:** accessible assistant suggestion, including an assistant recap where the maintainer's original acceptance cannot be quoted. A confirmed high-level choice does not approve its implementation details.
- **Superseded:** earlier choice replaced by a later explicit maintainer decision. The deployment change is established by the current instruction, not by an independently inspected ADR.
- **Conflicting:** incompatible statements with no known resolution. None identified in the accessible sources; inaccessible history may contain conflicts.
- **Not found:** no supporting historical evidence in accessible materials. This does not prove the topic was never discussed elsewhere in the Project. Unverified leads from the current request are identified as such, not treated as historical confirmations or assistant proposals.

Source cells contain source key, title and date. Quotes remain in their original language (Vietnamese or English); translations and limitations are in Notes. A dash means no qualifying quotation or source. A quoted lettered option proves only that the letter was selected, not its missing meaning. Draft SDD deferrals are not permanent non-goals or proof of approved milestone sequencing.

## A. Vision and problem

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-A01 | Family-focused photo sharing | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Đăng ảnh hằng ngày giống Facebook.” / “Xem dòng thời gian hoạt động của gia đình.” | Maintainer selected daily photo posting and a family activity timeline. The private family scope is separately evidenced in E01. |
| PRD-A02 | Web application for desktop/mobile use | Confirmed | U — Frontend Design, 2026-11-10 | “create the mock UI/UX for web application” / “create the mock UI/UX for mobile web responsive view (I mean user will open the web app in mobile brower, not create the native app).” | Web and mobile-browser responsive views explicitly requested. Desktop web is covered by the general web mockup request; exact desktop device support not specified. |
| PRD-A03 | Purpose/problem statement beyond photo sharing | Not found | — | — | The opening fragment “bài toán:” is visible, but the actual problem statement is not. No verified explanation of the underlying problem, motivation or alternatives. |
| PRD-A04 | Target audience beyond family members | Not found | — | — | Specific age groups, digital literacy, geographic distribution and intended household types unavailable. |
| PRD-A05 | Success criteria and product outcome metrics | Not found | — | — | No adoption, engagement, preservation or usability targets found. |

## B. Users and roles

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-B01 | Family member as a named authorization role | Not found | — | — | Family scope is confirmed, but a formal Member role and its permissions are not evidenced. |
| PRD-B02 | Family owner/admin role | Not found | — | — | No verified role definition, ownership or permission matrix. |
| PRD-B03 | Viewer/read-only role | Not found | — | — | No role definition or restrictions found. |
| PRD-B04 | Child role and restrictions | Not found | — | — | No child-specific account model, permissions or guardian controls found. |
| PRD-B05 | Grandparent/elderly-relative role or persona | Not found | — | — | No role, onboarding policy or persona-specific UI evidence. |
| PRD-B06 | System administrator, moderator, guest or other roles | Not found | — | — | No verified additional role model. |
| PRD-B07 | Who manages members and invitations | Not found | — | — | SDD mentions invitations but does not assign authority. Current brief mentions membership/access management; its historical details cannot be verified. |
| PRD-B08 | Authorization capability | Proposal | S — Establish SDD Specification, 2026-11-11, line 19 | “Authentication and authorization” | Deferred in assistant's draft SPEC-001. No role-level authorization rules or maintainer approval of this draft found. |

## C. Family model

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-C01 | One family versus multiple families per deployment | Not found | — | — | Family visibility does not establish tenancy or deployment cardinality. |
| PRD-C02 | A person belonging to more than one family | Not found | — | — | No membership cardinality decision found. |
| PRD-C03 | Subgroups, branches, households or family tree | Not found | — | — | No subgroup model or access boundaries found. |
| PRD-C04 | Family creation | Proposal | S — Establish SDD Specification, 2026-11-11, line 20 | “Family creation and invitations” | Draft defers this to later specifications. Creation actor, limits and tenant model unspecified. |
| PRD-C05 | Family-model question delegated for recommendation | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 1. Mô hình gia đình và quyền riêng tư => bạn gợi ý giúp tôi” | Maintainer asked for a suggestion on family model and privacy. This is evidence of the question, not acceptance of a particular model. Assistant's recommendation unavailable. |

## D. Membership and onboarding

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-D01 | Invitations | Proposal | S — Establish SDD Specification, 2026-11-11, line 20 | “Family creation and invitations” | Invitation capability appears in assistant draft; no explicit maintainer acceptance or protocol found. |
| PRD-D02 | Invitation method: email, link or code | Not found | — | — | No delivery channel, expiration, single-use or redemption decision. |
| PRD-D03 | Account creation and registration eligibility | Not found | — | — | No sign-up flow, invite-only policy or account creation details. |
| PRD-D04 | Authentication capability | Proposal | S — Establish SDD Specification, 2026-11-11, line 19 | “Authentication and authorization” | Draft capability deferred beyond foundation. |
| PRD-D05 | Sign-in method and account recovery | Not found | — | — | No password, social login, OTP, passkey, MFA or recovery decision found. |
| PRD-D06 | Removing members / leaving a family | Not found | — | — | No actor, revocation or offboarding behavior found. |
| PRD-D07 | Content ownership and handling after member departure | Not found | — | — | No retention, transfer, deletion or attribution decision. |
| PRD-D08 | Membership-management screens and workflows | Not found | — | — | Current request lists membership/access management as known; historical acceptance or workflow could not be verified. |

## E. Privacy and access model

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-E01 | Family-scoped content visibility | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “B. Phạm vi hiển thị: family” | Explicit choice of family visibility; S line 26 also recaps family-private content. No more detailed access matrix follows from this. |
| PRD-E02 | Selection of sharing/access-control option C (meaning unknown) | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 3. Cách thức chia sẻ và kiểm soát quyền truy cập => C” | Option text unavailable; cannot infer whether it concerns invitations, public links or other permissions. |
| PRD-E03 | Per-album visibility | Not found | — | — | No album-specific privacy controls found. |
| PRD-E04 | Per-post/photo visibility or member-level restrictions | Not found | — | — | No granular access rules found. |
| PRD-E05 | External sharing with non-family members / public links | Not found | — | — | Family visibility is confirmed, but whether exceptions, share links or external downloads are permitted is not specified. Option C cannot be decoded. |
| PRD-E06 | Data residency, country or Azure region | Not found | — | — | Azure target does not establish residency or region. |
| PRD-E07 | Encryption at rest and in transit | Not found | — | — | No encryption policy, key management or transport security requirements found. |
| PRD-E08 | User/content deletion, soft deletion and retention | Not found | — | — | No lifecycle, retention period or restoration rules found. |
| PRD-E09 | Backups and disaster recovery | Not found | — | — | No backup cadence, retention, recovery time or recovery point targets found. |
| PRD-E10 | Privacy of metadata, logs and auditing | Not found | — | — | No explicit policy found. |

## F. Capabilities

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-F01 | Daily photo posting | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Đăng ảnh hằng ngày giống Facebook.” | Daily posting like Facebook selected; no required daily frequency, post schema or Facebook feature parity implied. |
| PRD-F02 | Manual upload | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “C. Upload: manual” | Manual upload explicitly selected; no details on batching, background retry or sources. |
| PRD-F03 | Both original and optimized image renditions | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30; S — Establish SDD Specification, 2026-11-11, line 26 | P: “A. Chất lượng ảnh: both” / S: “support for original and optimized images” | Maintainer explicitly chose both image-quality options; S clarifies the pair as original and optimized. Original option definitions not accessible; exact processing rules remain unverified. |
| PRD-F04 | Photo processing | Proposal | S — Establish SDD Specification, 2026-11-11, line 21 | “Photo upload and processing” | Draft later-spec scope. Processing implementation not approved by the rendition choice alone. |
| PRD-F05 | Family activity timeline | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Xem dòng thời gian hoạt động của gia đình.” | View family activity timeline. Sort order, grouping, filtering and pagination unspecified. |
| PRD-F06 | Albums organized by events | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Tạo album ảnh theo sự kiện (sinh nhật, tốt nghiệp, du lịch...).” | Create albums by event, with birthdays, graduations and travel as examples. Separate Event entity not established. |
| PRD-F07 | Original-photo download to phone | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Tải ảnh gốc về điện thoại.” | Download original images to a phone. Bulk download and permission mechanics not specified. |
| PRD-F08 | Family creation and invitation capabilities | Proposal | S — Establish SDD Specification, 2026-11-11, line 20 | “Family creation and invitations” | Draft deferral; see C04 and D01. |
| PRD-F09 | Authentication and authorization capabilities | Proposal | S — Establish SDD Specification, 2026-11-11, line 19 | “Authentication and authorization” | Draft deferral; see B08 and D04. |
| PRD-F10 | Formal posts entity, captions, editing and deletion | Not found | — | — | Daily photo posting is confirmed (F01), not a particular Posts entity or CRUD contract. Current request's “posts” lead has no accessible historical text using that term. |
| PRD-F11 | Comments | Not found | — | — | Neither inclusion nor exclusion established. Facebook analogy does not imply comments. |
| PRD-F12 | Reactions / likes | Not found | — | — | Neither inclusion nor exclusion established. |
| PRD-F13 | Tagging people | Not found | — | — | Neither inclusion nor exclusion established. |
| PRD-F14 | Search, filtering and discovery | Not found | — | — | No search scope or indexing requirements. |
| PRD-F15 | Notifications | Not found | — | — | No in-app, email, push or notification preference decision. |
| PRD-F16 | Video upload/playback | Not found | — | — | Confirmed features concern photos; no explicit video inclusion or exclusion. |
| PRD-F17 | Face recognition or automated person identification | Not found | — | — | No decision found. |
| PRD-F18 | EXIF, capture dates and geolocation | Not found | — | — | No metadata extraction, preservation, removal or location display policy. |
| PRD-F19 | Slideshows | Not found | — | — | No decision found. |
| PRD-F20 | Printing or photo books | Not found | — | — | No decision found. |
| PRD-F21 | Allowed formats, MIME types and codecs | Not found | — | — | JPEG, PNG, HEIC, WebP and video formats not specified in accessible evidence. |
| PRD-F22 | File-size, resolution, count and upload batch limits | Not found | — | — | No numerical limits found. |
| PRD-F23 | Optimized rendition sizes, compression and quality | Not found | — | — | Original/optimized choice confirmed at high level only. No dimensions, quality factors or thumbnail variants found. |
| PRD-F24 | Album management: edit, delete, order, move, cover photo | Not found | — | — | Album creation confirmed; other operations unspecified. |
| PRD-F25 | Duplicate detection, moderation and reporting | Not found | — | — | No decision found. |
| PRD-F26 | Automatic camera-roll synchronization/import | Not found | — | — | Manual upload selected; no explicit permanent exclusion or future sync policy found. |
| PRD-F27 | Membership and access management | Not found | — | — | Current brief lists this as a known later capability; invitations and authorization appear in S, but historical evidence for management functionality itself is unavailable. |

## G. Explicitly out of scope / non-goals

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-G01 | Native mobile application excluded from current design | Confirmed | U — Frontend Design, 2026-11-10 | “I mean user will open the web app in mobile brower, not create the native app” | Mobile browser responsive web, not native application. No assertion about a future native app. |
| PRD-G02 | Complete application excluded from draft SPEC-001 scope | Proposal | S — Establish SDD Specification, 2026-11-11, line 15 | “The proposed first increment establishes a working foundation for Family Memories, not the complete application.” | Assistant explicitly labeled this first increment proposed. Not a permanent product non-goal. |
| PRD-G03 | Authentication, family creation/invitations, photo upload/processing, timeline/albums, full UI and production deployment deferred from SPEC-001 | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–24 | “Deferred to later specifications” | Draft scope table. These are milestone deferrals rather than product exclusions; later sequence is not specified. |
| PRD-G04 | Other permanent feature exclusions | Not found | — | — | No verified exclusions for video, social features, automated upload, public sharing, printing or other capabilities. Do not convert silence into non-goals. |

## H. Non-functional expectations and technical constraints

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-H01 | Medium-scale system | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Quy mô: medium” | Explicit scale category. S line 26 recaps it; original category definition unavailable. |
| PRD-H02 | Numerical scale: users, families, concurrency, photos and storage | Not found | — | — | No numeric definition of medium, expected growth, storage volume or workload distribution found. |
| PRD-H03 | React frontend | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Frontend: react” | Explicit choice. No React version, component framework, build system or TypeScript decision verified. |
| PRD-H04 | Responsive mobile-browser web UI | Confirmed | U — Frontend Design, 2026-11-10 | “create the mock UI/UX for mobile web responsive view (I mean user will open the web app in mobile brower, not create the native app).” | Responsive mobile web requested and subsequent mockup accepted. No device matrix or breakpoints verified. |
| PRD-H05 | Specific supported browsers, OS versions and device classes | Not found | — | — | No browser version, minimum viewport, tablet policy or support matrix found. |
| PRD-H06 | Performance targets | Not found | — | — | No response-time, upload-time, page-load or rendering targets found. |
| PRD-H07 | UI language(s) and localization | Not found | — | — | Vietnamese and English occur in conversations, but conversation language does not establish UI language. No locale or translation requirements found. |
| PRD-H08 | Accessibility and elderly-friendly usability targets | Not found | — | — | No WCAG level, font-size, contrast, touch-target or assistive technology policy found. |
| PRD-H09 | Storage/cost option A selected (meaning unknown) | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 4. Lưu trữ hình ảnh và chi phí vận hành => A” | Confirms a choice was made; missing option text prevents recovery of cost/storage policy. |
| PRD-H10 | Cost budget, limits, storage quota and operating-cost expectations | Not found | — | — | No monetary amounts, currency, billing ceilings, storage quotas or cost SLA found. Option A does not establish these without its text. |
| PRD-H11 | Home self-hosting as deployment target | Superseded | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30; E — Current product-evidence export request, 2026-11-27 | P: “Deployment: home” / E: “Known later change: on 2026-11-27 the deployment target changed from home self-hosting to Microsoft Azure (ADR-001).” | Replaced by Microsoft Azure on 2026-11-27. S line 26 still reflects the old self-hosting assumption; historical only. |
| PRD-H12 | Microsoft Azure as deployment target | Confirmed | E — Current product-evidence export request, 2026-11-27 | “Known later change: on 2026-11-27 the deployment target changed from home self-hosting to Microsoft Azure (ADR-001).” | Current maintainer instruction explicitly states change; original ADR-001 not available. No Azure service selections or region verified. |
| PRD-H13 | .NET backend foundation | Proposal | S — Establish SDD Specification, 2026-11-11, line 20 | “.NET backend foundation” | Assistant draft scope; full Backend Design unavailable, no maintainer quote accepting the backend stack found. |
| PRD-H14 | Database engine and version | Not found | — | — | S line 86 flags database engine for reconciliation; no actual engine choice available. |
| PRD-H15 | Availability, reliability, recovery and monitoring targets | Not found | — | — | Draft health checks/testing/CI are not quantitative production service objectives. |
| PRD-H16 | Mobile-experience option D selected (meaning unknown) | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 5. Trải nghiệm sử dụng trên điện thoại => D” | Original option D text unavailable. Later U explicitly clarifies mobile-browser web, but the content of option D is not recoverable. |
| PRD-H17 | Health checks, tests and CI for foundation | Proposal | S — Establish SDD Specification, 2026-11-11, line 24 | “Health checks, tests, and CI” | Draft engineering scope. No CI provider, coverage target or specific health criteria confirmed. |

## I. UI/UX evidence

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-I01 | Web application mockup requested | Confirmed | U — Frontend Design, 2026-11-10 | “create the mock UI/UX for web application” | Confirms the design request, not the unseen visual content. |
| PRD-I02 | Mobile responsive mockup requested | Confirmed | U — Frontend Design, 2026-11-10 | “create the mock UI/UX for mobile web responsive view (I mean user will open the web app in mobile brower, not create the native app).” | Confirms responsive-browser design intent. |
| PRD-I03 | Mockup approval | Confirmed | U — Frontend Design, 2026-11-10 | “tôi duyệt thiết kế mockup của bạn.” | Translation: I approve your mockup design. Approval is explicit; the approved image, exact version and whether one or both variants were covered cannot be independently established. |
| PRD-I04 | Visual style: palette, typography, spacing, icons, layout | Not found | — | — | No actual mockup or descriptive design specification accessible. Do not recreate or infer from approval. |
| PRD-I05 | App shell navigation labels: Timeline, Albums, Family | Not found | — | — | Listed as a lead in E. Timeline and album capabilities are independently confirmed (F05–F06), but actual navigation labels and the Family tab could not be historically verified. |
| PRD-I06 | Key screen designs: feed, album, family management, posts, invitation, sign-in, upload | Not found | — | — | Functional features and SDD mentions do not prove the screen inventory, layouts, components or interactions. |
| PRD-I07 | Mockup file, image, URL, Figma document or repository path | Not found | — | — | Only conversation title and approval available; Project file search returned no mockup. Do not invent a path or link. |
| PRD-I08 | Request for frontend implementation recommendations after mockup approval | Confirmed | U — Frontend Design, 2026-11-10 | “bạn hãy đề xuất cho tôi cách triển khai frontend như công nghệ, thư viện, etc ...” | Request for technology/library proposals. It does not approve particular libraries; recommendations unavailable. |

## J. Milestones and roadmap

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-J01 | Milestone 1 requested, with architecture explanation before coding | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Hãy lập Technical Design Document chi tiết và bắt đầu hướng dẫn Milestone 1 theo từng bước, giải thích kiến trúc trước khi code.” | Maintainer requested a detailed TDD and step-by-step guidance. Does not itself confirm exact Milestone 1 boundaries. |
| PRD-J02 | Milestone 1 named Project Foundation & Development Environment (SPEC-001) | Proposal | S — Establish SDD Specification, 2026-11-11, lines 7–15 | “SPEC-001: Project Foundation & Development Environment” | Draft v0.1, explicitly not approved in accessible SDD response (line 86). |
| PRD-J03 | Foundation scope: repository, backend/frontend foundation, DB connectivity/migrations, local dev, health checks, tests and CI | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–24 | “Included in SPEC-001” | Scope table as proposed, not accepted. The six included rows are transcribed in the item description. |
| PRD-J04 | Authentication and authorization after foundation | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–19 | “Authentication and authorization” | Listed in deferred column; no milestone number or priority assigned. |
| PRD-J05 | Family creation and invitations after foundation | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–20 | “Family creation and invitations” | Deferred; exact sequence unknown. |
| PRD-J06 | Photo upload and processing after foundation | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–21 | “Photo upload and processing” | Deferred; exact sequence unknown. |
| PRD-J07 | Timeline and albums after foundation | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–22 | “Timeline and albums” | Deferred; exact sequence unknown. |
| PRD-J08 | Production deployment after foundation | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–23 | “Production deployment” | Deferred in historical draft; any production-deployment design must distinguish the later Azure decision. |
| PRD-J09 | Full application UI after foundation | Proposal | S — Establish SDD Specification, 2026-11-11, lines 17–24 | “Full application UI” | Deferred; not a permanent non-goal. |
| PRD-J10 | SDD process: Specify → Clarify → Plan → Tasks → Implement & Verify | Proposal | S — Establish SDD Specification, 2026-11-11, lines 28–48 | “We should approve that specification before generating its technical plan or writing application code.” | Proposed workflow; actual approval and execution not evidenced. |
| PRD-J11 | SDD specification and starter artifacts | Proposal | S — Establish SDD Specification, 2026-11-11, lines 48–72 | “The immediate deliverable is `specs/001-project-foundation/spec.md`.” | The response references `family-memories-sdd-starter.zip`, `SPEC-001-project-foundation.md` and `family-memories-sdd/specs/001-project-foundation/checklists/requirements.md`. These names are evidenced; their contents/availability and repository commit are not. Claimed counts (5 user stories, 14 functional requirements, 6 nonfunctional requirements, 11 acceptance tests) could not be checked. |
| PRD-J12 | Ordered, numbered roadmap after Milestone 1 | Not found | — | — | S lists deferred work, not an ordered roadmap. Do not assign Milestone 2, 3, etc. from table row order. |
| PRD-J13 | GitHub repository for source code and documentation | Confirmed | R — Create GitHub Repository, 2026-11-11 | “I want to create the github repo to store the source code and document, please guide me.” | Confirms repository intent, not creation, URL, ownership or commit status. |
| PRD-J14 | Consolidation of prior backend designs requested | Confirmed | B — Backend Design, 2026-11-10 | “Dựa vào chat session "Đề xuất Backend Design" và "Cập nhật Backend Design" bạn hãy cung cấp phiên bản tổng hợp đầy đủ ở chat session này.” | Maintainer requested complete consolidated version. None of the three backend design responses were accessible. |
| PRD-J15 | Milestone completion, draft approval, deadlines and implementation status | Not found | — | — | S says SPEC-001 was draft on 2026-11-11; no subsequent approval, milestone completion or dated schedule found. |

## K. Open questions and unresolved evidence

These rows distinguish documented open/reconciliation questions from missing information. A missing answer is not proof that the maintainer never made a decision.

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-K01 | Family model and privacy recommendation | Confirmed | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 1. Mô hình gia đình và quyền riêng tư => bạn gợi ý giúp tôi” | Recommendation was requested; family-scoped visibility later selected, but tenancy, cardinality and detailed privacy rules remain unverified. See C and E. |
| PRD-K02 | Meaning of sharing/access-control option C | Not found | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 3. Cách thức chia sẻ và kiểm soát quyền truy cập => C” | Selection found, option definition not found. See E02. |
| PRD-K03 | Meaning of storage/cost option A | Not found | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 4. Lưu trữ hình ảnh và chi phí vận hành => A” | Selection found, option definition not found. See H09. |
| PRD-K04 | Meaning of mobile-experience option D | Not found | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30 | “Câu 5. Trải nghiệm sử dụng trên điện thoại => D” | Selection found, option definition not found. Mobile browser requirement separately confirmed. See H16. |
| PRD-K05 | Precise Milestone 1 boundaries for reconciliation | Proposal | S — Establish SDD Specification, 2026-11-11, line 86 | “the precise Milestone 1 boundaries” | Assistant explicitly flags reconciliation with earlier Backend Design. No resolution available. |
| PRD-K06 | .NET version, database engine, local environment, CI provider | Proposal | S — Establish SDD Specification, 2026-11-11, line 86 | “.NET version, database engine, supported local environment, and CI provider.” | Assistant identifies technical questions requiring reconciliation; no chosen values accessible. |
| PRD-K07 | Approval of SPEC-001 before planning | Proposal | S — Establish SDD Specification, 2026-11-11, lines 86–88 | “The specification is currently **Draft**, not approved.” | S describes draft state at that time and recommends approval. Subsequent maintainer approval not found. |
| PRD-K08 | Frontend implementation library choices | Not found | U — Frontend Design, 2026-11-10 | “bạn hãy đề xuất cho tôi cách triển khai frontend như công nghệ, thư viện, etc ...” | Request documented; assistant's library proposals and any acceptance unavailable. See I08. |
| PRD-K09 | Backend design reconciliation or conflicts | Not found | B — Backend Design, 2026-11-10 | “phiên bản tổng hợp đầy đủ” | Consolidation request is visible; underlying versions are inaccessible, so actual changes and conflicts cannot be identified. |
| PRD-K10 | Numerical definition of medium scale | Not found | — | — | High-level category selected, numbers missing. See H01–H02. |
| PRD-K11 | Azure ADR details and impact on earlier specifications | Not found | — | — | Current target confirmed; original ADR, migration scope, service choices and any amended SDD documents unavailable. See H11–H12. |

## Targeted questions

| # | Question | Status | Answer / source |
|---|---|---|---|
| 1 | One family or many families per deployment? | Not found | No tenant/deployment cardinality decision. P (2026-10-30) confirms family visibility: “B. Phạm vi hiển thị: family”, but that does not answer deployment cardinality. See C01. |
| 2 | Which roles exist and what can each do? | Not found | No role list or permissions matrix. S (2026-11-11, line 19) proposes “Authentication and authorization”, without role definitions. See B01–B08. |
| 3 | How does a new member join? | Proposal | Invitations are mentioned in S — Establish SDD Specification (2026-11-11, line 20): “Family creation and invitations”. No approved join method, invitation type or registration flow found. See D01–D05. |
| 4 | Photos only, or video too? | Not found | The photos-versus-video scope boundary is not established. P (2026-10-30) confirms photo posting: “Đăng ảnh hằng ngày giống Facebook.” Photos are confirmed; whether video is supported or explicitly excluded is unknown. See F01 and F16. |
| 5 | Comments, reactions or tagging: in scope or not? | Not found | No inclusion or exclusion evidence for any of the three features. The Facebook analogy does not establish parity. See F11–F13. |
| 6 | UI language(s)? | Not found | No UI language or localization decision found. See H07. |
| 7 | Concrete numbers behind medium scale? | Not found | P (2026-10-30): “Quy mô: medium” confirms category only. No numeric user, concurrency, photo or storage targets found. See H01–H02. |
| 8 | Any decision about sharing content with people outside the family? | Not found | P (2026-10-30): “B. Phạm vi hiển thị: family” confirms family scope. The earlier choice “Câu 3. Cách thức chia sẻ và kiểm soát quyền truy cập => C” is also recorded, but the option is unavailable. No explicit rule authorizing or prohibiting external/public links found. See E01–E05. |

## Superseded and conflicting decisions

| ID | Item | Status | Source (conversation title, date) | Verbatim quote | Notes |
|---|---|---|---|---|---|
| PRD-H11 | Home self-hosting | Superseded | P — Phỏng vấn ý tưởng ứng dụng gia đình, 2026-10-30; E — Current product-evidence export request, 2026-11-27 | P: “Deployment: home” / E: “Known later change: on 2026-11-27 the deployment target changed from home self-hosting to Microsoft Azure (ADR-001).” | Azure replaces old deployment target. S (2026-11-11, line 26) also repeats the old assumption: “self-hosted deployment”. Treat the older statements as historical, not current requirements. |
| PRD-H12 | Microsoft Azure | Confirmed | E — Current product-evidence export request, 2026-11-27 | “Known later change: on 2026-11-27 the deployment target changed from home self-hosting to Microsoft Azure (ADR-001).” | The change is explicitly supplied by the maintainer; original ADR unavailable. |

**Conflicting decisions:** None identified in the accessible evidence. The home-to-Azure change is a resolved supersession, not an unresolved conflict. The missing backend versions and earlier conversations prevent an exhaustive conflict audit.

## Not found / never discussed

The following topics have status **Not found** in the accessible evidence. This heading is not a claim that they were never discussed in the complete Project. For item-level statuses, sources (where applicable), and distinctions between missing information and draft proposals, refer to the IDs below.

| Topic | Evidence IDs | Missing information |
|---|---|---|
| Vision, audience and success | A03–A05 | Original problem, audience personas, measurable outcomes. |
| Roles and permissions | B01–B07 | Owner/admin, member, viewer, child, grandparent, system admin, other roles, management authority and permissions. |
| Family tenancy | C01–C03 | One/many families, multi-family membership, family branches and subgroups. |
| Onboarding and membership management | D02–D03, D05–D08, F27 | Invitation protocol, account registration, sign-in, recovery, removal, content after leaving, management screens. |
| Privacy and governance | E03–E10 | Per-album/per-post rules, external sharing, public links, residency, encryption, deletion/retention, backups, metadata/logs. |
| Social, media and additional features | F10–F20, F24–F26 | Posts schema/CRUD, comments, reactions, tagging, search, notifications, video, face recognition, EXIF/location, slideshows, printing, album management, duplicates/moderation, automatic upload policy. |
| Media constraints | F21–F23 | Allowed formats, file sizes, counts, resolution, processing profiles and compression. |
| Permanent non-goals | G04 | Any explicit feature exclusions other than the confirmed current native-app exclusion. |
| Numerical and operational expectations | H02, H05–H08, H10, H14–H15 | Scale numbers, browsers/devices, performance, languages, accessibility, costs, database engine, availability and recovery. |
| Approved design details | I04–I07 | Appearance, navigation labels, screens, actual mockup files/images/links. |
| Roadmap and progress | J12, J15 | Actual ordering/numbering of later milestones, deadlines, approvals and progress. |
| Missing decision definitions and source artifacts | K02–K04, K08–K11 | Interview option C/A/D text, frontend/backend design outcomes, numerical scale definition and ADR-001 details. |

## Evidence-use notes

- Use the confirmed choices as the recoverable maintainer statements, subject to the excerpt-access limitation. Do not upgrade a Proposal solely because it appears in an assistant recap or draft.
- Keep current Azure deployment separate from historical home-hosting assumptions. The original ADR remains an outstanding source to retrieve.
- For the next evidence pass, the highest-value missing sources are the complete product interview (including option definitions), both original backend design sessions and their consolidation, the Technical Design Document, the approved UI mockup images and frontend response, and the original ADR-001/SDD documents. This identifies evidence gaps only; it introduces no design decisions.
- No real family member names, email addresses, photographs or other family-member personal data are included.
