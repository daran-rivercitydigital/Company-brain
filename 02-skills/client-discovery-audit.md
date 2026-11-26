---
id: SKILL-002
title: Client Discovery & AI Readiness Audit Compiler
category: skills
status: active
version: 1.0
effective_date: 2026-11-26
compliance_scope: [NZ-Privacy-Act-2020, ISO-27001-2022, SOC-2]
related_docs:
  - 01-wiki/playbooks/nz-sme-ai-adoption.md
  - 01-wiki/nz-compliance/privacy-security-ai-controls.md
  - 02-skills/ingest-rcd-doc.md
owner: Chief of Staff & AI Systems Architect
---

# `SKILL-002`: Client Discovery & AI Readiness Audit Compiler

## 1. Purpose & Trigger Conditions
Use this skill whenever raw client discovery notes, stakeholder interview transcripts, system inventories, or Phase 1 AI Readiness Audit materials are placed in `00-raw/` (or provided directly in a sanitized compilation prompt).

* **Primary Objective:** Transform unstructured client discovery inputs into a standardized, pseudonymized client knowledge file (`01-wiki/clients/Client-XXX-00.md`) and a scored Phase 1 Opportunity Matrix aligned with `PB-002`.
* **Mandatory Security Gate:** Enforce strict de-identification and immediate raw-file purging so zero client PII, commercial secrets, or credentials ever enter Git history.

---

## 2. Pseudonymization & Sanitization Rules (Zero-Tolerance Gate)
Before writing a single line to `01-wiki/clients/`, `index.md`, or `log.md`, strip and transform all sensitive identifiers:

