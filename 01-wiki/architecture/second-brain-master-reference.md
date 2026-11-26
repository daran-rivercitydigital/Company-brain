---
id: ARCH-001
title: River City Digital Second Brain Master Reference & System Architecture
category: architecture
status: active
version: 2.1
effective_date: 2026-11-26
compliance_scope: [NZ-Privacy-Act-2020, ISO-27001-2022, SOC-2]
related_docs:
  - 01-wiki/playbooks/second-brain-architecture.md
  - 01-wiki/playbooks/nz-sme-ai-adoption.md
  - 01-wiki/nz-compliance/privacy-security-ai-controls.md
  - 01-wiki/nz-compliance/privacy-data-processing-schedule.md
owner: Chief of Staff & AI Systems Architect
---

# River City Digital — Second Brain Master Reference (`RCD-ARCH-001 v2.1`)

## 1. Executive Summary & Live Deployment Status
River City Digital (Cambridge, New Zealand) operates as an AI-native adoption consultancy powered by an AI agent workforce. Built on Andrej Karpathy’s LLM Wiki pattern using plain-text Markdown and Git version control, `Company-brain` replaces fragmented static repositories with a **compiled, version-controlled institutional memory layer** that agents compile, cross-reference, and maintain continuously.

* **Current Milestone (26 November 2026 — Phase 6 P1–P5 Complete & Verified):**
  * Phases 1–5 (cloud vault, local directory tree, M365 intake bridge, initial playbooks/skills, and Cursor auto-governance) and **Phase 6 Priorities 1–5** are complete and verified.
  * **25 active Markdown knowledge files and reusable agent skills** (`ARCH-001`, `PB-001`, `PB-002`, `SKILL-001`–`SKILL-003`, compliance baselines, WFM specs/runbooks, and `client-wko-01.md`) are compiled, synchronized in `index.md`, logged in `log.md`, and validated via a 3-scenario cross-wiki Brain Test with zero PII or secret leakage.

---

## 2. Live Infrastructure & Environment Topology

| Architectural Layer | Component / Path | Data Classification | Live Configuration & Retention Policy |
| :--- | :--- | :--- | :--- |
| **1. Raw Vault & System of Record** | M365 SharePoint (`RCD Internal`) synced via OneDrive | Restricted / Confidential | Permanent source storage under M365 authentication & AU/NZ tenant controls. Kept strictly **outside** the `.git` directory. |
| **2. Ephemeral Local Staging** | `.../Github/Company-brain/00-raw/` (Git-ignored) | Ephemeral Staging | Excluded via `.gitignore` (`00-raw/*`). Must be manually purged down to `.gitkeep` immediately after synthesis. |
| **3. Compiled Institutional Wiki** | `.../Github/Company-brain/01-wiki/` (`playbooks/`, `architecture/`, `clients/`, `nz-compliance/`) | Internal / Sanitized | Version-controlled Markdown pushed to GitHub `main` (2FA enabled, force-push/deletion blocked). All clients pseudonymized (`Client-XXX-00`). |
| **4. Agent Skills & Governance** | `02-skills/` (`SKILL-001`..`003`), `AGENTS.md`, `index.md`, `log.md`, `.cursor/rules/company-brain.mdc` | Internal / Operational | Deterministic prompts, master catalog, append-only audit log, and `alwaysApply: true` governance rules. |
| **5. Local AI Execution IDE** | Cursor Desktop (Windows Local — *This PC*) | Local Workstation Runtime | Privacy Mode enabled (zero model training); local execution only. Cloud Background Agents prohibited for raw ingestion. |
| **6. Client App Delivery Stack** | GitHub + Supabase (`ap-southeast-2` Sydney) + Vercel + Resend + Sentry | Production / Client App Layer | Decoupled multi-tenant client application stack governed by Row-Level Security (RLS) and `{{ENV_VAR_NAME}}` secret vaults. Replit used only for early PoV prototyping per playbook. |

