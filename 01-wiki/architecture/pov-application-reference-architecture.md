# PoV Application Reference Architecture

> **Document Status:** Controlled Reference Architecture (v1.1) | **Effective Date:** 20 November 2026 | **Owner:** [Founder]  
> **Source:** `PoV_Application_Reference_architecture.pdf`  
> **Governing Documents:** [RCD Master Business Architecture](../playbooks/rcd-master-business-architecture.md) (v8.2) | [RCD Technology Stack Requirements](./tech-stack-requirements.md) (v1.1)  
> **Related Documents:** [Replit PoV Build & Cursor Migration Guide](../playbooks/replit-pov-build-and-cursor-migration.md) | [Privacy, Security and AI Control Baseline](../nz-compliance/privacy-security-ai-controls.md)

---

## 1. Purpose, Scope & Governance

This document converts RCD business and technology controls into a reusable application-engineering standard for Proof-of-Value (PoV) delivery and production candidates derived from them. A project-level `docs/ARCHITECTURE.md` instantiates this reference architecture with workload-specific decisions rather than replacing or overriding it.

| Governance Layer | Purpose | Authority |
| :--- | :--- | :--- |
| **Master Business Architecture (v8.2)** | Business model, customer promise, product boundaries, commercial rules, human authority, and risk position | **Highest** |
| **Technology Stack Requirements (v1.1)** | Approved, Provisional, Open, and Parked technology choices and platform controls | **Second** |
| **PoV Application Reference Architecture (v1.1)** | Reusable application structure, engineering controls, tests, and production-candidate pattern | **Third** |
| **Project `ARCHITECTURE.md`** | Workload-specific connectors, data classes, retention profile, approval policy, deployment target, and recovery design | **Project Implementation** |
| **Cursor Project Rules, Task Specs & Agent Instructions** | Bounded implementation tasks | **No Architectural Authority** |

* **Conflict & Authority Rules:**
  * Where documents conflict, the higher governing layer prevails.
  * An AI coding agent cannot approve a deviation, production promotion, security exception, or customer-data use.
  * Each PoV must record explicit **Adopt**, **Tailor**, or **Not Applicable** treatment for every mandatory control in this document.
  * The Technology Stack Requirements is an extracted document, not a new governing decision; Master Business Architecture prevails over it. Items in this document not named in Technology Stack v1.1 are RCD proposals carrying an explicit decision state until the Technology Stack is updated (see Appendix A).

### Traceability to Technology Stack v1.1

| Reference Architecture Section | Technology Stack v1.1 Section Implemented |
| :--- | :--- |
| 1. Purpose, scope and governance | §1, §5, §8 (source and interpretation note) |
| 2. Architectural principles | §1 executive summary; §3.4 |
| 3. Reference technology pattern | §3.1–3.3, §5 |
| 4. Modular application structure | §3.1, §3.4 |
| 5. Data and tenancy architecture | §3.4 (customer-isolated runtime; true multi-tenancy parked) |
| 6. Job lifecycle, idempotency and replay | §3.4 (integration resilience); §3.5 (exception and replay) |
| 7. Human approval architecture | §3.3 (human decision gates); §3.5 (release management) |
| 8. Payload retention and deletion controls | §3.4 (data minimisation and retention); §2.4 |
| 9. Logging, telemetry and evidence | §3.4 (metadata-first observability); §3.5 (auditability) |
| 10. AI engineering and provider controls | §3.3 |
| 11. Identity, authentication and secrets | §2.1, §2.4, §3.4, §3.6 |
| 12. Software supply chain and CI/CD | §3.1, §2.4 (security assurance) |
| 13. Backup, recovery and rollback | §2.4, §3.5 |
| 14. Candidate platform controls | §3.2, §3.6 |
| 15. Mandatory acceptance tests | §3.1 (automated testing), §3.3 |
| 16. PoV-to-production decision gate | §3.6 (deployment decision); §6 steps 6–7 |
| 17. Managed AI Operations telemetry | §3.5 |
| 18–20. Templates and checklists | §6, §7 |
| 21. Change control | §3.3, §5 |

---

## 2. Architectural Principles

