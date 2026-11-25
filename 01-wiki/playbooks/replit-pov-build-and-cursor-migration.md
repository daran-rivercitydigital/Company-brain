# Replit PoV Build and Cursor Migration Guide

> **Document Status:** Controlled Build Guide (v1.0) | **Effective Date:** 20 November 2026 | **Owner:** [Founder]  
> **Source:** `PoV_Replit_Build_and_Cursor_Migration_Guide.pdf`  
> **Governing Document:** [PoV Application Reference Architecture](../architecture/pov-application-reference-architecture.md) (v1.1)  
> **Default Transition:** `Replit -> Private GitHub Repository -> Local Cursor Workspace -> Production Candidate`

---

## 1. Purpose & Intended Outcome

This guide provides a plain-English, repeatable workflow to start a River City Digital Proof-of-Value (PoV) in Replit without requiring deep software-engineering knowledge, while enforcing portability controls so an approved PoV moves into Cursor IDE for production hardening without being rebuilt from scratch.

* Build quickly in Replit using **synthetic or approved deidentified data**.
* Keep code, configuration, and documentation portable from Day 1; use **GitHub** as the authoritative copy and change history.
* Use **Replit Agent** for bounded planning and implementation tasks—never for architecture approval.
* Move the approved PoV into **local Cursor IDE** (not Cursor Cloud Agents unless separately approved by ADR/DPA) through the same GitHub repository and revalidate security, data, deployment, and operational controls before production.

---

## 2. Tools in Plain English

| Tool | What It Does | RCD Role |
| :--- | :--- | :--- |
| **Replit** | Browser-based development workspace with an AI Agent, editor, runtime, and preview. | Rapid PoV development and demonstrations. |
| **GitHub** | Stores the official repository and the full history of code changes. | Authoritative source for both Replit and Cursor. |
| **Cursor** | Desktop engineering environment with an AI Agent. | Controlled production engineering after the PoV is accepted (local Cursor default). |
| **`replit.md`** | Root-level file automatically read by Replit Agent. | Project context, behaviour, and non-negotiable RCD instructions. |
| **Replit Skills** | Reusable instruction packages stored in `.agents/skills` or centrally in a Workspace. | Optional reusable RCD build workflows. |
| **`ARCHITECTURE.md`** | Project-specific architecture and decisions. | Workload authority beneath the RCD Reference Architecture. |

---

## 3. One-Time Setup & Workspace Controls

### 3.1 Create the Reusable RCD Replit Foundation (`rcd-replit-pov-foundation`)
1. Sign in to Replit using an **RCD-owned email address and controlled account**.
2. Create a new private Replit App called **`rcd-replit-pov-foundation`** from a general or blank application starting point (do not connect customer systems yet).
3. Create the portable folder and document structure (Section 4) and populate the root `replit.md` instructions (Section 5).
4. Create a private GitHub repository called **`rcd-replit-pov-foundation`**, connect the Replit App via Replit's Git tool, and commit/push the initial foundation.
5. Use this foundation as the starting point for every future PoV.

### 3.2 Replit Account & Workspace Controls
* Keep PoV projects **private** unless an explicit decision permits public access; invite only named collaborators (never use unrestricted edit links).
* Use the **Replit Secrets** tool for development secrets—never type secret values into source files, prompts, or `replit.md`.
* Do not place **Restricted data, production credentials, or unredacted customer evidence** in Replit. Use synthetic data by default (deidentified data requires recorded approval and a `DATA_PROFILE.md`).
* Do not enable connectors, MCP servers, or external integrations without an explicit architecture and data-processing decision.

---

## 4. Portable Project Structure & Portability Rules

