# Playbook: Second Brain Architecture & Governance Baseline

> **Document ID:** PB-001 | **Version:** 1.1 | **Effective Date:** 2026-11-23  
> **Owner:** Founder & AI Systems Architect (RCD) | **Status:** Approved  
> **Compliance Alignment:** NZ Privacy Act 2020, ISO/IEC 27001:2022, SOC 2 Type I/II

---

## 1. Purpose & Architectural Philosophy
This document establishes the operational architecture, data classification boundaries, and security controls for `company-brain`, the central context layer powering our New Zealand AI adoption consultancy.

Built on **Andrej Karpathy’s LLM Wiki pattern**, the system separates raw operational and client inputs stored in our **RCD Internal** SharePoint library (`00-raw/` staging) from durable, sanitized institutional intelligence (`01-wiki/` and `02-skills/`). This ensures AI agents operate with high-precision context while maintaining an immutable audit trail and strict data minimization.

---

## 2. System Topology & Tech Stack

| Layer | Technology | Role & Data Classification |
| :--- | :--- | :--- |
| **System of Record & Raw Intake** | Microsoft 365 SharePoint (`RCD Internal`) | **Restricted / Confidential:** Primary vault for all raw company documentation, client transcripts, contracts, and PII under M365 access controls. |
| **Local Staging Buffer** | `company-brain/00-raw/` (Git-Ignored) | **Ephemeral Staging:** Temporary local drop-zone for AI ingestion from `RCD Internal`. Excluded from version control via `.gitignore` and purged post-synthesis. |
| **Compiled Knowledge Base** | `company-brain/01-wiki/` (GitHub Private) | **Internal / Sanitized:** Version-controlled Markdown playbooks, reference architectures, and pseudonymized client learnings. |
| **Agent Capabilities** | `company-brain/02-skills/` (GitHub Private) | **Internal:** Standardized system prompts, Cursor rules, and tool workflows. |
| **Future Execution & App Layer** | Cursor, Replit, Vercel, Supabase | **Production / Staging:** Application runtime and database layer governed by environment-level secret management. |

---

## 3. Repository Structure & Control Files
* **`AGENTS.md`:** Enforces mandatory AI agent behaviors (index-first lookup, PII redaction, pseudonymization using `Client-XXX-00` codes, and zero-secret rules).
* **`index.md`:** Master semantic map enabling deterministic context retrieval without hallucination or file duplication.
* **`log.md`:** Append-only chronological audit ledger recording every structural change and knowledge compilation (`YYYY-MM-DD | [ACTOR] | Summary`).
* **`.gitignore`:** Technical guardrail blocking `00-raw/*`, `.env*`, keys (`*.pem`, `*.key`), local databases (`*.sqlite`, `*.db`), and spreadsheets (`*.csv`, `*.xlsx`) from entering Git history.

---

## 4. Security & Compliance Controls (ISO 27001 / SOC 2 / NZ Privacy Act)

1. **Identity & Access Control (ISO 27001 A.5.15 / SOC 2 CC6.1):**
   * `company-brain` is hosted as a private GitHub repository protected by mandatory Two-Factor Authentication (2FA). Raw artifacts remain protected inside M365 (`RCD Internal`).
2. **Change Management & Auditability (ISO 27001 A.8.32 / SOC 2 CC8.1):**
   * Branch protection rules on `main` strictly **block force pushes** and **restrict branch deletions**, preserving an immutable, cryptographically verifiable Git commit history.
3. **Data Minimization & PII Isolation (NZ Privacy Act 2020 IPP 1–11 / ISO 27001 A.8.11):**
   * Raw client files from `RCD Internal` never enter Git. All client entities documented in `01-wiki/clients/` are pseudonymized unless explicit written consent is recorded.
4. **Zero-Secret Hygiene (ISO 27001 A.8.24 / SOC 2 CC6.7):**
   * API keys, tenant IDs, and connection strings are prohibited from Markdown files and referenced solely via `{{ENV_VAR_NAME}}` placeholders.

---

## 5. Standard Operating Procedure: Knowledge Ingestion (`RCD Internal` → `company-brain`)
1. **Sync:** Access source files from the M365 SharePoint **`RCD Internal`** library via local OneDrive sync.
2. **Stage:** Copy target files into `company-brain/00-raw/`.
3. **Synthesize:** Instruct the AI agent (via Cursor) to process `00-raw/` according to `AGENTS.md`, writing compiled Markdown into `01-wiki/`.
4. **Log & Index:** Verify that the agent updated `index.md` and appended an entry to `log.md`.
5. **Purge & Commit:** Delete the temporary files from `00-raw/`, review the Git diff in GitHub Desktop, and commit to `main`.