| Principle | Mandatory Interpretation |
| :--- | :--- |
| **Customer-isolated first** | Initial deployments use a reusable RCD codebase in an isolated customer runtime or isolated project. A `tenant_id` / `customer_id` remains present for isolation, traceability, and future evolution; it does not approve shared multi-tenancy. |
| **Spec-first** | Interfaces, schemas, acceptance criteria, data classifications, approval policies, and tests are defined before feature code. |
| **Portable engineering assets** | Code, configuration schemas, tests, prompts, evaluations, ADRs, and runbooks remain exportable and version-controlled in GitHub. |
| **Deterministic core, bounded AI** | Rules, calculations, permissions, and consequential state transitions execute deterministically. AI produces structured, constrained outputs subject to evaluation and human policy. |
| **Ephemeral payloads** | Minimise payload persistence. Normal processing payloads are removed immediately when no longer needed and targeted for deletion **no later than 15 minutes** after completion or expiry; any contractual SLA requires proven operational evidence. |
| **Metadata-first observability** | Operational evidence contains identifiers, state, timing, cost, and sanitised error codes—never raw customer payloads. |
| **Human accountability** | The defined human approval policy governs consequential actions. Development tools and AI agents never approve production promotion. |
| **Evidence-triggered platform evolution** | Shared multi-tenancy, permanent platform standardisation, and autonomous operation require paid evidence and formal governance decisions. For multi-tenancy, the repeatability gate (decided after Customers 1–3) requires: demonstrated repeated demand, **at least 70% reuse**, **at least 30% comparable delivery-hour reduction**, and **at least two of Customers 1–3** buying substantially the same core pattern. |

---

## 3. Reference Technology Pattern

*Production reference, not mandate: Vercel + Supabase + n8n is the current RCD candidate reference pattern (an RCD proposal pending a Technology Stack change, not a Technology Stack position). Power Automate, Azure Functions/Container Apps, and customer-owned runtimes are equally valid candidates.*

| Layer | Reference Implementation | Architectural Status |
| :--- | :--- | :--- |
| **PoV workbench** | Replit | **Provisional**; synthetic/deidentified development only by default |
| **System of record** | GitHub private repositories | **Mandatory and authoritative** |
| **AI engineering worker** | Cursor IDE and Cursor Agent (preferred); Replit Agent permitted for bounded PoV workspace tasks | **Provisional**, human-directed and human-accepted |
| **Web application** | Next.js App Router + TypeScript | **RCD reference proposal**; not named in Technology Stack. Provisional pending ADR; supply-chain review of Next.js required |
| **UI** | Tailwind CSS + standard accessible component primitives (e.g., `shadcn/ui`) | **RCD reference proposal**; Provisional pending ADR; supply-chain review of `shadcn/ui` required |
| **Validation** | Zod or equivalent typed schemas | **Mandatory capability**; Zod not named in Technology Stack (Provisional pending ADR) |
| **Database** | PostgreSQL with one selected ORM per product line; Drizzle preferred unless an ADR selects Prisma | **RCD reference proposal**; PostgreSQL, Drizzle, and Prisma not named in Technology Stack (Provisional pending ADR) |
| **Candidate frontend/API runtime** | Vercel | **RCD proposal** pending Technology Stack change; assess engagement controls |
| **Candidate data/auth platform** | Supabase PostgreSQL and Auth | **RCD proposal** pending Technology Stack change (Supabase remains Parked for automated commercial telemetry); assess isolation, region, recovery, and service-role paths |
| **Candidate orchestration** | Power Automate / n8n / code, selected per workload | No orchestration vendor is the product. **Power Automate** is Agreed for WFM; **n8n** is Provisional and not on the WFM launch path (validate via paid PoV and production gate) |
| **AI providers** | Approved enterprise endpoints selected by an AI Provider Profile | Provider/model not hard-coded as architecture |
| **Secrets** | Approved secrets manager or workload identity; environment variables as runtime delivery mechanism | **Mandatory production capability** |
| **Language foundation** | Python for deterministic services and calculations; TypeScript/JavaScript after Python foundations | **Agreed direction**. TypeScript-first for PoV applications requires an ADR recording rationale and a Python service option |
| **Candidate runtime class** | Azure Functions / Azure Container Apps or equivalent, or customer-owned runtime | **Provisional** target class selected per implementation; gate: cloud/region, workload identity, cost, logging, backup/recovery, operational ownership |
| **Packaging** | Docker / containers | **Agreed direction**; image provenance, scanning, patching, and secret handling required |
| **Future AI workforce platform** | Coordination layer for specialised engineering agents | **Parked**; no autonomous production authority |

