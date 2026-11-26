---
id: PB-002
title: Flagship NZ SME AI Adoption Playbook
category: playbooks
status: active
version: 1.0
effective_date: 2026-11-26
compliance_scope: [NZ-Privacy-Act-2020, ISO-27001-2022, SOC-2]
related_docs:
  - 01-wiki/architecture/second-brain-master-reference.md
  - 01-wiki/nz-compliance/privacy-security-ai-controls.md
  - 01-wiki/playbooks/second-brain-architecture.md
owner: Chief of Staff & AI Systems Architect
---

# Flagship NZ SME AI Adoption Playbook (`PB-002`)

## 1. Purpose & Target Profile
This playbook defines River City Digital’s end-to-end delivery methodology for **New Zealand Small-to-Medium Enterprises (SMEs)** (typically 10–150 staff across Waikato and nationwide in trades, field services, professional services, agribusiness, and logistics).

* **Core Objective:** Move NZ SMEs from ad-hoc, unvetted AI experimentation ("Shadow AI") to secure, measurable, human-in-the-loop operational workflows within 6–10 weeks.
* **Commercial Philosophy:** Fixed-scope, outcome-anchored phases that de-risk adoption, enforce NZ Privacy Act 2020 compliance from day one, and deliver auditable ROI before scaling custom automation.

---

## 2. Three-Phase Engagement Lifecycle

| Phase | Duration | Primary Deliverable | Exit Gate |
| :--- | :--- | :--- | :--- |
| **Phase 1: AI Readiness & Workflow Audit** | 1–2 Weeks | AI Readiness Scorecard, Opportunity Matrix & Data Governance Baseline | Sign-off on top 1–2 high-ROI pilot workflows + compliance clearance |
| **Phase 2: Controlled Pilot Build** | 2–4 Weeks | Live M365 Copilot / Custom Agent Pilot in isolated tenant/environment | ≥ 85% user acceptance & verified time/cost savings over 14-day UAT |
| **Phase 3: Governance, Handover & Scale** | 2–4 Weeks | Production Runbook, Staff AI Acceptable Use Policy & Quarterly ROI Ledger | Operational handover to client champion + optional Managed AI Retainer |

---

## 3. Phase 1: AI Readiness & Workflow Audit (Weeks 1–2)

### Step 1.1 — Discovery & Workflow Mapping
* Conduct structured stakeholder interviews across leadership, operations, admin, and frontline teams (using `02-skills/client-discovery-audit.md` once deployed).
* Map top 5–8 repetitive, high-friction workflows (e.g., quoting/estimating, job dispatch & field notes, invoice reconciliation, tender responses, customer triage).
* Capture baseline metrics: **hours spent/week**, **error/rework rate**, **turnaround SLA**, and **system touchpoints** (e.g., M365, Xero, Fergus/SimPRO, SharePoint, CRM).

### Step 1.2 — Security, Privacy & Data Residency Gate
Before connecting any AI model to business data, execute the baseline controls in `01-wiki/nz-compliance/privacy-security-ai-controls.md`:
* **Data Classification:** Tag candidate workflows (`Public`, `Internal`, `Confidential`, `Restricted PII`).
* **NZ Privacy Act 2020 Check:** Confirm purpose limitation (IPP 1–3), secure storage (IPP 5), and cross-border disclosure compliance (IPP 12 — prefer AU/NZ cloud regions where available and enforce zero-data-retention API agreements).
* **Tenant Hygiene Audit:** Review M365 SharePoint/OneDrive oversharing permissions prior to enabling Microsoft 365 Copilot so staff cannot query restricted HR or payroll folders.

