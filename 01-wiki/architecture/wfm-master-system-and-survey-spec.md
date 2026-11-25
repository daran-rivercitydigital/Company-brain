# Workflow Friction Assessment (WFM v0.2.2) — Master System & Survey Specification

> **Document Status:** Active (v0.2.2) | **Effective Date:** November 2026 | **Owner:** River City Digital  
> **Source:** `WFM_Master_system_and_Survey_Spec.pdf`  
> **Core Governance Rule:** *"Code calculates. AI explains. The adviser judges."*  
> **Related Documents:** [Commercial Introduction, Positioning & Customer FAQ](../playbooks/commercial-intro-and-positioning.md) | [PoV Application Reference Architecture](./pov-application-reference-architecture.md) | [RCD Technology Stack Requirements](./tech-stack-requirements.md)

---

## 1. Business Context & Governance Boundaries

WFM systematically identifies, quantifies, and prioritizes operational workflow friction points within SME and mid-market client organizations through a standardized 66-question assessment, converting raw employee pain points into evidence-backed automation, integration, and process improvement recommendations.

* **Intended Users:**
  * **Survey Respondents:** Client frontline staff, team leads, and operational managers experiencing day-to-day workflow friction.
  * **Client AI Adoption Champions:** Internal client sponsors coordinating survey distribution and contextualizing operational priorities.
  * **River City Digital Advisers / Analysts:** Consultants configuring engagements, running deterministic ingestion and AI-assisted synthesis, validating Primary Friction Records (PFRs), and delivering executive recommendations.
* **Non-Negotiable Success Criteria:**
  * **100% Engagement Isolation:** Zero cross-client data bleed across ingestion, AI synthesis, and reporting via canonical `EngagementID` filtering.
  * **Deterministic Calculation Accuracy:** 100% of weekly time-loss midpoints (`WeeklyHoursMidpoint`) and triage flags (`TriageFlags`) calculated by code rather than generative AI.
  * **Zero PII Exposure in AI & Telemetry:** Respondent attribution (`RespondentID`, names, emails) stripped prior to AI synthesis and excluded from operational logs.
  * **Timely Data Hygiene:** Raw respondent-linked records purged within **10 business days** of customer acceptance via governed purge automation.

### Version Scope & Roadmap
* **Current Production (`v0.2.2`):** Built entirely on **Microsoft 365 Business Basic** standard connectors (Microsoft Forms, SharePoint Online Lists, Office 365 Outlook, Data Operations) and included **Microsoft 365 Copilot Chat**—requiring zero Premium connectors, Dataverse, or external API credits.
* **Phase 1 (Immediate Hardening):** Enable post-review `AnalysisStatus = In Review` toggling in Stage 2, add Stage 2 telemetry logging, and deploy `WFM_Engagement_Purge_v01`.
* **Phase 2 (Direct AI Connector Integration):** Integrate Azure OpenAI or AI Builder directly into `WFM_Stage2_Friction_Synthesis_v01` with strict JSON schema validation to auto-populate `Draft` entries in `WFM_Recommendations`.
* **Phase 3 (Executive Reporting & Benchmarking):** Connect Power BI / automated Word deliverable generation to `WFM_Recommendations` and aggregated de-identified metrics, plus automated `TotalCompleted` counter updates on `WFM_Engagements`.

---

## 2. End-to-End Operational Lifecycle

```text
[1. Engagement Created] -> [2. Survey Issued] -> [3. Customer Completes Survey]
                                                            |
[6. SharePoint Records] <- [5. Power Automate] <- [4. Forms Response Submitted]
         |
         v
[7. Friction Records] -> [7.1 Gap Analysis (Ad-Hoc)] -> [8. AI Synthesis] -> [9. Recommendations] -> [10. Delivery & 10-Day Purge]
```