---

## 4. Modular Application Structure & Boundary Rules

```text
/src
  /app                 # UI pages and stateless route handlers
  /connectors          # Ingestion/delivery adapters only
  /core
    /pipeline          # State machine, idempotency, retry and replay
    /security          # Redaction, access helpers and retention controls
    /approvals         # Approval policy and decision records
    /telemetry         # Sanitised operational and economic metrics
  /ai_engine
    /prompts           # Versioned prompt templates
    /schemas           # Structured output schemas
    /providers         # Provider adapters and logical model aliases
    /evaluations       # Regression datasets and thresholds
  /db
    /schema            # ORM schema
    /migrations        # Standard SQL migrations
    /policies          # RLS and database controls where applicable
  /config              # Typed, non-secret configuration schemas
/tests
  /unit
  /integration
  /tenant-isolation
  /retention
  /ai-evaluation       # Includes synthetic fixtures (moved from /ai_engine)
/workflows             # Exported n8n / Power Automate definitions, no credentials
/infra                 # Configuration as code / IaC with drift detection
/.cursor
  /rules               # Short, mandatory project rules by control domain
  mcp.json.example     # Sanitised example only; no credentials or live customer endpoints
.cursorignore          # Excludes secrets, customer evidence, dumps and production logs
/.github
  /workflows           # CI/CD pipelines
  CODEOWNERS           # Required reviewers; branch protection documented
Dockerfile             # Container baseline and container config
/docs
  /specs               # Specifications and acceptance criteria
  ARCHITECTURE.md      # Project-specific profile
  /adr                 # Architecture decisions
  DATA_PROFILE.md
  AI_PROVIDER_PROFILE.md
  RUNBOOK.md
```

### Architectural Boundary Rules

| Boundary | Mandatory Rule |
| :--- | :--- |
| **Connectors** | Translate external payloads into versioned internal `JobPayload` contracts and deliver approved outputs. Customer-specific integration logic remains here. |
| **Core pipeline** | Owns deterministic state transitions, idempotency, bounded retry, quarantine, and authorised replay. Contains no hard-coded prompts or vendor SDK logic. |
| **AI engine** | Owns prompt templates, provider adapters, structured schemas, and evaluations. Provider/model changes do not require connector or core rewrites. |
| **API routes** | Stateless and bounded. No in-memory schedulers, local file persistence, or long-running processing assumptions. |
| **Database** | Schema, migrations, and access controls are reviewed artifacts. No runtime auto-mutation of production schema. |
| **Configuration** | Non-secret configuration is typed and versioned. Secret values remain outside source and database configuration documents. |

---

## 5. Data & Tenancy Architecture

| Entity | Minimum Fields / Intent |
| :--- | :--- |
| **`tenants`** | `id, name, status, region, created_at`; represents a customer deployment boundary even when one tenant exists per deployment |
| **`users`** | `id, auth_subject, email, status`; identity record independent of tenancy |
| **`tenant_memberships`** | `user_id, tenant_id, role, status, valid_from, valid_until`; supports RCD operators, customer reviewers, and time-bounded access |
| **`integrations`** | `id, tenant_id, provider, secret_reference, config_json`; stores references, never production secret values by default |
| **`workflows`** | `id, tenant_id, name, ai_module, approval_policy, policy_version, retention_profile` |
| **`jobs`** | `id, tenant_id, workflow_id, status, idempotency_key, attempt_count, timestamps, payload_expires_at, purged_at, quarantine/replay fields` |
| **`approvals`** | `job_id, policy, requested_at, decided_at, decided_by, decision, reason, policy_version` |
| **`audit_logs`** | `tenant_id, job_id, event_type, actor_id, timestamp, sanitised result/error code`; no customer payload or unnecessary PII |
| **`operational_metrics`** | `duration, AI duration, provider/model alias, token counts, estimated cost, retries, intervention indicator/minutes, outcome code` |