### Verified Production Directory Tree (25 Active Knowledge & Skill Files)
```text
Company-brain/
├── .cursor/rules/company-brain.mdc              # Always-on Cursor agent governance rule (alwaysApply: true)
├── .gitignore                                   # Security guardrail blocking 00-raw/*, secrets, and local DBs
├── AGENTS.md                                    # Master operating rules & compliance protocols for AI workforce
├── index.md                                     # Master catalog of all 25 active wiki documents and skills
├── log.md                                       # Append-only chronological audit trail
├── 00-raw/                                      # Ephemeral staging drop-zone (Git-ignored; contains .gitkeep only)
├── 01-wiki/
│   ├── playbooks/ (12 files)
│   │   ├── commercial-intro-and-positioning.md
│   │   ├── nz-sme-ai-adoption.md                # PB-002 Flagship NZ SME AI Adoption Playbook
│   │   ├── prospect-qualification.md
│   │   ├── prospect-qualification-validation.md
│   │   ├── rcd-application-foundation-setup-guide.md
│   │   ├── rcd-master-business-architecture.md
│   │   ├── replit-pov-build-and-cursor-migration.md
│   │   ├── second-brain-architecture.md         # PB-001 Official Architecture & Governance Record
│   │   ├── services-agreement-baseline.md
│   │   ├── standing-services-agreement-baseline.md
│   │   ├── wfm-pilot-exceptions-and-margin.md
│   │   └── wfm-standard-operational-runbook.md
│   ├── architecture/ (7 files)
│   │   ├── pov-application-reference-architecture.md
│   │   ├── second-brain-master-reference.md     # ARCH-001 Authoritative System Reference (v2.1)
│   │   ├── technology-stack-requirements.md
│   │   ├── wfm-master-system-and-survey-spec.md
│   │   ├── wfm-primary-friction-record-standard.md
│   │   ├── wfm-stage2-architectural-design-record.md
│   │   └── wfm-survey-questions-schema.md
│   ├── clients/ (1 file)
│   │   └── client-wko-01.md                     # Waikato SME client profile (Stage 1 Paid Pilot)
│   └── nz-compliance/ (2 files)
│       ├── privacy-data-processing-schedule.md
│       └── privacy-security-ai-controls.md
└── 02-skills/ (3 files)
    ├── client-discovery-audit.md                # SKILL-002 Client Discovery & AI Readiness Audit Compiler
    ├── ingest-rcd-doc.md                        # SKILL-001 RCD Internal Document Synthesis & Delta-Sync SOP
    └── session-restart-prompt.md                # SKILL-003 v1.1 Session Restart & Context Bootstrapper
```

---

## 3. Security & Compliance Control Matrix
All Second Brain and client delivery operations map directly to the **NZ Privacy Act 2020 (Information Privacy Principles 1–13)**, **ISO/IEC 27001:2022**, and **SOC 2 Trust Services Criteria** (codified in `01-wiki/nz-compliance/privacy-security-ai-controls.md` and `01-wiki/nz-compliance/privacy-data-processing-schedule.md`):

1. **Access Control & Identity (`ISO 27001 A.5.15/A.5.17` | `SOC 2 CC6.1`):** Private GitHub repository (`daran-rivercitydigital/Company-brain`) protected by mandatory 2FA.
2. **Change Integrity & Audit Trail (`ISO 27001 A.8.32` | `SOC 2 CC8.1`):** GitHub `main` branch ruleset blocks force pushes and deletions; chronological ledger maintained in `log.md`; human review required via `git diff` prior to commit.
3. **Data Minimization & PII Isolation (`NZ Privacy Act 2020 IPP 1–11` | `ISO 27001 A.8.11`):** `.gitignore` blocks `00-raw/*`, `*.csv`, `*.xlsx`, `*.db`, `*.sqlite`. Raw staging files are deleted immediately post-synthesis. All client entities in `01-wiki/clients/` are strictly pseudonymized (`Client-XXX-00`).
4. **Zero-Secret Hygiene (`ISO 27001 A.8.24` | `SOC 2 CC6.7`):** `.gitignore` blocks `.env*`, `*.pem`, `*.key`, `*secret*`, `*credentials*`, `*token*`. Markdown files reference `{{ENV_VAR_NAME}}` placeholders only.
5. **AI Data Residency & HITL Governance (`NZ Privacy Act 2020 IPP 12` | `ISO 27001 A.8.12`):** Cursor Privacy Mode locked ON; client Supabase production workloads pinned to **Sydney (`ap-southeast-2`)**; mandatory human-in-the-loop (HITL) review before external communications or financial/ERP writes commit.

---

