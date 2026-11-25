# Workflow Friction Assessment (WFM v0.2) — Stage 2 Architectural Design & Implementation Record (`WFM_Stage2_Friction_Synthesis_v01`)

> **Document Status:** Active / Verified in Test (`ENG-0003`) | **Version:** v0.2 (Zero-License Hybrid Human-in-the-Loop Architecture) | **Owner:** River City Digital  
> **Source:** `WFM_-_Architectural_design_and_implementation_record.pdf`  
> **Platform Stack:** SharePoint Online (`[RCD_INTERNAL_SITE]`) + Microsoft Power Automate + Microsoft 365 Copilot Chat (Adviser Assisted)  
> **Core Governance Principle:** *"Code calculates. AI explains. The adviser judges."*  
> **Related Documents:** [Workflow Friction Assessment (WFM v0.2.2) — Master System & Survey Specification](./wfm-master-system-and-survey-spec.md) | [PoV Application Reference Architecture](./pov-application-reference-architecture.md) | [RCD Technology Stack Requirements](./tech-stack-requirements.md)

---

## 1. Architectural Purpose & Governance Controls

`WFM_Stage2_Friction_Synthesis_v01` is an on-demand, engagement-isolated synthesis pipeline [1.3.1]. It extracts unanalysed workflow friction evidence for a single client engagement, strips all respondent attribution, packages deterministic time and triage metrics into a structured synthesis prompt, and delivers that prompt packet to the lead adviser for AI-assisted clustering and human judgment [1.3.1].

### Enforced Governance Guardrails
* **Strict Engagement Isolation:** Every SharePoint query filters on `EngagementID eq '[EngagementID]'`, preventing cross-client data bleed [1.3.1].
* **Privacy & Anonymization Gate:** `Data Operation -> Select` actions strip `RespondentID`, respondent names, and contact details before assembling the AI prompt payload [1.3.1].
* **Deterministic Calculation Boundary:** The flow passes pre-computed `WeeklyHoursMidpoint` and `TriageFlags` values from Stage 1 (`WFM_Form_Submission_v01`) without alteration and explicitly instructs the AI never to invent or recalculate numeric hours [1.3.1].
* **Human-in-the-Loop Promotion:** Candidate Primary Friction themes and recommendations remain non-authoritative drafts until reviewed, edited, and approved by a human adviser in `WFM_Recommendations` [1.3.1].

---

## 2. End-to-End Workflow Architecture & Step-by-Step Specification

* **Entry Point:** SharePoint List Action Button (`WFM_Engagements`) [1.3.1]
* **Column Name:** `RunSynthesis` (Single line of text) [1.3.2]
* **UI Mechanism:** SharePoint JSON Column Formatting (`executeFlow` action bound to Flow GUID) rendering a one-click **Run AI Synthesis** button per engagement row [1.3.2].

### Flow Execution Sequence (`WFM_Stage2_Friction_Synthesis_v01`)

