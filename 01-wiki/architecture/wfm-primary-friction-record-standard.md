# Workflow Friction Map: Primary Friction Record Data Standard

> **Document ID:** `WFM-STD-PFR-001` | **Status:** Controlled Design Standard (Agreed Core / Provisional Implementation)  
> **Scope:** Logical specification for the Workflow Friction Map (WFM) MVP and Customer 1 (`Client-WKO-01`) validation.  
> **Related Governance:** [RCD Master Business Architecture](../playbooks/rcd-master-business-architecture.md) | [WFM-001 Controlled Exceptions & Micro-Tier Margin Model](../playbooks/wfm-pilot-exceptions-and-margin.md) | [Technology Stack Requirements](./technology-stack-requirements.md) | [Privacy, Security and AI Control Baseline](../nz-compliance/privacy-security-ai-controls.md) | [Client-WKO-01](../clients/client-wko-01.md)

---

## 1. Definition

A **Primary Friction Record (PFR)** is the master internal case file for one distinguishable workflow friction. It links evidence, operational context, impact, cause hypotheses, calculations, assessment, and disposition without collapsing those components into a single unsupported conclusion.

---

## 2. Minimum Logical Schema

| Data Group | Minimum Content | Governance Status |
| :--- | :--- | :--- |
| **Identity** | Unique PFR ID; engagement/customer reference; record state | Agreed |
| **Workflow context** | Workflow/process; functional area; owner (if known); affected steps | Agreed |
| **Friction definition** | Concise evidence-based friction statement | Agreed |
| **Evidence linkage** | Evidence IDs; source type; confidence; clarification references | Agreed |
| **Operational characteristics** | Frequency; roles/functions affected; systems and data involved | Agreed |
| **Impact** | Supported time, rework, delay, quality, service, or control impact | Agreed |
| **Economic inputs** | Recorded inputs used by deterministic calculations | Agreed |
| **Cause assessment** | Observed cause; cause hypothesis; validation state | Agreed |
| **Constraints and dependencies** | Process, data, system, people, security, privacy, and operational dependencies | Agreed |
| **Assessment state** | Materiality, feasibility, risk, and complexity (when performed) | Agreed |
| **Traceability** | Assumptions, calculation references, changes, and approvals | Agreed |
| **Disposition** | `Consolidate`, `Clarify`, `Assess`, `Promote`, `Defer`, or `Close` | Provisional labels |

---

## 3. Friction Statement Standard

All PFR friction statements must follow the structural formula: **where the friction occurs + what happens + resulting operational effect**.

| Classification | Example | Compliance Note |
| :--- | :--- | :--- |
| **Acceptable** | *"During monthly management reporting, staff manually reconcile and re-key information from inconsistent source files, increasing preparation effort and rework."* | Grounded in observed mechanism and operational impact. |
| **Not acceptable (Solution)** | *"Automate reports with AI."* | Prematurely prescribes a solution inside the problem definition. |
| **Not acceptable (Vague)** | *"Reporting is inefficient."* | Lacks workflow location, mechanism, and measurable effect. |

---

## 4. Consolidation Rule

Associate evidence with the same PFR **only** where River City Digital has reasonable evidence that it relates to substantially the same:
1. Workflow or workflow stage
2. Friction mechanism
3. Business impact
4. Operating context

If uncertain, retain separate candidate records and trigger targeted clarification. The objective is to prevent both duplicate friction records and unjustified consolidation.

---

## 5. PFR Lifecycle Stages

| Stage | Control Gate |
| :--- | :--- |
| **Candidate** | Evidence suggests a distinct friction; not yet approved as a canonical PFR. |
| **Clarify** | Material gaps or conflicts require targeted clarification. |
| **Assess** | Sufficient evidence exists to test materiality, value, feasibility, and risk. |
| **Promote** | River City Digital approves formation of an Opportunity for decision analysis. |
| **Defer** | Retained in the register but not currently assessed or progressed. |
| **Close** | Not material, unsupported, duplicate, or outside scope; closure reason recorded. |

---

## 6. AI and Calculation Controls

In alignment with the [Privacy, Security and AI Control Baseline](../nz-compliance/privacy-security-ai-controls.md):

* **Proposal-Only AI Assistance:** AI may suggest evidence groupings, duplicates, friction wording, missing information, and possible causes. All AI outputs remain proposals until human review.
* **Deterministic Math:** Counts, annualisation, capacity, and economic values must use deterministic formulas and recorded inputs.
* **No AI Estimation of Missing Data:** Missing numbers remain missing. They must not be estimated or hallucinated by AI unless explicitly entered as labelled assumptions and approved by River City Digital.
* **Human Approval Gates:** All consequential promotion, ranking, risk scoring, and client recommendations require explicit River City Digital approval.

---

## 7. Illustrative Worked Example

> **Note:** The example below is illustrative only. It is not customer evidence and does not represent a claim of savings or technical feasibility.

| Component | Illustrative Content |
| :--- | :--- |
| **Evidence A** | *"Every month I export the information from the accounting system."* |
| **Evidence B** | *"Different teams use different spreadsheet layouts."* |
| **Evidence C** | *"Management reporting takes several days."* |
| **PFR Identifier** | `FR-001: Monthly management reporting` |
| **Friction statement** | Staff manually combine and reconcile information from inconsistent sources and formats, increasing preparation effort and rework. |
| **Possible cause** | Lack of standardised reporting inputs and definitions. |
| **Cause status** | Hypothesis; requires validation. |
| **Disposition** | Assess materiality. |
| **Possible later Opportunity** | Standardise and streamline monthly management-report preparation. |
