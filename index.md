# Company Brain — Master Index

> **System Status:** Active | **Compliance Baseline:** NZ Privacy Act 2020, ISO 27001 & SOC 2 Aligned  
> **Rule:** AI agents must update this index whenever files are added, moved, or deprecated.

## Root Governance

* [AGENTS.md](./AGENTS.md) — Operating rules, workflows, and security guardrails for AI agents.
* [log.md](./log.md) — Chronological audit log of repository updates and knowledge ingestion.

## 01-wiki (Compiled Knowledge Base)

## 01-wiki/playbooks/ — Methodologies & Operational Playbooks

- `01-wiki/playbooks/second-brain-architecture.md` — `2026-11-23` | **Playbook** | Core three-layer architecture, agent workflows (Ingest, Query, Lint), security posture, and operating rules for the River City Digital Second Brain.
- `01-wiki/playbooks/rcd-master-business-architecture.md` — `2026-11-23` | **Playbook** | Master business blueprint covering vision, four-layer hybrid service architecture, flagship Workflow Transformation Sprint offer, go-to-market, and 24-month financial/scaling roadmap.
- `01-wiki/playbooks/prospect-qualification.md` — `2026-11-23` | **Playbook** | Discovery and prospect qualification framework for evaluating NZ SME fit, pain points, readiness, and commercial viability.
- `01-wiki/playbooks/services-agreement-baseline.md` — `2026-11-23` | **Playbook** | Baseline services agreement structure, scope boundaries, commercial terms, and delivery governance for River City Digital engagements.
- `01-wiki/playbooks/prospect-qualification-validation.md` — `2026-11-25` | **Playbook** | Validation rules, scoring gates, and qualification checkpoints confirming prospect readiness prior to Sprint commitment.
- `01-wiki/playbooks/standing-services-agreement-baseline.md` — `2026-11-25` | **Playbook** | Master standing services agreement baseline governing ongoing client engagements, SOW structures, and liability boundaries.
- `01-wiki/playbooks/wfm-pilot-exceptions-and-margin.md` — `2026-11-25` | **Playbook** | Operational rules for handling Workflow Manager (WFM) pilot edge-case exceptions and protecting delivery/commercial margin targets.
- `01-wiki/playbooks/commercial-intro-and-positioning.md` — `2026-11-25` | **Playbook** | River City Digital commercial positioning, value proposition messaging, and executive introduction playbook for NZ SMEs.
- `01-wiki/playbooks/wfm-standard-operational-runbook.md` — `2026-11-26` | **Playbook** | Standard operational runbook covering day-to-day execution, monitoring, escalation, and support for WFM deployments.
- `01-wiki/playbooks/replit-pov-build-and-cursor-migration.md` — `2026-11-26` | **Playbook** | Rapid Proof-of-Value (PoV) prototyping workflow in Replit and structured migration path into local Cursor/Git production repositories.
- `01-wiki/playbooks/rcd-application-foundation-setup-guide.md` — `2026-11-26` | **Playbook** | Step-by-step setup guide for provisioning River City Digital’s standardized client application foundation (GitHub, Supabase, Vercel, environment vaults).
- `01-wiki/playbooks/nz-sme-ai-adoption.md` — `2026-11-26` | **Playbook** | Flagship NZ SME AI Adoption Playbook (`PB-002`) detailing the three-phase delivery lifecycle (AI Readiness Audit -> Controlled Pilot -> Governance & ROI) and consultant execution checklist.

---

## 01-wiki/architecture/ — System Designs, Agent Blueprints & Standards

- `01-wiki/architecture/technology-stack-requirements.md` — `2026-11-23` | **Architecture** | Approved technology stack requirements, runtime baselines, and platform constraints for River City Digital builds.
- `01-wiki/architecture/wfm-primary-friction-record-standard.md` — `2026-11-25` | **Architecture** | Canonical schema and data standard for capturing, classifying, and scoring primary workflow friction records during audits.
- `01-wiki/architecture/wfm-master-system-and-survey-spec.md` — `2026-11-26` | **Architecture** | End-to-end Workflow Manager (WFM) system specification and discovery survey architecture.
- `01-wiki/architecture/wfm-stage2-architectural-design-record.md` — `2026-11-26` | **Architecture** | Architectural Design Record (ADR) detailing Stage 2 WFM system components, data flows, and integration boundaries.
- `01-wiki/architecture/wfm-survey-questions-schema.md` — `2026-11-26` | **Architecture** | Structured question schema, validation logic, and scoring mappings powering the WFM discovery survey engine.
- `01-wiki/architecture/pov-application-reference-architecture.md` — `2026-11-26` | **Architecture** | Reference architecture blueprint for rapid Proof-of-Value (PoV) client applications, tenant isolation, and secret management.
- `01-wiki/architecture/second-brain-master-reference.md` — `2026-11-26` | **Architecture** | Authoritative Second Brain Master Reference (`ARCH-001 v2.0`) documenting live GitHub/Cursor/M365 infrastructure, compliance baselines, and the Phase 6 scaling roadmap.

---

## 01-wiki/clients/ — Client Profiles & Engagement Summaries

> *All client entries are strictly pseudonymized (`Client-XXX-00`). No real company names, contact names, or PII are permitted here.*

- `01-wiki/clients/client-wko-01.md` — `2026-11-25` | **Client Profile** | Waikato SME client (`Client-WKO-01`) engagement profile, workflow audit baseline, and pilot architecture scope.

---

## 01-wiki/nz-compliance/ — NZ Privacy Act 2020, ISO 27001 & Security Controls

- `01-wiki/nz-compliance/privacy-security-ai-controls.md` — `2026-11-23` | **Compliance** | Security, privacy, and AI governance controls mapped to NZ Privacy Act 2020, ISO 27001, and SOC 2, including data classification, retention SLAs, residency rules, and human-in-the-loop gates.
- `01-wiki/nz-compliance/privacy-data-processing-schedule.md` — `2026-11-25` | **Compliance** | Standardized Data Processing Schedule (DPS) template governing sub-processors, AU/NZ data residency, breach notification, and NZ Privacy Act 2020 obligations.

---


## 02-skills/ — Reusable Agent Workflow SOPs

- `02-skills/ingest-rcd-doc.md` — `2026-11-25` | **Skill** | Standard operating procedure (`SKILL-001`) for ingesting raw documents from `00-raw/` into sanitized `01-wiki/` markdown files with mandatory PII/secret redaction.
- `02-skills/session-restart-prompt.md` — `2026-11-25` | **Skill** | Standardized context-bootstrapping prompt and workflow for re-initializing AI agent sessions cleanly against `Company-brain`.
- `02-skills/client-discovery-audit.md` — `2026-11-26` | **Skill** | Standardized workflow skill (`SKILL-002`) converting raw client discovery transcripts and audit notes into sanitized, pseudonymized `01-wiki/clients/Client-XXX-00.md` readiness assessments.