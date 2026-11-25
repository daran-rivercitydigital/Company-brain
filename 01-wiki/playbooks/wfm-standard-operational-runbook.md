# Workflow Friction Assessment (WFM v0.2) — Standard Operational Runbook

> **Document Status:** Active Operational Runbook (v0.2) | **Effective Date:** November 2026 | **Owner:** River City Digital  
> **Source:** `WFM_-_Standard_Operational_Runbook.pdf`  
> **Platform Stack:** SharePoint Online (`[RCD_INTERNAL_SITE]`) + Microsoft Forms + Power Automate + Microsoft 365 Copilot Chat  
> **Related Documents:** [Workflow Friction Assessment (WFM v0.2.2) — Master System & Survey Specification](../architecture/wfm-master-system-and-survey-spec.md) | [Stage 2 Architectural Design & Implementation Record](../architecture/wfm-stage2-architectural-design-record.md)

---

## 1. Operational Purpose & Core Governance Rules

This runbook governs the end-to-end execution of a **Workflow Friction Assessment (WFM v0.2)** engagement—from engagement creation and survey distribution through Stage 2 AI synthesis, executive report delivery, and post-acceptance data purge.

* **Core Governance Principle:** *"Code calculates. AI explains. The adviser judges."*
* **Zero-Attribution Rule:** Never include respondent names, emails, or `RespondentID` values in AI synthesis prompts or client-facing deliverables.
* **Engagement Isolation Rule:** Verify the canonical `EngagementID` (`ENG-000X`) at every stage before sending invitations, running synthesis, or purging records.
* **10-Day Retention Rule:** Purge all raw respondent-linked records within **10 business days** of written customer acceptance.

---

## 2. Phase 1: Engagement Creation & Survey Distribution

### Step 1.1 — Create the Engagement Record
1. Navigate to the SharePoint list **`WFM_Engagements`** on `[RCD_INTERNAL_SITE]`.
2. Click **+ New** and populate the required engagement metadata:
   * **EngagementName (`Title`):** `[Client Name] — Workflow Friction Assessment`
   * **CustomerName:** Legal or trading name of the client organization.
   * **CustomerIndustry:** Client sector (e.g., Accountancy & Advisory, Legal, Professional Services).
   * **ChampionFirstName / ChampionLastName / ChampionEmail:** Designated client sponsor details.
   * **EngagementStatus:** `Active`
   * **SurveyVersion:** `WFM-0.2`
   * **StartDate / EndDate:** Agreed survey window dates.
   * **TotalInvited:** Exact headcount of staff nominated to receive the survey.
3. Click **Save**.

### Step 1.2 — Capture the Engagement ID & Issue Survey Invitations
1. Wait **1–3 minutes** for the background Power Automate flow (`WFM_EngagementID_Generator`) to run.
2. Refresh `WFM_Engagements` and confirm that:
   * The canonical **`EngagementID`** (e.g., `ENG-0006`) has been populated.
   * An automated email containing the **pre-filled Microsoft Forms URL** (`?[FORM_PREFILL_PARAM]=ENG-000X`) and HTML invitation template has arrived in your adviser inbox.
3. Distribute the survey invitation to nominated client staff:
   * **Direct Distribution:** Send via Outlook using **BCC** for all staff email addresses (strip any forwarding headers before sending).
   * **Champion Distribution:** Forward the clean invitation block and pre-filled URL to the Client AI Adoption Champion for internal distribution.
   * **Critical Check:** Confirm the URL contains the exact `EngagementID` parameter for the active client so all incoming responses map cleanly.

---

## 3. Phase 2: Response Monitoring & Quality Triage

1. Monitor incoming submissions in **`WFM_Respondents`**, **`WFM_DiagnosticContext`**, **`WFM_Applications`**, and **`WFM_Frictions`** filtered by `EngagementID`.
2. Verify intake health in **`WFM_Telemetry`**:
   * Confirm `EventType = Submission` and `Outcome = Success` for each completed survey.
   * If an `Unmatched EngagementID` alert email arrives, inspect the raw Microsoft Forms response, correct the `EngagementID` if a respondent altered Q1, and resubmit the failed run in Power Automate.
3. Review deterministic triage indicators in **`WFM_Frictions`**:
   * **`WeeklyHoursMidpoint`:** Automatically calculated weekly time burden (`(OccurrencesPerWeek * MinutesMidpoint) / 60`).
   * **`TriageFlags`:** Automatically tagged (`HighImpact`, `BroadlyAffected`, `HighWeeklyBurden`).