* **Tenancy & RLS Controls:**
  * Every customer-scoped table carries `tenant_id` / `customer_id` even in a customer-isolated deployment; shared multi-tenancy is not approved merely because the schema is tenant-aware.
  * Use database-enforced **Row-Level Security (RLS)** where a shared database is approved (supplements, but does not replace, application access controls and tests).
  * Test `SELECT`, `INSERT`, `UPDATE`, `DELETE`, joins, RPC/functions, background jobs, service-role paths, and object storage for cross-tenant access. Do not claim tenant leakage is mathematically impossible; retain defence in depth and evidence.

---

## 6. Job Lifecycle, Idempotency & Replay

```text
received -> validating -> processing -> pending_approval -> approved/rejected -> delivering -> completed
Exception paths: failed_retryable -> quarantined -> authorised_replay
Payload retention path: Any payload-bearing state -> expired -> purged
```

| Control | Requirement |
| :--- | :--- |
| **Idempotency** | Every ingress carries or derives an `idempotency_key`. Duplicate delivery cannot produce duplicate consequential actions. |
| **Retries** | Bounded exponential back-off with maximum attempts and sanitised error classification. |
| **Quarantine** | Exhausted or policy-blocked jobs move to quarantine with minimum necessary data and explicit expiry. |
| **Replay** | Replay requires authorisation, records `replay_of_job_id`, and cannot bypass approval or idempotency. |
| **State transitions** | Persist immutable audit events; reject invalid transitions. |
| **External delivery** | Use delivery receipts or reconciliation where the external system supports them. |

---

## 7. Human Approval Architecture

| Policy | Use |
| :--- | :--- |
| **`none`** | Only approved low-consequence, reversible actions with documented rationale |
| **`customer_reviewer`** | Customer-designated person approves customer-facing or business action |
| **`rcd_reviewer`** | RCD approves technical/operational action (`rcd_reviewer` maps to the **Founder** by default until formally delegated) |
| **`customer_and_rcd`** | Both parties approve material action |
| **`dual_control`** | Two authorised reviewers required for high-impact actions |

* **Approval Governance Rules:**
  * Approval records must capture requester, policy version, decision, decision-maker, time, and reason. A Boolean `requires_approval` may be retained for convenience but cannot replace the approval policy.
  * AI output may support a decision but cannot act as the approval actor.
  * **Fail-closed timeouts:** Approval timeouts transition the job to `expired` or `quarantined` according to the retention profile and are never auto-approved.
  * Any delegation of Founder approval authority requires a recorded delegation (delegate, scope, effective, and expiry dates). Production promotion always requires a named human approver outside AI tooling.
  * **No self-approval:** Where the requester is the sole RCD reviewer, the action requires the customer reviewer or Founder and is never self-approved.

---

## 8. Payload Retention & Deletion Controls

| Control | Standard |
| :--- | :--- |
| **Expiry model** | Use `processing_completed_at`, `approval_requested_at`, and `payload_expires_at` rather than deriving expiry only from `created_at`. |
| **Immediate purge** | On `completed` or `rejected` state, remove payload and AI output immediately unless a documented legal/contractual exception applies. |
| **Maximum target** | Normal processing payloads are targeted for removal **no later than 15 minutes** after completion or expiry (`payload_expires_at` / `processing_completed_at` to `purged_at`; worst-case schedule stated in Retention Profile). |
| **Quarantine** | Retry/quarantine payloads are removed within **24 hours** unless an approved exception defines shorter or longer treatment. |
| **Zero-persistence profile** | RCD application components do not intentionally persist payloads; separately validate platform, proxy, AI-provider, APM, and integration retention. |
| **Purge evidence** | Record metadata-only purge event and test actual elapsed deletion time. |
| **Contractual commitment** | Do not describe the 15-minute target as an SLA until the whole production chain has passed repeated operational tests and contract approval. |
| **Operational metadata** | Held online for **12 months**. |
| **WFM raw evidence** | Removed **no later than 30 days** after completion *(note: commercial customer decks commit to $\le 10$ business days post-acceptance; apply the stricter engagement commitment)*. |
| **Compliance/control evidence** | Generally retained for **three years** in the central evidence repository. |

