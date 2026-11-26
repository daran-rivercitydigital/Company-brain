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
