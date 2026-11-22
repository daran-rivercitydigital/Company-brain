# Architecture: Technology Stack Requirements

> **Source:** RCD Technology Stack Requirements v1.1 (updated 20 November 2026), including Appendix A  
> **Compiled:** 2026-11-23 | **Owner:** Founder | **Status:** Extracted implementation architecture  
> **Business authority:** [Master Business Architecture](../playbooks/rcd-master-business-architecture.md)  
> **Controls:** [Privacy, Security and AI Controls](../nz-compliance/privacy-security-ai-controls.md)

This article extracts the technology needed to run RCD and to deliver customer application and AI services. It does not replace the master business architecture. If the two conflict, the master governs the required outcome and the technology article governs the implementation choice.

RCD runs two connected stacks:

* A lean Microsoft-first business operating stack.
* A portable engineering and delivery stack controlled through GitHub, specifications, tests and CI/CD.

Customer solutions may use Power Automate, n8n or code according to workload evidence. No orchestration vendor is the product. Customer-isolated deployments, deterministic processing, human approval and metadata-first observability take precedence over multi-tenancy or autonomous AI operation.

## 1. Business operating stack

| Capability | Platform | Status |
| --- | --- | --- |
| Productivity, email, calendar, Teams and tenant identity | Microsoft 365, RCD-owned | Required |
| Identity and access | Microsoft Entra ID capabilities: MFA, least privilege, time-limited privileged access, logging, immediate removal | Required control |
| Controlled documents and WFM evidence | SharePoint and OneDrive | Required |
| Customer-facing documents | Word, PowerPoint and PDF | Required |
| Deterministic WFM, pricing and margin models | Excel initially | Required |
| WFM survey | Microsoft Forms or equivalent Microsoft capability | Required for WFM |
| WFM orchestration | Power Automate | Required for WFM |
| CRM and customer truth | Attio | Required |
| Scheduling and booking caps | Cal.com or equivalent | Planned |
| Demand generation | Website, tracked links and a newsletter platform | Product still open |
| Contracting | Word and PDF templates plus e-signature | Capability required; product open |
| Accounting, GST, invoicing | NZ-capable cloud accounting platform | Open; select with an NZ accountant |
| Banking | Operating, GST and Reserve accounts | Open; provider not selected |
| Commercial ledger | Excel initially: founder labour at $125/hour, three cost layers, discounts, credits and margin gates | Required |
| Incident records | Proportionate ticketing; product not selected | Capability required |
| Endpoint security | Managed, encrypted devices for Confidential or Restricted access | Control required; product not named |

Keep three records separate and reconcilable: Attio for customer truth, Excel for pricing and management truth, and the accounting platform for statutory truth. GitHub is also part of business operations because it is the record for reusable IP and controlled change.

Use controlled Microsoft 365 storage as the initial evidence repository for access reviews, test evidence, approvals, incidents, risks, deployments and restoration evidence. Compliance evidence is generally retained for three years.

Do not place customer data in public consumer AI services.

## 2. Engineering control plane

| Component | Role | Status |
| --- | --- | --- |
| GitHub | System of record for code, configuration, schemas, specifications, tests, prompts, evaluations, deployment definitions and runbooks | Agreed |
| GitHub Actions or equivalent | Automated checks, retained evidence, controlled promotion, runner isolation, protected secrets and rollback | Agreed direction |
| Specifications and ADRs | Markdown specifications, acceptance criteria, decision records and review evidence | Required practice |
| Automated testing | Unit, integration, regression, security and acceptance tests. Failed tests or AI evaluations block promotion | Required |
| Configuration as code | Repeatable deployment and drift control, with daily and post-change detection | Agreed |
| Package governance | Approved sources, version pinning where appropriate, dependency and container scanning | Required |
| Replit | Bounded PoV prototyping and demonstrations. Not the authoritative repository | Provisional |

Promotion pattern for workbench-built code: RCD-controlled GitHub branch, development workspace, lint and security checks, pull request, human review, then an approved demonstration or production environment. Workspace checkpoints do not replace Git commits or retained CI evidence.

A development workspace may not approve its own production promotion. Development runtime and production runtime are separate decisions.

## 3. Execution targets

| Technology | Best-fit use | Decision |
| --- | --- | --- |
| Power Automate | Minimum sellable WFM and Microsoft-heavy customer workflows | Agreed for WFM |
| Python | Deterministic rules, calculations, integrations and test harnesses | Agreed direction |
| TypeScript / JavaScript | API services and workflow extensions, after Python foundations | Agreed direction |
| Docker / containers | Repeatable packaging and isolated deployment | Agreed direction |
| n8n | Heterogeneous, API-heavy or AI-heavy workflows | Provisional; evaluate in a suitable paid PoV, not on the WFM launch path |
| Azure Functions or Container Apps, or equivalent | Customer-isolated bounded services | Provisional target class, chosen per implementation |
| Vercel | Stateless bounded frontend and API functions | Provisional candidate; evidence-triggered |
| Supabase | PostgreSQL and Auth for customer PoV and production-candidate apps | Provisional candidate; evidence-triggered |