* **Recommended Timing Fields:** `created_at`, `processing_started_at`, `processing_completed_at`, `approval_requested_at`, `payload_expires_at`, `purged_at`, `retention_policy`, `retention_exception_id`.

---

## 9. Logging, Telemetry & Evidence

* Raw request bodies, payloads, prompt content, raw LLM responses, credentials, and tokens are **forbidden in logs**.
* All application logging passes through a sanitised logger with a field allow-list (`timestamp`, `tenant_id`, `job_id`, `workflow_id`, `status`, sanitised error code, `duration`, `attempt`, `correlation_id`).
* Platform logs, APM, error tracking, web analytics, and session replay must be assessed as separate data destinations.
* Audit evidence includes approvals, deployments, configuration changes, model/prompt versions, tests, exceptions, replay, and restoration results.

---

## 10. AI Engineering & Provider Controls

| Artifact | Required Content |
| :--- | :--- |
| **AI Provider Profile** | Provider, model, endpoint, region, training use, request retention, abuse-monitoring exceptions, subprocessors, approved classifications, customer approval, effective/review dates |
| **Prompt package** | Prompt ID/version, schema version, logical model alias, tool allow-list, and prohibited behaviours |
| **Evaluation suite** | Synthetic fixtures, expected/acceptable outcomes, failure cases, safety/control cases, and quantitative threshold |
| **Change gate** | Material provider, model, prompt, schema, or tool change requires impact assessment and passing evaluation |
| **Runtime control** | Only approved logical model aliases may be invoked; fail closed or invoke an approved fallback when no compliant route exists |

* No-training and zero-retention (ZDR) are separate provider attributes and must be validated separately per provider, endpoint, feature, and credentials combination.
* AI-generated code and architecture changes require human review, tests, and repository evidence. AI engineering workers (Cursor Agent and permitted Replit Agent use) require explicit controls over tool permissions, prompt-injection exposure, extension supply chain, data exposure, and reproducibility.
* Maintain a version-controlled provider/model inventory and an approved baseline for regression evidence. A future AI workforce platform is **Parked** and may never hold autonomous production authority.

---

## 11. Identity, Authentication & Secrets

* Replit development uses an RCD-owned workspace, MFA, and least-privileged collaboration; personal workspaces are not approved. Replit Auth, Replit KV, and Replit Object Storage are not used in portable application foundations unless an approved ADR explicitly accepts the dependency.
* Production authentication uses an approved identity service; email/password is not the default for enterprise customer access where federation is required. Use `users` plus `tenant_memberships` rather than forcing one user into one tenant.
* Secrets are supplied at runtime through environment variables or workload identity, originating from an approved secret manager. Local `.env` files are synthetic-development only, excluded by `.gitignore`, and never committed.
* Production credentials are least-privileged, customer-specific, and separated from development credentials.
* Replit may be used with customer Confidential data only after engagement-specific approval and validation of the RCD-owned workspace against managed-device, MFA, and JIT access controls in the Technology Stack; Restricted data, production credentials, and unredacted evidence are not approved.

---

## 12. Software Supply Chain & CI/CD

```text
pull request -> build -> lint -> typecheck -> unit tests -> integration tests
-> tenant-isolation tests -> retention tests -> secret scan -> SAST
-> dependency/SCA scan -> AI evaluation tests -> preview deployment
-> human acceptance -> controlled production promotion -> health check -> rollback
```

| Gate | Minimum Expectation |
| :--- | :--- |
| **Dependencies** | Lock file, approved sources, vulnerability review, and licence review |
| **Secrets** | Repository and build-output secret scanning |
| **Static analysis** | SAST/CodeQL or equivalent for production candidates |
| **SBOM** | Generate and retain for production candidates |
| **Agent changes** | Review all files, packages, scripts, and configuration changes introduced by Cursor Agent or Replit Agent |
| **Vulnerability threshold** | **Zero Critical; zero High** unless a Founder-approved non-production exception with compensating control under Section 21 (Founder holds authority until formally delegated); **Medium** remediation plan before production |
| **Traceability** | Production artifact maps to approved commit, tests, approvals, and deployment record |
| **Container and IaC scanning** | Container image scanning and IaC/configuration scanning with image provenance and patching |
| **Version pinning** | Pin dependency, base image, and CI action versions where appropriate |
| **CI runners and secrets** | Isolated CI runners; protected secrets; no secrets in build output |
| **Configuration drift** | Configuration as code with daily and post-change drift detection and risk-based remediation evidence |
| **Penetration testing** | Annual penetration test and re-testing after material change |
| **CI evidence** | Retain CI evidence for builds, tests, scans, and approvals |