1. **Engagement Created:** Adviser creates a row in `WFM_Engagements`; `WFM_EngagementID_Generator` stamps canonical `ENG-000X`.
2. **Survey Issued:** Flow embeds `ENG-000X` into the master Microsoft Forms pre-filled URL and emails an HTML invitation template to the adviser for BCC distribution.
3. **Survey Completed:** Staff verify `ENG-000X` in Q1, provide informed consent in Q6, and complete the 66-question assessment (including up to 3 deep-dive friction reports).
4. **Ingestion (`WFM_Form_Submission_v01`):** Webhook triggers immediate retrieval, validates `EngagementID`, writes normalized records to `WFM_Respondents`, `WFM_DiagnosticContext`, and `WFM_Applications`, calculates deterministic `WeeklyHoursMidpoint` and `TriageFlags` for `WFM_Frictions`, and logs anonymized telemetry in `WFM_Telemetry`.
5. **Ad-Hoc Gap Analysis (`WFM_Stage2B_FollowUp_Gap_Analysis_v01`):** Optional one-click flow isolates unanalysed frictions, strips PII, and generates an internal Evidence Gap & Data Quality Audit, role/team-grouped draft respondent emails (3–4 targeted questions), and a SharePoint Note Capture Template.
6. **AI Synthesis (`WFM_Stage2_Friction_Synthesis_v01`):** One-click SharePoint button strips `RespondentID` and PII, packaging anonymized JSON arrays (`Frictions`, `DiagnosticContext`, `Applications`) into an email prompt for clustering in **Microsoft 365 Copilot Chat**.
7. **Validation & Delivery:** Adviser validates Primary Friction themes against deterministic `WeeklyHoursMidpoint` metrics, logs prioritized items in `WFM_Recommendations` (`Draft` -> `Approved`), and compiles the client *Workflow Friction & AI Readiness Report*.
8. **Post-Acceptance Purge (`WFM_Engagement_Purge_v01`):** Within **10 business days** of written customer acceptance, adviser runs the purge flow (confirming `PURGE`) to delete all raw respondent-linked records while preserving approved recommendations and telemetry logs.

---

## 3. Survey Specification (66 Questions)

| Section | Name | Question Range | Purpose & Key Rules |
| :--- | :--- | :--- | :--- |
| **1** | Consent & Identification | **Q1–Q6** | Q1 pre-filled `ENG-000X` (`Contains ENG-`); Q2 Name & Q3 Email optional (stripped before AI); Q4 Role & Q5 Team mandatory; **Q6 Consent** (`Yes/No` — if `No`, branches directly to end with no processing). |
| **2** | Work Context | **Q7–Q12** | Daily responsibilities (Q7), work setting (Q8: Office/Remote/Hybrid/Field-based), weekly hours (Q9: numeric `1–100`), workload pace (Q10), interruption frequency (Q11), cross-team coordination frequency (Q12). |
| **3** | Applications | **Q13–Q19** | Comma-separated weekly apps (Q13, optional, split by flow into `WFM_Applications`), most critical tool (Q14), daily tool count band (Q15: `1-3` to `More than 15`), duplicate entry freq (Q16), manual copy/paste freq (Q17), system reliability (Q18), current AI use (Q19). |
| **4** | AI Readiness | **Q20–Q25** | AI familiarity (Q20), confidence (Q21), workplace sentiment 5-point scale (Q22), multi-select AI help areas (Q23 -> JSON array), multi-select AI concerns (Q24 -> JSON array), willingness to trial AI (Q25: `Yes/Maybe/No`). |
| **5** | Workflow Frictions (Overview) | **Q26–Q31** | Top 1–3 friction summaries (Q26 mandatory; Q27–Q28 optional), combined weekly time lost band (Q29), overall impact on best work (Q30), perceived role improvement potential (Q31). |
| **6** | Friction Deep Dive 1 | **Q32–Q41** | Mandatory primary friction: Title (Q32), detail (Q33), tools (Q34), frequency (Q35: Monthly/Fortnightly/Weekly/Daily/Several times daily), minutes per occurrence (Q36: `<10` to `>60`), people affected (Q37), operational impact (Q38: Low/Medium/High/Critical), primary root cause (Q39), workaround (Q40), **Q41 Branching** (`Yes` -> Q42; `No` -> Q61). |
| **7** | Friction Deep Dive 2 | **Q42–Q51** | Conditional on `Q41 = Yes` (`FrictionNumber = 2`). Identical schema to Q32–Q40; **Q51 Branching** (`Yes` -> Q52; `No` -> Q61). |
| **8** | Friction Deep Dive 3 | **Q52–Q60** | Conditional on `Q51 = Yes` (`FrictionNumber = 3`). Identical schema to Q32–Q40; advances to Q61. |
| **9** | Recommendations & Closing | **Q61–Q66** | Single highest-value fix (Q61), priority improvement category (Q62: Automation / System integration / Process simplification / Better training/guidance / AI assistant tools), org automation benefit (Q63), org AI benefit (Q64), open remarks (Q65), **Q66 Follow-up Consent** (`Yes/No` required before any interview outreach). |