## 4. Deployed Governance & Core Workflows
* **Constitution (`AGENTS.md`) & Auto-Rule (`.cursor/rules/company-brain.mdc`):** Enforces index-first lookup, strict PII/secret redaction, `00-raw/` synthesis + purge, and mandatory `index.md` / `log.md` synchronization on every session.
* **Deployed Agent Skills (`02-skills/`):**
  * **`SKILL-001` (`02-skills/ingest-rcd-doc.md` v1.1):** Net-new document synthesis (Mode A) and semantic delta-sync (Mode B) from `00-raw/` into `01-wiki/` with PII/secret stripping and `00-raw/` purge verification.
  * **`SKILL-002` (`02-skills/client-discovery-audit.md` v1.0):** Converts raw discovery transcripts and workflow audit notes into pseudonymized `01-wiki/clients/Client-XXX-00.md` readiness assessments (`/25` composite score, Workflow Opportunity Matrix, and HITL/NZPA 2020 gates).
  * **`SKILL-003` (`02-skills/session-restart-prompt.md` v1.1):** Context-bootstrapping prompt instructing fresh Cursor or external AI sessions to load `index.md`, `01-wiki/playbooks/rcd-master-business-architecture.md`, and `01-wiki/architecture/second-brain-master-reference.md` first.

---

## 5. Section 06 Scaling Roadmap (Phase 6 Execution Status)

| Priority | Action Item | Target Path / Tool | Status & Execution Details |
| :--- | :--- | :--- | :--- |
| **Priority 1 (Immediate)** | Complete Batch Ingestion of `RCD Internal` IP | `00-raw/` -> `01-wiki/` (25 active files) | **COMPLETE (26 Nov 2026).** All core strategy, commercial positioning, WFM architecture/runbooks, agreements, and `ARCH-001` compiled, indexed in `index.md`, and purged from `00-raw/`. |
| **Priority 2 (Week 1–2)** | Build Flagship NZ SME AI Adoption Playbook | `01-wiki/playbooks/nz-sme-ai-adoption.md` (`PB-002`) | **COMPLETE (26 Nov 2026).** Compiled 3-phase NZ SME delivery methodology (AI Readiness Audit -> Controlled Pilot -> Governance & ROI) and consultant checklist. |
| **Priority 3 (Week 2)** | Create NZ Privacy Act & ISO 27001 Baseline | `01-wiki/nz-compliance/privacy-security-ai-controls.md` & `privacy-data-processing-schedule.md` | **COMPLETE (26 Nov 2026).** Security/privacy/AI controls and Data Processing Schedule (DPS) covering IPP 1–13, `ap-southeast-2` residency, retention SLAs, and HITL gates. |
---
id: ARCH-001
title: River City Digital Second Brain Master Reference & System Architecture
category: architecture
status: active
version: 2.0
effective_date: 2026-11-26
compliance_scope: [NZ-Privacy-Act-2020, ISO-27001-2022, SOC-2]
owner: Chief of Staff & AI Systems Architect
---

# River City Digital — Second Brain Master Reference (`RCD-ARCH-001 v2.0`)

## 1. Executive Summary & Architectural Philosophy
River City Digital (Cambridge, New Zealand) operates as an AI-native adoption consultancy powered by an AI agent workforce. The Second Brain replaces fragmented, static document repositories with a **compiled, version-controlled Markdown knowledge base** (`Company-brain`) that agents compile, cross-reference, and maintain continuously.

* **Core Pattern:** Raw documents are staged locally, distilled into structured Markdown files in `01-wiki/`, indexed in `index.md`, logged in `log.md`, and immediately purged from staging.
* **Three-Layer Architecture:**
  1. **Raw Sources (`00-raw/`):** Git-ignored ephemeral staging zone fed from the Microsoft 365 SharePoint `RCD Internal` intake vault via OneDrive.
  2. **The Wiki (`01-wiki/`):** Agent-compiled, LLM-generated Markdown knowledge organized across `playbooks/`, `architecture/`, `clients/`, and `nz-compliance/`.
  3. **The Schema (`AGENTS.md` + `02-skills/`):** Operational constitution, Cursor rules, and reusable agent SOPs.

---

## 2. Live Infrastructure & Environment Topology

| Layer | Component | Live Configuration & Security Posture |
| :--- | :--- | :--- |
| **Source Control** | GitHub (`daran-rivercitydigital/Company-brain`) | Private repository; 2FA enabled; `main` branch ruleset blocking force pushes and deletions. |
| **Local Workstation** | Windows (`.../Github/Company-brain/`) | Managed via GitHub Desktop and Cursor IDE (Free tier, Privacy Mode enabled, local *This PC* execution only). |
| **Intake Bridge** | M365 SharePoint (`RCD Internal`) | Synced via OneDrive strictly **outside** the `.git` directory; copied manually into `00-raw/` for processing. |
| **App Delivery Stack** | GitHub + Supabase + Vercel | Decoupled client delivery stack (Scale Phase); zero production credentials stored in `Company-brain`. |

