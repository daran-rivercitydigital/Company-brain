# RCD Application Foundation Setup Guide (`rcd-app-foundation`)

> **Document Status:** Operational Setup Guide (v1.0) | **Effective Date:** November 2026 | **Owner:** [Founder]  
> **Source:** `RCD_Application_Foundation_Setup_Guide.pdf`  
> **Target Repository:** `rcd-app-foundation` (Private GitHub Template Repository)  
> **Governing Documents:** [PoV Application Reference Architecture](../architecture/pov-application-reference-architecture.md) (v1.1) | [Replit PoV Build and Cursor Migration Guide](./replit-pov-build-and-cursor-migration.md) (v1.0) | [RCD Master Business Architecture](./rcd-master-business-architecture.md) (v8.2) | [RCD Technology Stack Requirements](../architecture/tech-stack-requirements.md) (v1.1)

---

## 1. Purpose & Foundation Overview

This guide walks through creating River City Digital's reusable application foundation template repository (`rcd-app-foundation`) in GitHub, connecting it to Cursor IDE and Replit, and using it as the standardized starting point for every Proof-of-Value (PoV) and production candidate.

* **What `rcd-app-foundation` Provides:**
  * Portable `/src`, `/tests`, `/docs`, `/infra`, and `/workflows` folder skeleton aligned with the Reference Architecture.
  * Pre-configured `.cursor/rules/` domain policies, `.cursorignore`, `.gitignore`, `replit.md`, `.env.example`, and `Dockerfile`.
  * Standard templates for `docs/ARCHITECTURE.md`, `docs/DATA_PROFILE.md`, `docs/AI_PROVIDER_PROFILE.md`, `docs/RUNBOOK.md`, `docs/MIGRATION_TO_CURSOR.md`, and Architecture Decision Records (`docs/adr/`).
  * GitHub repository protections, `CODEOWNERS`, pull request templates, and CI validation workflows.

---

## 2. Phase 1: Create the Private GitHub Template Repository

1. Sign in to GitHub using your **RCD-controlled GitHub organization/account** (`[RCD_GITHUB_ORG]`).
2. Create a new **Private** repository named **`rcd-app-foundation`**:
   * Enable **Template repository** in repository settings so future PoVs can be generated cleanly via **Use this template**.
   * Initialize with a `README.md` and a `main` default branch.
3. Configure baseline repository security & governance under **Settings**:
   * **Branch Protection (`main`):** Require pull request reviews before merging, require status checks to pass before merging, and block force pushes.
   * **Secret Scanning & Dependabot:** Enable secret scanning, push protection, and Dependabot security alerts.
   * **Access Control:** Restrict access strictly to named RCD personnel with least-privileged roles.

---

## 3. Phase 2: Scaffold the Foundation Repository Structure

Clone `rcd-app-foundation` locally, open it in **Cursor IDE**, and scaffold the canonical directory tree:

```text
rcd-app-foundation/
├── .agents/
│   └── skills/                 # Optional reusable Replit Agent workflow skills
├── .cursor/
│   ├── rules/
│   │   ├── architecture.mdc
│   │   ├── security-and-data.mdc
│   │   ├── typescript.mdc
│   │   ├── database.mdc
│   │   ├── testing.mdc
│   │   └── deployment.mdc
│   └── mcp.json.example        # Sanitised example only — zero credentials/endpoints
├── .github/
│   ├── workflows/
│   │   └── ci.yml              # Build, lint, typecheck, tests, secret & dependency scans
│   ├── CODEOWNERS              # Maps critical paths to @[FOUNDER_GITHUB_HANDLE]
│   └── pull_request_template.md
├── docs/
│   ├── adr/
│   │   └── 0000-template.md
│   ├── specs/
│   ├── ARCHITECTURE.md         # Workload profile template
│   ├── DATA_PROFILE.md
│   ├── AI_PROVIDER_PROFILE.md
│   ├── RUNBOOK.md
│   └── MIGRATION_TO_CURSOR.md
├── infra/
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
├── workflows/
├── .cursorignore
├── .env.example
├── .gitignore
├── Dockerfile
├── package.json
├── README.md
└── replit.md
```