---

## 4. SharePoint Data Architecture & Entity Relationships

*To avoid SharePoint's 5,000-item list view threshold and delegation limits, all foreign keys are stored as indexed **Single Line of Text** columns rather than SharePoint Lookup columns.*

### Entity Relationship Diagram
```text
WFM_Engagements (PK: EngagementID, e.g., ENG-0006)
  └── 1 : N ──> WFM_Respondents (PK: RespondentID, e.g., RSP-0035 | FK: EngagementID)
                  ├── 1 : 1 ──> WFM_DiagnosticContext (FK: RespondentID, EngagementID)
                  ├── 1 : N ──> WFM_Applications (PK: ApplicationID, e.g., APP-0051 | FK: RespondentID, EngagementID)
                  └── 1 : 1..3 -> WFM_Frictions (PK: FrictionID, e.g., FR-0018 | FK: RespondentID, EngagementID)
                                    └── N : M (Logical) ──> WFM_Recommendations (PK: RecommendationID, e.g., REC-0001 | FK: EngagementID, FrictionID)
  └── 1 : N ──> WFM_Telemetry (FK: EngagementID — RespondentID intentionally blank)
```

### SharePoint Lists Summary
1. **`WFM_Engagements`:** `EngagementID` (`ENG-000X`), `Title` (EngagementName), `CustomerName`, `CustomerIndustry`, `ChampionFirstName`, `ChampionLastName`, `ChampionEmail`, `EngagementStatus` (`Planned`, `Active`, `In Analysis`, `Completed`, `Archived`), `SurveyVersion` (`WFM-0.2`), `StartDate`, `EndDate`, `TotalInvited`, `TotalCompleted`, `Notes`, and JSON action buttons (`RunSynthesis`, `PurgeData`, `RunGapAnalysis`).
2. **`WFM_Respondents`:** `RespondentID` (`RSP-00XX`), `EngagementID`, `FullName` (Q2, PII), `WorkEmail` (Q3, PII), `JobTitle` (Q4), `Department` (Q5), `ConsentProvided` (Q6), `FollowUpConsent` (Q66), `SubmittedAt`, `SurveyVersion` (`WFM-0.2`), `MappingVersion` (`MAP-0.2`), `RangeMappingVersion` (`RNG-0.2`).
3. **`WFM_DiagnosticContext`:** `Title` (`CTX-RSP-00XX`), `RespondentID`, `EngagementID`, `TeamName`, `PrimaryResponsibilities`, `WorkingLocation`, `WeeklyHours`, `WorkloadPace`, `InterruptionFrequency`, `CollaborationFrequency`, `MostCriticalApp`, `AppCountBand`, `DuplicateEntryFreq`, `ManualTransferFreq`, `SystemRelibility`, `CurrentAIUsage`, `AIUsageLevel`, `AIConfidenceLevel`, `AIWorkplaceView`, `AIHelpAreas`, `AIConcerns`, `WillingToTrialAI`, `TopFriction1Summary`–`3Summary`, `TotalWeeklyTimeLostBand`, `OverallFrictionImpact`, `PotentialImprovementLevel`, `OneThingToImprove`, `PriorityImprovementArea`, `OrgAutomationBenefit`, `OrgAIBenefit`, `AdditionalComments`, `SchemaVersion`, `Gap responses`.
4. **`WFM_Applications`:** `ApplicationID` (`APP-00XX`), `RespondentID`, `EngagementID`, `AppName` (`trim(item())` from Q13), `SchemaVersion`.
5. **`WFM_Frictions`:** `FrictionID` (`FR-00XX`), `RespondentID`, `EngagementID`, `FrictionNumber` (`1`–`3`), `FrictionDescription`, `ApplicationsInvolved`, `Frequency`, `DurationBand`, `WeeklyHoursMidpoint` (`(OccurrencesPerWeek * MinutesMidpoint) / 60`), `PeopleAffected`, `ImpactLevel`, `RootCause`, `CurrentWorkaround`, `TriageFlags` (space-delimited: `HighImpact` if High/Critical, `BroadlyAffected` if `>= 5` people, `HighWeeklyBurden`), `AnalysisStatus` (`Not Analysed`, `In Review`, `Analysed`, `Excluded`), `SchemaVersion`.
6. **`WFM_Recommendations`:** `RecommendationID` (`REC-00XX`), `EngagementID`, `FrictionID`, `RecommendationType` (`Automation`, `Process Improvement`, `Integration`, `AI Enablement`), `RecommendationTitle`, `RecommendationSummary`, `ConfidenceLevel` (`High`, `Medium`, `Low`), `EstimatedBenefit` (strictly grounded in `WeeklyHoursMidpoint`), `Status` (`Draft`, `Approved`, `Rejected`, `Delivered`), `AnalystNotes`, `SchemaVersion`.
7. **`WFM_Telemetry`:** `Title` (`TEL-yyyyMMdd-HHmmss`), `Timestamp`, `FlowName`, `EventType` (`Submission`, `Synthesis`, `DataPurge`, `Error`), `Outcome` (`Success`, `Failure`, `Warning`), `Details` (anonymized counts/status only), `EngagementID`, `RespondentID` (always blank), `SchemaVersion`.