---

## 13. Backup, Recovery & Rollback

| Area | Requirement |
| :--- | :--- |
| **Application** | GitHub authoritative; release tags; reproducible build; previous approved artifact available for rollback |
| **Database** | Backup/PITR selected for service tier; migration strategy; integrity validation; restoration procedure |
| **Orchestration** | Workflow definitions exported/source-controlled without credentials; recreation runbook |
| **Configuration** | Typed configuration inventory; secret-reference inventory; environment reconstruction procedure |
| **Targets** | Internal initial targets **RPO $\le 24	ext{ hours}$** and **RTO $\le 1	ext{ business day}$** until achieved in two restoration exercises |
| **Testing** | Continuity backup after each production release and restoration test at least every six months |

---

## 14. Candidate Platform Controls

* **Replit PoV:** Synthetic or approved deidentified data only by default; private development access; no public publishing; no production credentials; final work pushed to an RCD-controlled GitHub branch and reviewed via pull request; project must execute without relying on undocumented Replit state. Customer Confidential data requires engagement-specific approval; Restricted data and production credentials are not approved; Replit deployments are short-lived, non-production, and have a documented shutdown date.
* **Vercel Candidate Runtime:** Use stateless bounded functions; prohibit payload logging; do not adopt durable workflow/payload features without retention review; assess region, private access, audit logging, log retention, recovery, and cost.
* **Supabase Candidate Data/Auth:** Use standard migrations and one ORM; validate pooling mode; enable and test RLS where shared data infrastructure is approved; treat service-role credentials as privileged bypass paths; schedule purge functions and monitor execution evidence.
* **n8n Candidate Orchestration:** Disable unnecessary successful/progress/manual execution data retention; test success, error, waiting, retry, and manual paths against retention requirements; use HMAC/signature verification, idempotency, and least-privileged credentials; source-control/export workflow definitions and define recreation/rollback.
* **Container Baseline & Runtime Portability:** Every application carries a `Dockerfile` and container configuration so it can move from Vercel to Azure Functions/Container Apps or a customer-owned runtime. Container images are scanned, patched, built with provenance, and run without baked-in secrets. Vercel serverless limits do not suit long-running replay, purge, and scheduled jobs—run these in the orchestration runtime or a container/Azure Function with its own scheduler and record placement in `docs/ARCHITECTURE.md`.

---

## 15. Mandatory Acceptance Tests

| Test Family | Required Evidence |
| :--- | :--- |
| **Architecture** | Folder boundaries and dependency rules enforced; no vendor logic in core pipeline |
| **Portability** | Fresh clone builds and runs from documented configuration without Replit-only services |
| **Isolation** | Cross-tenant read/write/delete/insert/join/RPC/service-role tests |
| **Retention** | Immediate purge on completion/rejection; expiry purge within target; quarantine expiry; no payload in logs/platform evidence |
| **Approval** | Invalid actor blocked; timeout handled; policy version and reason retained |
| **Idempotency** | Duplicate webhook produces one consequential outcome |
| **Replay** | Replay authorised, traceable, and cannot bypass idempotency/approval |
| **AI** | Schema adherence, regression threshold, prohibited outcome, and provider-failure fallback |
| **Security** | AuthN/AuthZ, HMAC, secret handling, dependency/SAST/secret scans |
| **Recovery** | Rollback and restoration procedure demonstrated |
| **Economics** | Token/call/runtime/retry/intervention telemetry supports unit-cost calculation |
| **AI security** | Prompt injection and indirect injection via customer documents; context scoping (no cross-tenant or unauthorised context); tool allow-list enforcement; AI must not invent missing numeric inputs |
| **Deterministic processing** | Calculations, mappings, and scoring performed by deterministic code, not the model, and tested as such |