---

## 4. Phase 3: Populate Mandatory Governance & Control Files

### 4.1 `.cursor/rules/` Domain Rule Files
Create short, focused, always-applied Markdown rule files (`*.mdc`) enforcing the Reference Architecture:
* **`architecture.mdc`:** Enforces governance order, modular folder boundaries (`/src/connectors`, `/src/core/pipeline`, `/src/ai_engine`), stateless API routes, and human approval before file changes.
* **`security-and-data.mdc`:** Prohibits secrets, raw customer payloads, prompts, and LLM responses in logs or source control; enforces `tenant_id` scoping, 15-minute payload expiry/purge, and fail-closed approval gates.
* **`typescript.mdc`:** Enforces strict TypeScript typing, typed Zod environment/payload schemas, and explicit ADR requirement if TypeScript is chosen over Python for deterministic services.
* **`database.mdc`:** Enforces single ORM per product line, reviewed SQL migrations (no runtime auto-migration), and RLS testing across all operations and service-role paths.
* **`testing.mdc`:** Requires tests across all 13 mandatory test families (architecture, portability, isolation, retention, approval, idempotency, replay, AI eval, AI security, deterministic processing, security, recovery, economics).
* **`deployment.mdc`:** Requires `Dockerfile` container portability, pinned dependency/image versions, SBOM/SAST/SCA gates, and human approval for release promotion.

### 4.2 `.gitignore` & `.cursorignore`
Ensure both files exclude `.env`, `.env.*` (except `!.env.example`), `*.pem`, `*.key`, `customer-data/`, `evidence/`, `exports/`, `dumps/`, `logs/`, `*.log`, local SQLite/DB files, `node_modules/`, `dist/`, and `build/`.

### 4.3 `replit.md` & `.env.example`
* Populate `replit.md` with the standard RCD PoV Engineering Instructions (role/authority boundaries, governing order, before-changing-files protocol, stop conditions, mandatory build rules, and completion evidence checklist).
* Populate `.env.example` with non-secret variable names and descriptions only (e.g., `DATABASE_URL=`, `AI_PROVIDER_ALIAS=`, `LOG_LEVEL=info`).

---

## 5. Phase 4: Configure Cursor IDE & Replit Environments

### 5.1 Cursor IDE Baseline Controls
1. Sign in to Cursor using your **RCD-controlled account/workspace** (local Cursor IDE is default; Cursor Cloud Agents remain disabled unless approved by project ADR and DPA).
2. Enable **Terminal Command Approval** (require confirmation before agent shell execution) and disable auto-run for destructive/network commands.
3. Verify `.cursorignore` is active and **do not** configure unapproved MCP servers or external connectors.

### 5.2 Replit Foundation App (`rcd-replit-pov-foundation`)
1. Sign in to Replit using your **RCD-owned email address and workspace**.
2. Import or connect `rcd-app-foundation` into a **private** Replit App named `rcd-replit-pov-foundation`.
3. Verify that `replit.md` is detected in the root directory, Replit Secrets contains zero production credentials, and no Replit DB/KV/Auth dependencies exist.

---

## 6. Phase 5: Starting a New Customer or Internal PoV

1. **Create PoV Repository:** In GitHub, click **Use this template** on `rcd-app-foundation` to create a new private repository (`rcd-pov-[client-or-workload]`).
2. **Complete Day-1 Governance Docs:** Before writing feature code, populate `docs/ARCHITECTURE.md`, `docs/DATA_PROFILE.md`, and `docs/AI_PROVIDER_PROFILE.md`, recording explicit **Adopt / Tailor / Not Applicable** status for every Reference Architecture control.
3. **Select Workbench:**
   * If prototyping rapidly in **Replit**, import the new private GitHub repo into a private Replit App using synthetic/approved deidentified data and run the standard Kick-Off Prompt.
   * If engineering directly in **Cursor IDE**, clone the repo locally and execute the 10-packet bounded task sequence with human approval at each gate.
4. **Verify Portability:** Run a clean-clone install, build, and test check outside Replit before promoting to production engineering.