---

## 5. Power Automate Flows & ID Standards

### Deterministic ID Expressions (Zero-Collision via Atomic SharePoint `ID`)
* **Engagement:** `concat('ENG-', formatNumber(triggerOutputs()?['body/ID'], '0000'))`
* **Respondent:** `concat('RSP-', formatNumber(outputs('Create_Respondent_Record')?['body/ID'], '0000'))`
* **Application:** `concat('APP-', formatNumber(outputs('Create_item_-_Applications')?['body/ID'], '0000'))`
* **Friction:** `concat('FR-', formatNumber(outputs('Create_item_(Friction_X)')?['body/ID'], '0000'))`
* **Recommendation:** `concat('REC-', formatNumber(item_ID, '0000'))`
* **Telemetry:** `concat('TEL-', formatDateTime(utcNow(), 'yyyyMMdd-HHmmss'))`

### Core Power Automate Workflows

| Flow Name | Trigger | Core Function & Guardrails |
| :--- | :--- | :--- |
| **`WFM_EngagementID_Generator`** | SharePoint: When an item is created (`WFM_Engagements`) | Stamps `ENG-000X`, builds pre-filled Forms URL (`?[FORM_PREFILL_PARAM]=ENG-000X`), and emails HTML invitation button to adviser. *(Allow 1–3 min M365 polling latency).* |
| **`WFM_Form_Submission_v01`** | Microsoft Forms: New response submitted | Validates `EngagementID` (alerts adviser if unmatched), creates `RSP-00XX` + `DiagnosticContext`, null-safe splits Q13 (`trim(coalesce(..., ''))`) into `WFM_Applications`, calculates `WeeklyHoursMidpoint` (`div(mul(F_Frequency, F_Minutes), 60)`) & `TriageFlags` for Frictions 1–3, and logs `Submission` telemetry. |
| **`WFM_Stage2_Friction_Synthesis_v01`** | SharePoint: For a selected item (`RunSynthesis` button) | OData filters `EngagementID eq '[EngagementID]' and AnalysisStatus eq 'Not Analysed'`, uses `Select` cards (`item()?['...']`) to strip `RespondentID`/PII, formats HTML prompt packet (`replace(..., decodeUriComponent('%0A'), '<br>')`), and emails adviser for Copilot Chat synthesis. |
| **`WFM_Stage2B_FollowUp_Gap_Analysis_v01`** | SharePoint: For a selected item (`RunGapAnalysis` button) | Cloned from Stage 2 with identical `EngagementID` isolation and PII-stripping `Select` cards; generates gap audit, draft follow-up emails, and SharePoint note capture template. |
| **`WFM_Engagement_Purge_v01`** | SharePoint: For a selected item (`PurgeData` button + `ConfirmPurge` input) | Verifies `toUpper(trim(coalesce(triggerBody()?['text'], ''))) == 'PURGE'` (aborts otherwise), deletes all rows for `EngagementID` across `WFM_Frictions`, `WFM_Applications`, `WFM_DiagnosticContext`, and `WFM_Respondents`, and logs `DataPurge` telemetry. |