---

## 16. PoV-to-Production Decision Gate

| Decision | Meaning |
| :--- | :--- |
| **Proceed on reference stack** | Vercel/Supabase/n8n or selected components pass all engagement controls and economics |
| **Proceed, migrate runtime** | PoV proves value but another approved runtime better satisfies production requirements |
| **Revise** | Security, privacy, retention, recovery, operations, or economics require redesign |
| **Stop** | Value, control, or service economics do not justify production progression |

* **Gate Prerequisites:** Confirm customer-isolation model and whether customer-owned deployment is required -> approve provider/region/subprocessor/data-retention profile -> demonstrate Go-Live tests, recovery, and rollback -> confirm monitoring, support ownership, service hours, and cost envelope -> record architecture decision and production baseline.

---

## 17. Managed AI Operations Telemetry

Retain non-sensitive metrics sufficient to explain service health, support effort, and economics without storing customer payloads:
`duration_ms`, `ai_duration_ms`, `provider_alias`, `model_alias`, `input_token_count`, `output_token_count`, `estimated_ai_cost`, `integration_calls`, `retry_count`, `human_intervention_required`, `human_intervention_minutes`, `outcome_code`, `estimated_infrastructure_cost`, `licence_allocation`, `monitoring_cost`, `support_minutes`, `service_tier`, `exception_queue_depth`, `replay_count`.

* **Production Operations Controls:**
  * Cost attribution (licences, model/API use, infrastructure, partner support, monitoring, and founder intervention) is attributed to the customer service envelope.
  * Monitoring and alerting cover health, integration status, failures, latency, consumption, and exception queues (automated monitoring may be continuous; human response is not $24 	imes 7$).
  * Incident record with customer notification workflow and a post-incident review within **five business days** of material incident closure.
  * Release management with Founder approval gate (until formally delegated), health checks, and rollback. Runbooks define support boundary, escalation, defect vs. enhancement classification, customer dependency ownership, and safe suspension/shutdown. Service reporting is tiered (`Essential`, `Growth`, `Scale`) and includes exception and replay counts. Configuration drift is detected daily and after each change.

---

## 18. Project `ARCHITECTURE.md` Template

```markdown
# Project Architecture Profile
## 1. Workload and customer outcome
## 2. Governing documents and ADRs
## 3. Data classifications and prohibited data
## 4. Customer-isolation model
## 5. Connectors and JobPayload contract
## 6. Approval policy
## 7. Retention profile and exceptions
## 8. AI Provider Profile and evaluation threshold
## 9. Deployment target and region
## 10. Secrets and identity model
## 11. Monitoring, support and operational telemetry
## 12. Backup, recovery, rollback and shutdown
## 13. Mandatory tests and acceptance evidence
## 14. PoV-to-production decision
```

---

## 19. Cursor Engineering Workflow, Task Structure & Controls

### Foundation Instructions
Before modifying code, read `docs/ARCHITECTURE.md`, applicable ADRs, specifications, `.cursor/rules`, and this Reference Architecture:
1. Identify conflicts, missing decisions, and ambiguous acceptance criteria; stop where a missing decision affects architecture, security, data handling, retention, identity, or production operation.
2. Produce an implementation plan listing proposed files, dependencies, migrations, tests, assumptions, and task sequence; **do not modify files until accepted by the human reviewer**.
3. Implement only the approved task scope without introducing unapproved packages, services, MCP servers, external endpoints, or platform dependencies, and without accessing customer data, production credentials, or Restricted information.
4. Run task-specific and mandatory acceptance tests; return changed files, dependencies, commands executed, test results, unresolved issues, and residual risks. Never merge, deploy, promote, or approve the work.

### 10 Bounded Cursor Task Packets (Human Review Gate After Each Packet)
1. **Repository intake** -> 2. **Implementation plan** (no code changes) -> 3. **Foundation scaffold** -> 4. **Data foundation** -> 5. **Pipeline controls** -> 6. **Security and retention** -> 7. **AI-engine boundary** -> 8. **Acceptance evidence** -> 9. **Supply-chain review** -> 10. **Pull-request preparation**.