```text
/
├── .agents/
│   └── skills/                 # Optional reusable Replit Agent skills
├── .github/
│   ├── CODEOWNERS
│   ├── pull_request_template.md
│   └── workflows/              # Platform-independent validation
├── .cursor/
│   └── rules/                  # Present from Day 1 for later Cursor migration
├── docs/
│   ├── ARCHITECTURE.md
│   ├── DATA_PROFILE.md
│   ├── AI_PROVIDER_PROFILE.md
│   ├── RUNBOOK.md
│   ├── MIGRATION_TO_CURSOR.md
│   ├── adr/
│   └── specs/
├── src/
│   ├── app/
│   ├── connectors/
│   ├── core/
│   │   ├── approvals/
│   │   ├── pipeline/
│   │   ├── security/
│   │   └── telemetry/
│   ├── ai_engine/
│   │   ├── evaluations/
│   │   ├── prompts/
│   │   ├── providers/
│   │   └── schemas/
│   ├── config/
│   └── db/
│       ├── migrations/
│       ├── policies/
│       └── schema/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── tenant-isolation/
│   ├── retention/
│   └── ai-evaluation/
├── infra/
├── workflows/
├── replit.md
├── .replit
├── replit.nix                  # Only if actually required
├── Dockerfile
├── .env.example
├── .gitignore
├── .cursorignore
├── package.json
├── README.md
└── LICENSE
```

### 4.1 Portability Rules
* Application logic belongs under `/src`, not inside Replit-specific configuration; keep `.replit` limited to Replit run and development settings.
* Use standard package scripts (`npm run dev`, `npm test`, `npm run build`, `npm start`) and pin runtime/dependency versions in normal repository files.
* Use environment variables through a typed configuration layer—never call Replit secret APIs directly from core application code.
* Use standard database migrations that run outside Replit, provider interfaces for external services (AI, email, storage, auth), a `Dockerfile` to prove container portability, and `.cursor/rules` from Day 1.

---

## 5. Foundational `replit.md`

Create `replit.md` in the repository root and paste this exact specification:

```markdown
# River City Digital PoV Engineering Instructions

## Role and authority
You are a human-directed AI engineering worker for River City Digital.
You may analyse, plan, implement and test explicitly approved tasks.
You may not approve architecture deviations, security exceptions, customer-data use,
new subprocessors, production deployment, release promotion or your own work.

## Governing order
1. RCD Master Business Architecture
2. RCD Technology Stack Requirements
3. RCD PoV Application Reference Architecture
4. docs/ARCHITECTURE.md
5. Approved ADRs and specifications
6. Project build rules and task instructions
A lower-level instruction must not override a higher-level requirement.

## Replit role
Replit is a rapid PoV development and demonstration environment.
GitHub is authoritative. The application must be able to move to Cursor and a
production candidate platform without rewriting core business logic.

## Before changing files
1. Read docs/ARCHITECTURE.md and relevant ADRs/specifications.
2. Inspect the repository, dependencies, migrations and tests.
3. Identify conflicts, missing decisions, assumptions and risks.
4. Produce a file-level implementation plan.
5. List proposed dependencies, external services, migrations and tests.
6. Wait for explicit human approval before implementation.

## Stop conditions
Stop and request a human decision if:
- architecture or acceptance criteria are unclear;
- data classification, retention, tenancy, identity or privileged access is unclear;
- a new connector, integration, dependency, MCP server or external endpoint is needed;
- production credentials or Restricted information would be required;
- the proposed solution creates a Replit-only dependency;
- a mandatory control cannot be met.

## Mandatory build rules
- Customer-isolated and portable first.
- Use synthetic data by default.
- Do not store Restricted data or production credentials in Replit.
- Keep core business logic independent of Replit.
- Use standard package scripts and a documented local run process.
- Use typed environment-based configuration.
- Store no secret values in code, prompts, replit.md, logs or GitHub.
- Do not place raw customer payloads, prompts, model responses or tokens in logs.
- Keep deterministic calculations, permissions and state transitions outside AI models.
- Use provider interfaces and logical aliases; do not hard-code a model or platform.
- Use reviewed, platform-independent database migrations.
- Apply idempotency, bounded retry, quarantine and authorised replay.
- Apply approved human approval controls to consequential actions.
- Implement payload expiry and purge controls.
- Add unit, integration, isolation, retention, replay, approval, security and AI tests.
- Do not depend on Replit Auth, Replit Database, Replit Object Storage or Replit
  deployment behaviour unless an ADR explicitly approves the dependency and its exit plan.
- Do not merge, deploy or approve the work.

## Completion evidence
Return changed files, dependencies, migrations, commands, tests and results,
unmet acceptance criteria, unresolved issues, residual risks and required human approvals.
```