---

## 6. Security Matrix, AI Guardrails & Operational SOPs

### Role-Based Access Control (RBAC)

| Role | Create Engagements | View Master Survey | Access Raw Responses | Modify Lists | Run Flows |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RCD Lead Adviser / Admin** | Yes | Yes (Edit & Pre-fill) | Yes (Full Site Owner/Member) | Yes | Yes (Owner / Co-owner) |
| **RCD Analyst / Consultant** | Yes | Yes (View / Share Link) | Yes (Site Member) | Yes (`Draft`/`Review` status) | Yes (Run-only on buttons) |
| **Client AI Champion** | No | Yes (Receives invite template) | No | No | No |
| **Survey Respondent** | No | Yes (Via pre-filled URL) | No (Write-only via Forms) | No | No (Implicit on submit) |

### AI Prompt Governance Rules
1. Never invent, recalculate, or alter numeric hours (reference only input `WeeklyHoursMidpoint` values).
2. Never infer or mention individual respondent identities.
3. Group recurring patterns into candidate Primary Friction themes across `Automation`, `Process Improvement`, or `Integration`.
4. Ground every estimated benefit statement strictly in the deterministic input metrics.
5. Every AI-generated recommendation enters `WFM_Recommendations` as `Draft` and requires explicit human adviser approval (`Status = Approved`) before client inclusion.

### Standard Operating Procedures (SOPs)
* **SOP 1 (Create & Issue):** Create row in `WFM_Engagements` (`Status = Active`, `SurveyVersion = WFM-0.2`) -> wait 1–2 min for `ENG-000X` -> forward received invitation email using **BCC** for staff addresses (strip forwarding header).
* **SOP 2 (Stage 2 AI Synthesis):** Click blue **Run AI Synthesis** button on `ENG-000X` -> copy prompt from Outlook email into Microsoft 365 Copilot Chat -> validate clusters against `WeeklyHoursMidpoint` -> log in `WFM_Recommendations` (`Draft` -> `Approved`).
* **SOP 3 (Recover Failed Flow):** Open Power Automate -> inspect 28-day run history for failed run -> inspect red `!` error card -> click **Resubmit** once transient/schema issue is resolved to replay original trigger payload safely.
* **SOP 4 (10-Day Post-Acceptance Purge):** Confirm written customer acceptance ($\le 10$ business days) -> click **Purge Raw Data** -> enter `PURGE` -> verify `DataPurge (Success)` row in `WFM_Telemetry` and zero remaining rows in `WFM_Respondents`, `WFM_DiagnosticContext`, `WFM_Applications`, and `WFM_Frictions`.