### Cursor Security, Data Controls & Rules Hierarchy
* Use an RCD-controlled Cursor account/team and repository; keep terminal command approval enabled; configure `.cursorignore` to exclude `.env`, credential exports, customer evidence, dumps, production logs, raw customer samples, and secret-manager output.
* Treat MCP servers as new integrations/subprocessors requiring explicit architecture, security, and DPA approval.
* Local Cursor IDE is default; Cursor Cloud Agents require a project ADR, repository-access assessment, secrets design, retention review, and DPA.
* **Rules Hierarchy:** `Master Business Architecture -> Technology Stack Requirements -> PoV Application Reference Architecture -> project ARCHITECTURE.md -> approved ADRs/specifications -> Cursor project rules -> individual task instructions`. Recommended `.cursor/rules/`: `architecture.mdc`, `security-and-data.mdc`, `typescript.mdc`, `database.mdc`, `testing.mdc`, `deployment.mdc`.

---

## 20. Day-1 PoV & Production Candidate Checklists

### Day-1 PoV Checklist
* [ ] Private RCD GitHub repository created and approved local clone opened in an RCD-controlled Cursor workspace.
* [ ] Project `ARCHITECTURE.md` completed and approved; synthetic/deidentified dataset prepared; Data, AI provider, approval, and retention profiles recorded.
* [ ] CI baseline and mandatory tests scaffolded; zero Replit-only persistence/auth dependency.
* [ ] Required `.cursor/rules` files installed and reviewed; `.cursorignore` validated; Cursor privacy, terminal, MCP, and external-tool settings recorded and approved.
* [ ] Initial task plan approved before agent changes begin; Replit workspace created only where required for PoV development/demonstration.

### Production Candidate Checklist
* [ ] Customer-isolation, provider, region, and subprocessor decisions approved.
* [ ] All mandatory tests and security gates pass; audit, monitoring, support, and cost telemetry operational; backup, rollback, and restoration evidence exists.
* [ ] Payload retention proven across application and all subprocessors; production artifact traceable to approved GitHub commit and human approval; `Proceed / Revise / Stop` decision recorded.

---

## 21. Change Control & Appendix A (Technology Stack Change Request)

| Change Type | Required Treatment |
| :--- | :--- |
| **Prompt/model/provider change** | AI impact assessment and evaluation results |
| **New connector** | Contract, auth, idempotency, retry, retention, and security tests |
| **New platform/subprocessor** | Technology architecture review and data-processing assessment |
| **Shared multi-tenancy** | Master/technology governance decision and repeatability evidence after Customers 1–3 ($\ge 70\%$ reuse, $\ge 30\%$ delivery-hour reduction, $\ge 2$ of Customers 1–3 buying substantially the same core pattern) |
| **Production data-class increase** | Customer/contract/security approval and updated Data Profile |
| **Control exception** | Named owner, reason, compensating control, expiry, and approval |

### Appendix A: Technology Stack Change Request (`v1.1 -> v1.2`)
* **Target Document:** RCD Technology Stack Requirements v1.1 (`§3.2`, `§3.4`, `§5`) | **Requested By:** `[Founder]` | **Date:** 20 November 2026
* **Proposed Change:** Add **Vercel** (stateless bounded frontend/API functions) and **Supabase** (PostgreSQL and Auth) as **Provisional, evidence-triggered** candidates in `§3.2` and `§5` (leaving Supabase for automated commercial telemetry as **Parked**). Not approved: Restricted data, production credentials in PoV workspaces, shared multi-tenancy, or production standardisation without a paid PoV.
* **10 Mandatory Gate Criteria:** (1) Cloud/region acceptable to customer; (2) Customer isolation + cross-tenant RLS/service-role tests; (3) MFA, least privilege, JIT access, secret manager/workload identity; (4) 15-minute payload purge & 24h quarantine proven + no payload logging; (5) Subprocessor DPA & customer approval; (6) Backup/PITR + `RPO <= 24h` / `RTO <= 1 business day` proven in two restoration exercises; (7) Zero Critical/High dependency/container/IaC findings; (8) Monitoring/runbooks + long-running jobs offloaded from Vercel; (9) Cost per envelope meets margin gate; (10) Fresh clone portability + documented exit path to Azure or customer-owned runtime.