1. **Client Entity Code (`Client-XXX-00`):**
   * Assign a 3-letter region/sector code + 2-digit sequence number (e.g., `Client-WKO-01` for Waikato client #1, `Client-AKL-02`, `Client-TRD-01`).
   * Verify `index.md` first so existing client codes are reused rather than duplicated.
2. **Strip All Direct & Indirect PII:**
   * Replace real company names, trading names, and subsidiary names with `Client-XXX-00`.
   * Replace all personal names with role titles (`[Managing Director]`, `[Operations Manager]`, `[Lead Estimator]`, `[Admin Coordinator]`).
   * Redact all email addresses, phone numbers, physical street addresses, URLs/domains, NZBNs, IRD numbers, and bank/account details.
3. **Strip All Secrets & Tenant Identifiers:**
   * Redact API keys, tenant IDs, SharePoint site URLs, webhook endpoints, and passwords; replace with `{{ENV_VAR_NAME}}` or `[REDACTED-TENANT-ID]`.
4. **Generalize Identifying Niche Facts:**
   * Express revenue, staff count, and volume as bands or rounded metrics (e.g., `25–35 staff`, `~$4M–$6M annual turnover`, `~120 quotes/month`) so the entity cannot be re-identified externally.

---

## 3. Step-by-Step Execution Workflow

### Step 1: Intake & De-Identification Pass
1. Read all discovery files staged in `00-raw/` (e.g., meeting transcripts, questionnaire exports, tech-stack notes).
2. Check `index.md` to confirm whether a `Client-XXX-00` file already exists for this client.
3. Perform the **Sanitization Pass** (Section 2) in memory before generating any repository output.

### Step 2: Score AI Readiness (1–5 Scale per Dimension)
Evaluate the client across the five `PB-002` readiness pillars based strictly on evidence in the discovery notes (mark unverified items as `TBD — Verify in Technical Audit`):

| Dimension | Score (1–5) | Assessment Criteria |
| :--- | :---: | :--- |
| **1. Data & Document Hygiene** | `[1-5]` | Structured digital records vs. paper/siloed spreadsheets; SharePoint/folder hygiene |
| **2. Core Tech Stack & APIs** | `[1-5]` | Cloud SaaS maturity (M365, Google Workspace, Xero, modern CRM/ERP) vs. legacy on-prem |
| **3. Privacy & Security Posture** | `[1-5]` | MFA/Entra ID adoption, M365 permissions hygiene, NZ Privacy Act 2020 awareness |
| **4. Leadership & Champion Buy-In** | `[1-5]` | Executive sponsorship + availability of 3–8 frontline pilot champions |
| **5. Workflow Repeatability & ROI** | `[1-5]` | Clear, high-volume repetitive bottlenecks with measurable baseline hours/rework |

### Step 3: Build the Workflow Opportunity Matrix
Extract 3–6 candidate workflows from the discovery inputs and score each using `PB-002` rules:
* **Baseline Volume & Time:** Tasks/week × minutes/task = weekly hours lost.
* **Impact Score (1–5):** Direct margin, turnaround speed, or capacity unlocked.
* **Feasibility & Compliance Score (1–5):** Ease of integration + low privacy risk (`Public` / `Internal` data preferred for Pilot #1).
* **Recommended Track:** `Track A (M365 Native Copilot)` vs. `Track B (Custom Agentic Workflow)` vs. `Defer`.

### Step 4: Write `01-wiki/clients/Client-XXX-00.md`
Create or update `01-wiki/clients/Client-XXX-00.md` using the canonical template in **Section 4** below.

### Step 5: Update `index.md`, `log.md`, and Purge `00-raw/`
1. Add or update the entry in `index.md` under `01-wiki/clients/` (using pseudonym + sector + stage only—zero real names).
2. Append an audit entry to `log.md`.
3. **Delete all raw client discovery files from `00-raw/` immediately** (leaving only `.gitkeep`).
4. Present changes to the human operator for `git diff` review and commit via GitHub Desktop.

---

## 4. Canonical Output Template: `01-wiki/clients/Client-XXX-00.md`

```markdown
---
id: Client-XXX-00
sector: [e.g., Commercial Trades / Field Services / Agribusiness / Professional Services]
region: [e.g., Waikato / Bay of Plenty / Auckland]
size_band: [e.g., 15-30 staff]
engagement_stage: [Discovery | Phase-1-Audit | Phase-2-Pilot | Phase-3-Scale]
compliance_tier: [Standard-NZPA2020 | High-Sensitivity]
last_updated: YYYY-MM-DD
related_docs:
  - 01-wiki/playbooks/nz-sme-ai-adoption.md
  - 01-wiki/nz-compliance/privacy-security-ai-controls.md
---

# Client Profile: `Client-XXX-00`

## 1. Operational Context & Objectives
- **Business Model:** [Concise, non-identifying summary of operations]
- **Primary Pain Points:** [Top 3 operational bottlenecks identified in discovery]
- **Strategic Goals (Next 6–12 Months):** [e.g., Reduce quoting turnaround by 70%, eliminate admin overtime]

## 2. Current Technology Stack & Data Environment
- **Identity & Productivity:** [e.g., Microsoft 365 Business Premium, SharePoint, Teams]
- **Finance & Operations:** [e.g., Xero, Fergus / SimPRO / HubSpot / Custom SQL]
- **Data Residency & Security Notes:** [e.g., AU/NZ M365 tenant; SharePoint permissions require cleanup prior to Copilot]

## 3. AI Readiness Scorecard (`PB-002` Baseline)

| Pillar | Score (1–5) | Key Findings & Gaps |
| :--- | :---: | :--- |
| Data & Document Hygiene | X/5 | ... |
| Core Tech Stack & APIs | X/5 | ... |
| Privacy & Security Posture | X/5 | ... |
| Leadership & Champion Buy-In | X/5 | ... |
| Workflow Repeatability & ROI | X/5 | ... |
| **Composite Readiness Score** | **XX/25** | **[Ready for Track A/B Pilot | Needs Data/Permission Remediation First]** |

## 4. Prioritized Workflow Opportunity Matrix

| Workflow | Current Baseline | Impact (1–5) | Feasibility (1–5) | Recommended Track | Priority |
| :--- | :--- | :---: | :---: | :--- | :---: |
| [e.g., Automated Quote Drafting] | ~12 hrs/wk; 48h SLA | 5 | 4 | Track B (Custom Agent + HITL) | **Pilot #1** |
| [e.g., Site Meeting & Scope Summaries] | ~6 hrs/wk | 4 | 5 | Track A (M365 Copilot) | **Quick Win** |

## 5. Privacy, Security & HITL Guardrails (`privacy-security-ai-controls.md`)
- **Data Classification Involved:** [Internal / Confidential / Restricted PII]
- **NZ Privacy Act 2020 Controls:** [e.g., Redact customer residential addresses before LLM inference; zero-retention API enabled]
- **Mandatory Human-in-the-Loop Gate:** [Specify who approves output before external send or ERP write]

## 6. Next Actions & Open Questions
- [ ] [Action item 1 — e.g., Run M365 SharePoint permission audit]
- [ ] [Action item 2 — e.g., Collect 10 sanitized sample quotes for Pilot #1 benchmarking]
```