### Canonical Directory Tree
```text
Company-brain/
├── .cursor/rules/company-brain.mdc   # Auto-loaded Cursor governance (alwaysApply: true)
├── .gitignore                        # Blocks 00-raw/*, .env*, keys, secrets, *.pem, *.pfx
├── AGENTS.md                         # System constitution & 3 core workflows
├── index.md                          # Master catalog of all wiki entries & skills
├── log.md                            # Chronological audit log of ingestions & updates
├── 00-raw/                           # Ephemeral staging (contains .gitkeep only in Git)
├── 01-wiki/
│   ├── playbooks/                    # Operational & delivery methodologies (e.g., PB-001)
│   ├── architecture/                 # Internal technical & agent blueprints (e.g., ARCH-001)
│   ├── clients/                      # Pseudonymized client profiles (Client-XXX-00.md)
│   └── nz-compliance/                # NZ Privacy Act 2020, ISO 27001, SOC 2 controls
└── 02-skills/                        # Reusable agent workflow SOPs (e.g., SKILL-001)
```

---

## 3. Compliance & Security Governance Baseline
All Second Brain operations adhere to the **NZ Privacy Act 2020 (Information Privacy Principles 1–13)**, **ISO/IEC 27001:2022**, and **SOC 2 Trust Services Criteria**:

1. **Zero Secrets in Git:** API keys, tokens, passwords, and connection strings are strictly prohibited; reference environment placeholders (`{{ENV_VAR_NAME}}`) only.
2. **Data Minimization & Sanitization:** Raw files in `00-raw/` are deleted immediately after synthesis into `01-wiki/` (retaining only `.gitkeep`).
3. **Mandatory Pseudonymization:** Client names, personal names, emails, phone numbers, IRD/NZBN numbers, and physical addresses are never written to `01-wiki/` or `log.md`. All client entities use the format `Client-XXX-00` (e.g., `Client-WAI-01`).
4. **Sovereignty & Boundary Controls:** Cursor Privacy Mode remains enabled; raw client PII is never transmitted to unapproved external endpoints.
5. **Human-in-the-Loop Approval:** All agent changes require human review via `git diff` and manual commit/push in GitHub Desktop.

---

## 4. Deployed Governance & Core Workflows
* **Constitution (`AGENTS.md`) & Auto-Rule (`.cursor/rules/company-brain.mdc`):** Enforces three core workflows across every session:
  1. **Ingest:** Read `00-raw/` -> synthesize sanitized Markdown into `01-wiki/` -> update `index.md` & `log.md` -> delete raw file.
  2. **Query:** Read `index.md` first -> load targeted `01-wiki/` pages -> synthesize answers with file citations (and save high-value syntheses back into `01-wiki/`).
  3. **Lint:** Audit for broken `[[wikilinks]]`, stale claims, missing `index.md` entries, or accidental PII/secret leaks.
* **Deployed Assets:**
  * `PB-001` (`01-wiki/playbooks/second-brain-architecture.md`) — Second Brain operational playbook.
  * `ARCH-001` (`01-wiki/architecture/second-brain-master-reference.md`) — Authoritative system architecture & configuration baseline.
  * `SKILL-001` (`02-skills/ingest-rcd-doc.md`) — Standardized document ingestion & sanitization skill.

---

## 5. Section 06 Scaling Roadmap (Phase 6 Execution)
1. **Immediate (Completed):** Complete batch ingestion of core `RCD Internal` company IP and lock in `ARCH-001`.
2. **Priority 2 (Week 1–2):** Compile `01-wiki/playbooks/nz-sme-ai-adoption.md` (Flagship Waikato/NZ SME AI Adoption Playbook: Readiness Audit -> Pilot -> Governance & ROI).
3. **Priority 3 (Week 2):** Compile `01-wiki/nz-compliance/nz-privacy-iso-baseline.md` (Reusable IPP, AU/NZ residency, and human-in-the-loop client checklists).
4. **Priority 4 (Week 2–3):** Deploy `02-skills/client-discovery-audit.md` (Standardized skill converting discovery notes into `01-wiki/clients/Client-XXX-00.md`).
5. **Priority 5 (Week 3–4):** Execute the 'Brain Test' validation against `01-wiki/` and upgrade Cursor tier (Plus or BYOK) for high-volume client delivery.
6. **Future (Scale Phase):** Stand up decoupled client application delivery repos across GitHub, Supabase, and Vercel.