4. *(Optional)* **Ad-Hoc Evidence Gap Analysis:**
   * If submitted friction descriptions lack sufficient detail or context, click **Run Gap Analysis** (`WFM_Stage2B_FollowUp_Gap_Analysis_v01`) on the engagement row in `WFM_Engagements`.
   * Review the emailed **Evidence Gap & Data Quality Audit** and send targeted follow-up questions **only** to respondents who selected `FollowUpConsent = Yes` (Q66).

---

## 4. Phase 3: Stage 2 AI Synthesis & Adviser Validation

### Step 4.1 — Trigger Stage 2 Synthesis Packet
1. Open **`WFM_Engagements`** and locate the active `ENG-000X` row.
2. Click the blue **Run AI Synthesis** button (`RunSynthesis` column) and confirm flow execution.
3. Open the resulting email (`WFM Synthesis Packet - ENG-000X`) in Outlook.

### Step 4.2 — Run Clustering in Microsoft 365 Copilot Chat
1. Copy the entire sanitized prompt block from the email body (all `RespondentID` and PII fields have already been stripped by the flow).
2. Open **Microsoft 365 Copilot Chat** (using your RCD commercial M365 tenant account—never a personal/consumer AI account).
3. Paste the prompt and execute.

### Step 4.3 — Validate & Promote Recommendations (`Draft` -> `Approved`)
1. Audit Copilot's clustered themes against the deterministic records in **`WFM_Frictions`**:
   * Verify that Copilot has **not** altered, summed incorrectly, or invented any `WeeklyHoursMidpoint` figures.
   * Confirm that zero individual staff names or roles are identifiable in the theme descriptions.
2. Log validated themes into **`WFM_Recommendations`**:
   * Assign `RecommendationID` (`REC-00XX`), `EngagementID`, linked `FrictionID`(s), `RecommendationType` (`Automation`, `Process Improvement`, `Integration`, `AI Enablement`), `ConfidenceLevel`, and `EstimatedBenefit` (strictly grounded in `WeeklyHoursMidpoint`).
   * Save initially as `Status = Draft`; update to **`Status = Approved`** only after lead adviser review.

---

## 5. Phase 4: Deliverable Assembly & Executive Decision Gate

1. Compile the client **Workflow Friction & AI Readiness Report** (Executive PowerPoint / PDF Pack) from approved items in `WFM_Recommendations` and aggregated engagement context.
2. Assign each shortlisted opportunity a clear Investment Gate disposition: **Progress**, **Consider**, or **Defer**.
3. Deliver the pack and facilitate the **60-minute Joint Investment Gate** meeting with the client sponsor/leadership team.
4. Obtain **written confirmation of acceptance** (email or signed gate record) to start the 10-business-day retention countdown.

---

## 6. Phase 5: Post-Acceptance Data Purge & Closure

*Complete this procedure **no later than 10 business days** after written customer acceptance.*

1. Open **`WFM_Engagements`** and verify that all final deliverables are accepted and no active dispute or documented legal hold exists.
2. Click the **Purge Raw Data** button (`PurgeData` column) on the `ENG-000X` row.
3. When prompted for `ConfirmPurge`, type **`PURGE`** (exact uppercase) and submit.
4. Verify complete deletion across all four raw respondent-linked lists filtered by `EngagementID`:
   * `WFM_Frictions` — **0 rows remaining**
   * `WFM_Applications` — **0 rows remaining**
   * `WFM_DiagnosticContext` — **0 rows remaining**
   * `WFM_Respondents` — **0 rows remaining**
5. Confirm **`WFM_Telemetry`** contains a `DataPurge` record with `Outcome = Success` for `ENG-000X`.
6. Update `EngagementStatus` in `WFM_Engagements` to **`Completed`** (or **`Archived`**) while retaining approved de-identified recommendations (`WFM_Recommendations`) and anonymized telemetry (`WFM_Telemetry`).

---

## 7. Exception Handling & Troubleshooting Quick Reference

| Issue / Symptom | Root Cause | Resolution |
| :--- | :--- | :--- |
| **`EngagementID` not generated after 5 minutes** | M365 SharePoint polling delay or flow connection issue | Open Power Automate -> check `WFM_EngagementID_Generator` run history -> inspect error or re-authenticate SharePoint connection and resubmit. |
| **Respondent overwrote Q1 (`EngagementID`)** | Manual edit of pre-filled form field | Correct the `EngagementID` value in the Forms response or `WFM_Respondents` row, then rerun/re-link child records. |
| **Power Automate flow run shows `Failed`** | Transient connector timeout or null field | Open Power Automate -> locate failed run in 28-day history -> inspect red `!` action -> fix underlying data/connection and click **Resubmit** (idempotent). |
| **Purge flow aborts without deleting rows** | Confirmation input did not match exact string `PURGE` | Re-trigger **Purge Raw Data** on the target row and enter `PURGE` with no extra text. |