Vercel and Supabase are candidates alongside Power Automate, Azure Functions or Container Apps, and customer-owned runtimes. They are selected per workload. The source Appendix A still asks the founder to record formal approval of that candidate status as technology-stack v1.2. Until that approval is logged, treat both as proposals under test, not as a production standard.

Not approved for these candidates: Restricted data, production credentials in PoV workspaces, shared multi-tenancy, or production standardisation without a suitable paid PoV. Supabase for automated commercial telemetry remains Parked.

### 3.1 Candidate runtime gate

Record the outcome before a candidate runtime processes customer data or is retained after a PoV:

| Gate | Criterion |
| --- | --- |
| Cloud and region | Hosting region and data location recorded and acceptable to the customer |
| Customer isolation | Isolated project or runtime. Cross-tenant read, write, delete, insert, join, RPC and service-role tests pass. Service-role credentials are privileged bypass paths |
| Identity and access | MFA, least privilege, time-bounded privileged access and access logging. Workload identity or an approved secrets manager |
| Data and retention | 15-minute payload-purge target and 24-hour quarantine rule proven. Platform logs, APM and analytics assessed as separate destinations. No payload logging |
| Subprocessor | Data-processing assessment and customer approval recorded |
| Backup and recovery | Backup or point-in-time recovery for the service tier. RPO no more than 24 hours and RTO no more than 1 business day, demonstrated in two restoration exercises. Rollback proven |
| Supply chain | Dependency, container and infrastructure-as-code scanning. Zero Critical and zero High findings unless a recorded founder exception exists |
| Operations | Monitoring, support ownership and runbooks. Long-running replay, purge and scheduled jobs placed on a suitable runtime |
| Economics | Cost per customer envelope supports the margin gate |
| Portability and exit | A fresh clone runs from documented configuration. A migration path to Azure or a customer-owned runtime is documented |

No final cloud region is selected. NZ onshore residency is not a company-wide hosting standard in this source. When a customer requires New Zealand or Australia data residency, record that requirement on the client page before any non-Microsoft runtime is used. Microsoft 365 remains the approved store for WFM evidence.

## 4. AI services and assisted engineering

| Capability | Position | Status |
| --- | --- | --- |
| Model and provider | Selectable. Keep a version-controlled inventory and avoid single-provider dependence | Provider still open |
| Cursor | Replaceable, human-directed coding workbench | Provisional |
| Claude Code | Bounded repository implementation, testing and documentation | Provisional |
| Replit Agent | Human-directed and human-accepted only | Provisional |
| Future AI workforce platform | No autonomous production authority | Parked |
| Prompt and evaluation management | Version-controlled prompts, baselines and regression evidence | Required |

Required AI controls: approved data-processing terms, scoped context, prompt-injection testing, constrained tool allow-lists, and an impact evaluation before a material model, provider or prompt change reaches production. AI may draft or explain. Code or rules calculate. A designated human approves. Founder approval remains until it is formally delegated.

Validate any AI provider, Cursor, Claude Code, n8n, cloud runtime or connector before it processes Confidential or Restricted customer data.

## 5. Replit PoV controls

Replit may accelerate prototyping and demonstrations. It is not the default production runtime and not an automatic destination for customer data.

Permitted initially: synthetic-data PoVs, UI and workflow prototypes, mock APIs, demonstration applications, internal sandboxes, scaffolding, test generation and non-sensitive technical feasibility.

Customer Confidential data needs an engagement-specific approval after contractual processing terms, data location, workspace access, private preview, retention and deletion, AI model handling, secrets and audit requirements have been validated for the selected plan.

Not approved initially: Restricted information, production credentials, live accounting or client-ledger data, unredacted WFM evidence, customer production databases, autonomous production deployment, or business-critical production workloads.

Operating rules:

* Use an RCD-owned workspace, not a personal account. Require MFA, limit collaborators, and remove access at engagement closure.
* Private development URLs by default. Disable public publishing. Password protection alone is not equivalent to identity-controlled access.
* Never hard-code credentials. Use PoV-specific least-privileged secrets, separate from production, and revoke or rotate them at closure.
* Review packages introduced by the agent. Acceptance threshold: zero Critical findings, and zero High findings unless a founder-approved non-production exception with compensating controls exists. Medium findings need a remediation plan before production.
* Record plan, data-hosting location, subprocessors, model providers, retention behaviour, export capability and customer approval before Confidential data is introduced.
* A short-lived Replit deployment may demonstrate non-production work on synthetic or specifically approved de-identified data, with restricted access, no production credentials and a documented shutdown date.
* At Proceed / Revise / Stop, decide whether to retain Replit, migrate, revise controls, or stop.