---

## 6. Prompt for Starting a New Replit PoV

```text
I want to start a River City Digital Proof-of-Value application.
Application name: [APPLICATION NAME]
Customer: [CUSTOMER NAME OR INTERNAL]
Business problem: [DESCRIBE THE PROBLEM IN PLAIN LANGUAGE]
Desired outcome: [DESCRIBE WHAT SUCCESS LOOKS LIKE]
Initial workflow: [DESCRIBE THE STEPS A USER OR SYSTEM SHOULD TAKE]
Data available for the PoV: [SYNTHETIC / APPROVED DEIDENTIFIED / OTHER]

Before writing application code:
1. Read replit.md and all governing project documents.
2. Inspect the repository structure.
3. Ask only for decisions that cannot be safely derived from the RCD architecture.
4. Recommend a portable application architecture.
5. Draft docs/ARCHITECTURE.md, docs/DATA_PROFILE.md and the initial ADRs.
6. Identify any proposed Replit-specific feature and provide a platform-independent alternative.
7. Define how the application will run in Replit and later in Cursor/local development.
8. Produce a staged implementation plan and proposed first task.
9. Define tests that prove the PoV can be exported from Replit and run elsewhere.

Do not implement code yet.
Stop after presenting the architecture, assumptions, unresolved decisions,
implementation stages, migration approach and first proposed task.
Wait for my approval.
```

---

## 7. Build Rhythm, Migration Rules & Features to Avoid

### Operating Rhythm
`Architecture -> plan -> human approval -> one bounded task -> tests and evidence -> GitHub commit -> next task`

### Rules That Guarantee Migration to Cursor

| Control | Required Replit Treatment | Migration Evidence |
| :--- | :--- | :--- |
| **Source authority** | Connect to private GitHub repo and push accepted work regularly | Cursor opens the same repository and full history |
| **Runtime** | Use standard runtime commands and pin versions | Fresh local clone can install, build, test, and run |
| **Configuration** | Use typed env variables and `.env.example` with names only | Equivalent variables supplied outside Replit |
| **Secrets** | Store values in Replit Secrets during PoV; never commit values | Production secrets recreated in target secret manager |
| **Database** | Use approved external/portable DB and source-controlled migrations | Migrations execute against a fresh non-Replit database |
| **Authentication** | Use portable provider interface or explicitly approved provider | No core dependency on Replit identity |
| **Storage** | Use portable storage abstraction and documented provider | Files and metadata move without rewriting app logic |
| **AI providers** | Use interfaces, logical model aliases, typed outputs, and evals | Provider/model swaps require no core rewrite |
| **Logging** | Use field allow-lists and standard telemetry interfaces | Logs work without Replit and contain no prohibited payloads |
| **Deployment** | Keep deployment config outside core logic; include `Dockerfile` | Container or target runtime passes health checks |
| **Testing** | Run tests through standard package commands | Same test suite runs in Replit, GitHub CI, and Cursor/local |
| **Documentation** | Maintain `ARCHITECTURE.md`, ADRs, Data Profile, and Runbook | Cursor intake distinguishes settled decisions from open items |

### Features to Avoid or Tightly Control

| Replit Feature / Pattern | RCD Position | Why |
| :--- | :--- | :--- |
| **Replit-only DB / KV persistence** | **Avoid by default** (ADR + exit plan required if used) | Creates migration and data-export work |
| **Replit Auth embedded directly in business logic** | **Avoid** (place authentication behind an adapter) | Production identity may change |
| **Replit Object Storage called directly across app** | **Avoid** (use a storage interface) | Locks code to a platform-specific API |
| **Secrets written into files or prompts** | **Prohibited** | Exposes credentials via chat, source control, or logs |
| **Unreviewed Connectors or MCP servers** | **Prohibited until approved** | Introduces data destinations and subprocessor risk |
| **Production customer data in a PoV** | **Prohibited by default** | PoV environment is not the production control boundary |
| **Agent-created dependency without review** | **Not accepted** | Supply-chain, licence, maintenance, and security risk |
| **Replit Deployments as permanent production design** | **Not assumed** | Production platform remains an evidence-triggered decision |
| **Business logic in `.replit` or deployment scripts** | **Prohibited** | Prevents standard execution outside Replit |

