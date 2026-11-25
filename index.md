# Company Brain — Master Index

> **System Status:** Active | **Compliance Baseline:** NZ Privacy Act 2020, ISO 27001 & SOC 2 Aligned  
> **Rule:** AI agents must update this index whenever files are added, moved, or deprecated.

## Root Governance

* [AGENTS.md](./AGENTS.md) — Operating rules, workflows, and security guardrails for AI agents.
* [log.md](./log.md) — Chronological audit log of repository updates and knowledge ingestion.

## 01-wiki (Compiled Knowledge Base)

### Playbooks (`01-wiki/playbooks/`)

* [Second Brain Architecture & Setup Record](./01-wiki/playbooks/second-brain-architecture.md) — Official ISO 27001 / SOC 2 aligned architecture and setup record for this repository.
* [RCD Master Business Architecture](./01-wiki/playbooks/rcd-master-business-architecture.md) — Current operating model, product catalogue, provisional price book, gates and decision standards (source v8.2).
* [Prospect Qualification & Meeting Validation](./01-wiki/playbooks/prospect-qualification-validation.md) — Pre-sales boundary rules, pass/fail qualification gates, and commercial routing matrix.
* [Standing Services Agreement Commercial Baseline](./01-wiki/playbooks/standing-services-agreement-baseline.md) — Master services contract rules, 50/50 payment defaults, 10-day acceptance, AI/privacy controls, and IP protection.
* [WFM-001 Controlled Exceptions & Micro-Tier Margin Model](./01-wiki/playbooks/wfm-pilot-exceptions-and-margin.md) — Pilot exceptions (`CE-001` to `CE-003`), 5-hour Micro-tier unit economics, and pre-launch legal/accounting items.


### Architecture (`01-wiki/architecture/`)

* [Technology Stack Requirements](./01-wiki/architecture/technology-stack-requirements.md) — Microsoft-first operating stack, GitHub control plane, and provisional PoV runtimes including Replit, Vercel and Supabase.
* [Workflow Friction Map: Primary Friction Record Data Standard](./01-wiki/architecture/wfm-primary-friction-record-standard.md) — Logical schema, friction statement standard, lifecycle stages, and deterministic AI/calculation controls for WFM MVP (`WFM-STD-PFR-001`).


### Clients (`01-wiki/clients/`)

* [Client-WKO-01](./01-wiki/clients/client-wko-01.md) — Pseudonymized Waikato accountancy Pilot for the Workflow Friction Map, including open contracting exceptions.

### NZ Compliance (`01-wiki/nz-compliance/`)

* [Privacy, Security and AI Control Baseline](./01-wiki/nz-compliance/privacy-security-ai-controls.md) — Classification, retention, access, residency, AI governance, and incident targets. Not a certification claim.
* [Privacy & Data Processing Baseline (`RCD-PDS-001`)](./01-wiki/nz-compliance/privacy-data-processing-schedule.md) — Standalone NZ Privacy Act 2020, ISO 27001, and SOC 2 data processing schedule for Customer 2+.


## 02-skills (Agent Prompts & SOPs)

* [Ingest RCD Internal Documentation](./02-skills/ingest-rcd-doc.md) — Mandatory sequence for sanitizing SharePoint exports from `00-raw/` into the wiki.
* [Session Handover & External Compiler Restart Prompt (`SKILL-002`)](./02-skills/session-restart-prompt.md) — Copy-pasteable prompt for restarting batch ingestion sessions in external LLM tools with full architectural context.
* [Pre-Sales Discovery Scoring & Commercial Routing (`SKILL-003`)](./02-skills/client-discovery-audit.md) — Evaluates pre-sales discovery notes against the 6 evidence prompts and 7 qualification gates, selects the commercial route, and drafts pseudonymized client profiles.