| Step | Action Name | Connector / Type | Configuration & Logic | Governance / Data Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **1** | `For a selected item` | SharePoint Trigger | **Site:** `[RCD_INTERNAL_SITE]` \| **List:** `WFM_Engagements` | Captures the clicked engagement row's SharePoint `ID` directly from the list UI [1.3.2]. |
| **2** | `Get item` | SharePoint (`Get item`) | **List:** `WFM_Engagements` \| **Id:** `ID` from Step 1 | Resolves the canonical `EngagementID` (e.g., `ENG-0003`) for downstream OData isolation filters [1.3.2]. |
| **3** | `Get Friction Context` | SharePoint (`Get items`) | **List:** `WFM_Frictions` \| **Filter Query:** `EngagementID eq '[EngagementID]' and AnalysisStatus eq 'Not Analysed'` | Retrieves only unanalysed raw friction evidence belonging to the target engagement [1.3.2]. |
| **4** | `Get Engagement Context` | SharePoint (`Get items`) | **List:** `WFM_DiagnosticContext` \| **Filter Query:** `EngagementID eq '[EngagementID]'` | Retrieves team-level workload pace, AI readiness, and duplicate/manual transfer context [1.3.2]. |
| **5** | `Get Engagement Applications` | SharePoint (`Get items`) | **List:** `WFM_Applications` \| **Filter Query:** `EngagementID eq '[EngagementID]'` | Retrieves the normalized software stack reported across respondents in the engagement [1.3.2]. |
| **6** | `Sanitize Frictions for AI` | Data Operation (`Select`) | **From:** `body/value` (Step 3) \| **Maps:** `FrictionID`, `FrictionDescription`, `Frequency`, `WeeklyHoursMidpoint`, `ImpactLevel`, `PeopleAffected`, `TriageFlags` | **Privacy Gate:** Strips `RespondentID` and metadata before AI exposure [1.3.2, 1.3.3]. |
| **7** | `Sanitize Context for AI` | Data Operation (`Select`) | **From:** `body/value` (Step 4) \| **Maps:** `TeamName`, `AIUsageLevel`, `AppCountBand`, `DuplicateEntryFreq`, `ManualTransferFreq`, `PriorityImprovementArea` | **Privacy Gate:** Strips `RespondentID` while preserving team and tooling friction indicators [1.3.3]. |
| **8** | `Sanitize Apps for AI` | Data Operation (`Select`) | **From:** `body/value` (Step 5) \| **Maps:** `AppName` | **Privacy Gate:** Extracts clean application names without respondent linkage [1.3.3]. |
| **9** | `Compose - Frictions JSON` | Data Operation (`Compose`) | **Inputs:** `body('Sanitize_Frictions_for_AI')` | Helper inspection card isolating sanitized friction JSON for run-history auditing [1.3.3]. |
| **10** | `Compose - Context JSON` | Data Operation (`Compose`) | **Inputs:** `body('Sanitize_Context_for_AI')` | Helper inspection card isolating sanitized diagnostic context JSON [1.3.3]. |
| **11** | `Compose - Apps JSON` | Data Operation (`Compose`) | **Inputs:** `body('Sanitize_Apps_for_AI')` | Helper inspection card isolating sanitized application stack JSON [1.3.3]. |
| **12** | `Compose - Ready-to-Paste AI Prompt` | Data Operation (`Compose`) | Combines `EngagementID` (Step 2), the 4 Governance Rules, and Outputs from Steps 9–11 | Assembles the complete, standardized synthesis prompt for LLM consumption [1.3.3]. |
| **13** | `Compose - HTML Email Body` | Data Operation (`Compose`) | **Expression:** `replace(outputs('Compose_-_Ready-to-Paste_AI_Prompt'), decodeUriComponent('%0A'), '<br>')` | Preserves newline formatting for clean rendering in HTML email clients [1.3.3]. |
| **14** | `Send an email (V2)` | Office 365 Outlook | **To:** `[ADVISER_EMAIL]` \| **Subject:** `WFM Synthesis Packet - [EngagementID]` \| **Body:** Output of Step 13 | Delivers the formatted synthesis packet to the adviser for execution in Microsoft 365 Copilot Chat [1.3.3, 1.3.4]. |
| **15** | `Stage 2 Telemetry` | SharePoint (`Create item`) | **List:** `WFM_Telemetry` \| **Fields:** `EventType = SynthesisRun`, `EngagementID`, `Timestamp`, `Outcome = Success` (`RespondentID` blank) | Records anonymized friction extraction telemetry in `WFM_Telemetry` [1.3.4]. |

---

## 3. Remaining Roadmap Items (Future Enhancements)

The pipeline is operational at **$0 additional license cost** on Microsoft 365 Business Basic + Microsoft 365 Copilot Chat [1.3.1, 1.3.4]. Three self-contained enhancements are defined for transitioning from testing (`ENG-0003`) to full automation [1.3.4]:

### Phase A: Enable Friction Analysis Status Toggling (Post-Testing)
* **Current State:** Intentionally deferred during testing so `ENG-0003` records remain `Not Analysed` for repeated test runs [1.3.4].
* **Implementation:**
  * Add a `Control -> Apply to each` loop after Step 14 iterating over `body/value` from `Get Friction Context` (Step 3), containing a `SharePoint -> Update item` action on `WFM_Frictions` that sets `AnalysisStatus Value = In Review` (or `Analysed`) [1.3.4].
  * Pull `Department` and `Role` (`JobTitle`) into the AI extract (`Sanitize Context for AI`) to support ROI estimation calculations [1.3.4].
* **Value:** Prevents duplicate synthesis packets from re-processing the same raw friction rows on subsequent runs [1.3.4].

### Phase B: Direct AI Connector Integration (Replacing Manual Copy-Paste)
* **Current State:** Step 14 emails the sanitized prompt to the adviser to paste into Microsoft 365 Copilot Chat [1.3.4].
* **Implementation (when an Azure OpenAI, OpenAI API, or AI Builder license is provisioned):**
  1. Insert `Azure OpenAI -> Creates a completion for the chat message` (or `HTTP POST` with `"response_format": {"type": "json_object"}`) directly after Step 11 (`Compose - Apps JSON`), feeding Steps 9–11 as the user message [1.3.4].
  2. Add `Data Operation -> Parse JSON` to validate the structured recommendations array returned by the model [1.3.4].
  3. Add `Control -> Apply to each -> SharePoint -> Create item` targeting `WFM_Recommendations`, automatically writing each candidate recommendation with `Status = Draft`, `EngagementID`, `FrictionID`, `EstimatedBenefit`, and `SchemaVersion = WFM-0.2` [1.3.5].
  4. Update Step 14 (`Send an email (V2)`) to notify the adviser that new `Draft` recommendations are ready for review in `WFM_Recommendations` [1.3.5].

### Phase C: Operational Telemetry & 10-Day Post-Acceptance Purge Flow
* **Retention Purge Automation:** Build a companion `WFM_Engagement_Purge_v01` button flow on `WFM_Engagements` (triggered after customer acceptance) that deletes raw respondent-linked rows in `WFM_Respondents`, `WFM_DiagnosticContext`, `WFM_Applications`, and `WFM_Frictions` for that `EngagementID` while preserving de-identified approved deliverables and telemetry logs [1.3.5].