---

## 8. GitHub Connection, Transition Gate & Migration Checklist

### GitHub Connection Steps
1. Create a private GitHub repository matching the Replit project name; connect your GitHub account in Replit settings and link the repo in the Git tool.
2. Verify `.gitignore` excludes `.env`, exports, logs, customer evidence, and local database files before pushing the initial commit (`Initial RCD PoV foundation`).
3. Commit and push after every accepted task; verify the latest accepted commit in GitHub.

### PoV Acceptance & Transition Decision Gate
Record an ADR choosing one of four decisions after confirming business outcome, named owner, isolation/deployment model, data classifications/retention, identity/integration/AI-provider decisions, latest GitHub commit, and Section 12 checklist:
* **Proceed to Cursor engineering** | **Revise in Replit** | **Stop** | **Re-architect before migration**

### Replit-to-Cursor Migration Checklist
* [ ] **Repository & Clean Clone:** Private GitHub repo holds latest accepted commit with zero secret values; fresh clone into empty folder succeeds.
* [ ] **Install, Build, Test & Run:** Standard commands install dependencies, build, pass unit/integration/isolation/retention/AI tests, and start locally with synthetic config without Replit.
* [ ] **Configuration & Database:** `.env.example` lists names/descriptions only; migrations create a fresh dev schema outside Replit.
* [ ] **External Services & Coupling:** Every provider has an interface + approved decision or open ADR; search confirms zero Replit-only modules or environment dependencies in `/src`.
* [ ] **Documents, Cursor Rules & Operations:** `ARCHITECTURE.md`, `DATA_PROFILE.md`, `AI_PROVIDER_PROFILE.md`, `RUNBOOK.md`, ADRs, `MIGRATION_TO_CURSOR.md`, and `.cursor/rules` are current; operational/support gaps listed; human owner approved transition.

---

## 9. First Prompt in Cursor IDE & Day-1 Checklist

### First Prompt After Opening Repository in Cursor
```text
This repository contains an RCD Proof-of-Value developed in Replit and approved for production engineering.
Do not modify files yet.
1. Read .cursor/rules, docs/ARCHITECTURE.md, all ADRs, docs/DATA_PROFILE.md,
   docs/AI_PROVIDER_PROFILE.md, docs/RUNBOOK.md and docs/MIGRATION_TO_CURSOR.md.
2. Inspect the repository, dependencies, migrations, tests and Replit-specific files.
3. Run or propose the documented install, build, test and local-start checks.
4. Identify every remaining Replit dependency and classify it as:
   - development-only and removable;
   - portable and acceptable;
   - requires replacement;
   - requires an architecture decision.
5. Compare the application against the RCD PoV Application Reference Architecture.
6. Produce a production-hardening plan covering security, secrets, identity, data,
   tenancy, retention, telemetry, CI/CD, deployment, backup, recovery and support.
7. List proposed files, dependencies, migrations, tests and ADRs.
8. Stop for human approval before making changes.
Return current-state findings, portability test results, gaps, assumptions,
required decisions, proposed migration tasks and the recommended first task.
```

### Day-1 Checklist for Each PoV
* [ ] New private Replit App and matching private GitHub repo created from `rcd-replit-pov-foundation` and connected.
* [ ] `replit.md` and `.cursor/rules` present and reviewed; `docs/ARCHITECTURE.md` drafted and approved; `DATA_PROFILE.md` completed.
* [ ] Synthetic or approved deidentified dataset prepared; zero production credentials or Restricted data present.
* [ ] Standard install, test, build, and run commands defined; DB and external-service choices recorded; initial portability test defined; first bounded implementation plan approved.

---

## 10. Appendix A: Suggested `.gitignore` and `.cursorignore` Coverage

```text
# Secrets and local configuration
.env
.env.*
!.env.example
*.pem
*.key

# Customer and operational evidence
customer-data/
evidence/
exports/
dumps/
logs/
*.log

# Local databases and caches
*.db
*.sqlite
.cache/
node_modules/
dist/
build/
coverage/

# Editor and OS files
.DS_Store
Thumbs.db
.vscode/
```