## 6. Runtime, data and operations

* Deploy one reusable codebase into isolated customer runtimes. Keep customer differences in external configuration and keep secrets separate. Customer-owned deployment remains available.
* Do not build a shared multi-tenant runtime before repeated demand, at least 70% reuse, at least 30% comparable delivery-hour reduction, and at least two of Customers 1–3 buying substantially the same pattern.
* Use explicit REST or HTTP, JSON, webhook and schema contracts, with validation, authentication, error handling and versioning.
* Keep credentials outside code and workflow definitions. Select a dedicated secrets product when production requirements trigger it.
* Financial calculations, mappings, materiality, scoring and business rules execute in code or rules.
* Use bounded retries with exponential back-off, idempotency, quarantine, investigation and authorised replay.
* Delete processing payloads within a 15-minute target. Delete retry and quarantine payloads within 24 hours unless an exception is documented. Keep operational metadata online for 12 months. Delete WFM raw evidence no later than 30 days after completion.
* Log health, status, timing, identifiers and exception metadata without retaining customer payloads by default.
* Release path: build, automated test, pre-production validation, founder approval, controlled deployment, health checks and rollback.
* Continuity backup after every production release, integrity verification, six-monthly restoration tests, and an extra test after a material change.
* Internal targets until proven twice: RPO no more than 24 hours and RTO no more than 1 business day.
* Automated monitoring may be continuous. Human response is not represented as 24x7.
* Attribute licences, model and API use, infrastructure, partner support, monitoring and founder intervention to the customer service envelope.

## 7. Minimum sellable WFM path

| Stage | Technology | Control |
| --- | --- | --- |
| Collect | Microsoft Forms | Adaptive survey. Identifiable evidence available only to RCD |
| Orchestrate | Power Automate | Administration, evidence movement, first-pass preparation, approval tasks and draft artefacts |
| Store | SharePoint and OneDrive | Access-controlled evidence in the RCD Microsoft 365 environment |
| Model | Excel | Deterministic materiality, workload, capacity, Value x Feasibility and pricing |
| Assist | Approved AI service | Draft grouping, synthesis, wording, gaps and narrative. Must not invent missing numbers |
| Approve | Founder review | PFR boundaries, recoverability, economic use, materiality, risk, complexity, ranking and recommendations |
| Deliver | PowerPoint and PDF | Executive WFM Report Pack |
| Relationship | Attio | Customer and engagement truth, not the WFM evidence store |
| Reusable assets | GitHub | Versioned schemas, specifications, exportable automation definitions, prompts, tests and runbooks |

Do not add n8n to the WFM launch path.

## 8. Implementation sequence and gaps

1. Establish Microsoft 365 identities, MFA, SharePoint libraries, permissions, retention locations and the managed-device rule.
2. Configure Attio and the Excel commercial ledger. Select the NZ accounting platform and banking provider with the accountant.
3. Create the GitHub control plane: private repositories, branch and review rules, ADR and specification templates, secrets hygiene, backup and baseline CI.
4. Build the minimum sellable WFM and pass a synthetic end-to-end test that preserves every founder approval gate.
5. Implement monitoring, an incident record, a release checklist, backup, a restoration test, vulnerability workflow and the customer-isolated deployment pattern before the first production acceptance.
6. Use the first suitable paid PoV to compare Power Automate, n8n and code. Do not standardise a platform from a learning exercise alone.
7. After Customers 1–3, reassess reuse, effort, margin and managed-service evidence before considering multi-tenancy or a broader workflow runtime.

Still open before operational readiness: accounting platform, banking provider, Microsoft 365 information architecture, managed-device standard, GitHub and CI baseline, WFM assets including the PFR model, proportionate incident and monitoring tools, AI-provider validation, and the exact isolation, secrets, logging, backup and recovery pattern for the first production implementation.

## 9. Decision summary

| State | Items |
| --- | --- |
| Required | Microsoft 365, Forms, Power Automate for WFM, SharePoint and OneDrive, Excel, Word, PowerPoint, PDF, Attio, GitHub, specifications, automated tests, CI/CD, deterministic code, human approval, customer isolation, central evidence store, access governance, monitoring and recovery |
| Agreed direction | Python, TypeScript or JavaScript, containers, GitHub Actions or equivalent, configuration as code, API contracts, approved AI-provider abstraction |
| Provisional | n8n, Replit, Vercel, Supabase for customer apps, Cursor, Claude Code, Azure Functions or Container Apps, Power Platform ALM detail, specific AI providers, dedicated secrets platform, cloud provider and region |
| Open products | NZ accounting platform, banking provider, e-signature, ticketing, newsletter tools, endpoint-security product |
| Parked | True multi-tenant SaaS, full Advisory Flow platform, commercial telemetry into Supabase, permanent AI workforce platform, self-service training platform, dedicated tooling not justified by paid evidence |