### Step 1.3 — Prioritization Matrix (Impact vs. Feasibility)
Rank candidate workflows on a 1–5 scale across **Time/Margin Impact** and **Technical/Compliance Readiness**:
* **Quick Wins (High Impact, High Readiness):** Deploy first in Phase 2 (e.g., automated meeting/site-visit summaries, quote drafting from templates, SOP knowledge assistant).
* **Strategic Builds (High Impact, Medium Readiness):** Queue for Phase 3 after data cleanup or API integration (e.g., multi-system job costing agents, automated compliance reporting).
* **Defer / Reject:** High-risk autonomous decisions without human review, or workflows dependent on uncleaned paper/legacy silos.

---

## 4. Phase 2: Controlled Pilot Build (Weeks 3–6)

### Step 2.1 — Architecture Selection Pattern
Select the lightest architecture that solves the validated bottleneck:
1. **Track A — M365 Native (Copilot / Copilot Studio):** Best when client data already lives in SharePoint/Teams/Outlook and requires strict Entra ID permission inheritance.
2. **Track B — Custom Agentic Workflow (Python / API / Supabase / Vercel):** Best for cross-system automation (e.g., parsing PDFs/emails -> validating rules -> staging drafts in ERP/CRM).
   * Store all client credentials exclusively in environment secret vaults (`{{ENV_VAR_NAME}}`).
   * Isolate client repositories and databases per tenant (`Client-XXX-00`).

### Step 2.2 — Mandatory Human-in-the-Loop (HITL) Guardrails
In alignment with `01-wiki/nz-compliance/privacy-security-ai-controls.md`:
* **Draft-First Execution:** Pilot agents generate drafts, classifications, or recommended actions; a designated human staff member approves before external emails, quotes, invoices, or database writes commit.
* **Audit Logging:** Log prompt inputs (redacted of unnecessary PII), model outputs, confidence flags, and human approval timestamps.

### Step 2.3 — 14-Day Pilot UAT & Telemetry
* Run with a cohort of 3–8 pilot champions against real operational tasks.
* Track three hard metrics daily:
  1. **Cycle-Time Reduction (%)** vs. Phase 1 baseline.
  2. **First-Pass Quality / Edit Distance** (how much human rewriting is required).
  3. **Exception / Hallucination Rate** (target < 2% on structured extractions).

---

## 5. Phase 3: Governance, Handover & Scale (Weeks 7–10)

### Step 3.1 — Client AI Governance Pack
Deliver a concise, plain-English operational pack tailored to the NZ SME:
* **Staff AI Acceptable Use Policy (AUP):** Clear rules on approved tools, prohibited PII uploads into public consumer LLMs, and mandatory human verification.
* **System Runbook & Architecture Card:** Plain-language diagram of data flows, prompt templates, API endpoints, and escalation contacts.
* **Incident & Drift Protocol:** How to pause an agent, report an inaccurate output, and rotate API keys if needed.

### Step 3.2 — ROI Verification & Executive Readout
Present a 1-page **Executive Value Scorecard** comparing Phase 1 baseline vs. Phase 2/3 actuals:
* Annualized hours recovered (`Weekly Hours Saved × 48 weeks × Fully Loaded Hourly Rate`).
* Revenue velocity gains (e.g., quote turnaround reduced from 48 hours to 2 hours).
* Licensing & API run-rate cost vs. net annual benefit.

### Step 3.3 — Post-Launch Expansion Paths
* **Path 1 — Self-Sufficient Handover:** Client internal champion manages prompts and user onboarding using RCD runbooks.
* **Path 2 — Managed AI Operations Retainer:** Monthly prompt/model tuning, compliance audits, usage telemetry reviews, and backlog sprints for Workflow #2 and #3.

---

## 6. Consultant Execution Checklist (Per Client)
- [ ] Client pseudonym assigned (`Client-XXX-00`) and profile initialized in `01-wiki/clients/`.
- [ ] Zero raw client PII or API keys stored in `Company-brain` (`00-raw/` purged post-synthesis).
- [ ] M365 SharePoint permission audit completed before any Copilot rollout.
- [ ] Human-in-the-loop approval gate verified on all external-facing or financial outputs.
- [ ] Phase 1 baseline metrics recorded prior to pilot launch to guarantee auditable ROI.
