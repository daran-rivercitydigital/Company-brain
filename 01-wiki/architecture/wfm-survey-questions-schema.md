# Workflow Friction Assessment (`WFM-0.2`) — Complete 66-Question Survey Schema & Branching Specification

> **Document Status:** Active Survey Instrument (`WFM-0.2`) | **Effective Date:** November 2026 | **Owner:** River City Digital  
> **Source:** `Survey_questions.pdf`  
> **Estimated Completion Time:** 10–15 minutes per respondent  
> **Related Documents:** [Workflow Friction Assessment (WFM v0.2.2) — Master System & Survey Specification](./wfm-master-system-and-survey-spec.md) | [Workflow Friction Assessment (WFM v0.2) — Standard Operational Runbook](../playbooks/wfm-standard-operational-runbook.md)

---

## 1. Survey Governance, Privacy Notice & Global Branching Rules

* **Purpose:** Collect confidential workflow, tooling, AI readiness, and operational friction evidence from client staff to prioritize automation, integration, and process improvements.
* **Privacy & Attribution Controls:**
  * Name (Q2) and work email (Q3) are optional and used solely if targeted clarification is needed (subject to Q66 consent).
  * Client reporting describes workflows, roles, and teams without attributing individual feedback.
  * Raw survey responses are access-controlled and deleted no later than **10 business days** after engagement acceptance.
* **Global Branching Map:**
  * **Q6 (`Consent`):** `Yes` -> proceeds to Section 2 (`Q7`); `No` -> branches directly to **End of Form** (no data ingested).
  * **Q41 (`Add Friction 2?`):** `Yes` -> proceeds to Section 7 (`Q42`); `No` -> skips directly to Section 9 (`Q61`).
  * **Q51 (`Add Friction 3?`):** `Yes` -> proceeds to Section 8 (`Q52`); `No` -> skips directly to Section 9 (`Q61`).

---

## 2. Section 1 — Consent & Identification (`Q1–Q6`)

| Q# | Question Prompt | Input Type | Req. | Options / Validation / Branching | SharePoint Target Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q1** | Engagement ID *(Do not edit this pre-filled code)* | Short Text | Yes | Must contain `ENG-` (pre-filled via URL parameter) | `WFM_Respondents.EngagementID` |
| **Q2** | Your full name *(optional)* | Short Text | No | Free text (PII — stripped before AI synthesis) | `WFM_Respondents.FullName` |
| **Q3** | Your work email *(optional)* | Short Text | No | Free text (PII — stripped before AI synthesis) | `WFM_Respondents.WorkEmail` |
| **Q4** | What is your job title or role? | Short Text | Yes | Free text | `WFM_Respondents.JobTitle` |
| **Q5** | Which team or department do you work in? | Short Text | Yes | Free text | `WFM_Respondents.Department` & `WFM_DiagnosticContext.TeamName` |
| **Q6** | Do you consent to your responses being analysed as part of this workflow assessment? | Single Choice | Yes | `Yes` (proceeds to Q7) \| `No` (**Branches to End of Form**) | `WFM_Respondents.ConsentProvided` |

---

## 3. Section 2 — Work Context (`Q7–Q12`)

| Q# | Question Prompt | Input Type | Req. | Options / Validation | SharePoint Target Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q7** | Briefly describe your main day-to-day responsibilities. | Long Text | Yes | Free text | `WFM_DiagnosticContext.PrimaryResponsibilities` |
| **Q8** | What is your primary working arrangement? | Single Choice | Yes | `Office-based` \| `Remote` \| `Hybrid` \| `Field-based` | `WFM_DiagnosticContext.WorkingLocation` |
| **Q9** | Roughly how many hours do you work in a typical week? | Number | Yes | Numeric range: `1` to `100` | `WFM_DiagnosticContext.WeeklyHours` |
| **Q10** | How would you describe your typical workload pace? | Single Choice | Yes | `Manageable` \| `Busy but sustainable` \| `Frequently overloaded` \| `Consistently unsustainable` | `WFM_DiagnosticContext.WorkloadPace` |
| **Q11** | How often is your work interrupted by urgent requests, chasing information, or context switching? | Single Choice | Yes | `Rarely` \| `Occasionally` \| `Frequently` \| `Constantly` | `WFM_DiagnosticContext.InterruptionFrequency` |
| **Q12** | How often does your work require coordination or hand-offs with other teams? | Single Choice | Yes | `Rarely` \| `Weekly` \| `Several times a week` \| `Daily` \| `Constantly` | `WFM_DiagnosticContext.CollaborationFrequency` |

---

## 4. Section 3 — Applications & Data Handling (`Q13–Q19`)

| Q# | Question Prompt | Input Type | Req. | Options / Validation | SharePoint Target Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q13** | List the main software applications, systems, or spreadsheets you use each week *(separated by commas)*. | Long Text | No | Comma-separated list (split by Power Automate into normalized child rows) | `WFM_Applications.AppName` |
| **Q14** | Which single application or system is most critical to your daily work? | Short Text | Yes | Free text | `WFM_DiagnosticContext.MostCriticalApp` |
| **Q15** | Roughly how many different applications or systems do you use on a typical day? | Single Choice | Yes | `1-3` \| `4-6` \| `7-10` \| `11-15` \| `More than 15` | `WFM_DiagnosticContext.AppCountBand` |
| **Q16** | How often do you have to enter the same information into more than one system? | Single Choice | Yes | `Never` \| `Rarely` \| `Weekly` \| `Daily` \| `Multiple times a day` | `WFM_DiagnosticContext.DuplicateEntryFreq` |
| **Q17** | How often do you manually copy, paste, export, or reformat data between systems or spreadsheets? | Single Choice | Yes | `Never` \| `Rarely` \| `Weekly` \| `Daily` \| `Multiple times a day` | `WFM_DiagnosticContext.ManualTransferFreq` |
| **Q18** | How reliable and responsive are the core systems you rely on? | Single Choice | Yes | `Very reliable` \| `Mostly reliable` \| `Sometimes slow or unreliable` \| `Frequently problematic` | `WFM_DiagnosticContext.SystemRelibility` |
| **Q19** | Do you currently use any AI tools (such as ChatGPT, Microsoft Copilot, or built-in AI features) in your role? | Single Choice | Yes | `Never` \| `Rarely` \| `Weekly` \| `Daily` | `WFM_DiagnosticContext.CurrentAIUsage` |

---

## 5. Section 4 — AI Readiness & Sentiment (`Q20–Q25`)

| Q# | Question Prompt | Input Type | Req. | Options / Validation | SharePoint Target Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q20** | How familiar are you with generative AI tools and what they can do in a workplace setting? | Single Choice | Yes | `Not at all familiar` \| `Slightly familiar` \| `Moderately familiar` \| `Very familiar` | `WFM_DiagnosticContext.AIUsageLevel` |
| **Q21** | How confident would you feel using AI tools safely and effectively if provided with guidance? | Single Choice | Yes | `Not confident` \| `Somewhat confident` \| `Confident` \| `Very confident` | `WFM_DiagnosticContext.AIConfidenceLevel` |
| **Q22** | Overall, how do you feel about AI being introduced to support workflows in your workplace? | Single Choice (5-Point) | Yes | `1 - Very concerned` \| `2 - Somewhat concerned` \| `3 - Neutral` \| `4 - Somewhat positive` \| `5 - Very positive` | `WFM_DiagnosticContext.AIWorkplaceView` |
| **Q23** | Which areas of your work do you think AI or automation could help with most? *(Select all that apply)* | Multi-Select | No | `Drafting emails or documents` \| `Summarising information or meetings` \| `Data entry and formatting` \| `Searching for internal information` \| `Reporting and analysis` \| `Scheduling and follow-ups` \| `Quality checks and validation` \| `Not sure` \| `Other` | `WFM_DiagnosticContext.AIHelpAreas` (JSON array) |
| **Q24** | What concerns, if any, do you have about using AI tools at work? *(Select all that apply)* | Multi-Select | No | `Data privacy and confidentiality` \| `Accuracy and errors` \| `Lack of training or guidance` \| `Unclear company rules` \| `Extra workload to check outputs` \| `Job security` \| `No major concerns` \| `Other` | `WFM_DiagnosticContext.AIConcerns` (JSON array) |
| **Q25** | Would you be open to trialling new AI or workflow automation tools if supported? | Single Choice | Yes | `Yes` \| `Maybe` \| `No` | `WFM_DiagnosticContext.WillingToTrialAI` |

---

## 6. Section 5 — Workflow Frictions Overview (`Q26–Q31`)

| Q# | Question Prompt | Input Type | Req. | Options / Validation | SharePoint Target Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q26** | In one sentence, what is your **#1 biggest workflow friction** or repetitive bottleneck? | Short Text | Yes | Free text | `WFM_DiagnosticContext.TopFriction1Summary` |
| **Q27** | In one sentence, what is your **#2 workflow friction**? *(optional)* | Short Text | No | Free text | `WFM_DiagnosticContext.TopFriction2Summary` |
| **Q28** | In one sentence, what is your **#3 workflow friction**? *(optional)* | Short Text | No | Free text | `WFM_DiagnosticContext.TopFriction3Summary` |
| **Q29** | Across all of these frictions combined, roughly how much time do you lose in a typical week? | Single Choice | Yes | `Less than 1 hour` \| `1-2 hours` \| `3-5 hours` \| `6-10 hours` \| `More than 10 hours` | `WFM_DiagnosticContext.TotalWeeklyTimeLostBand` |
| **Q30** | How much do these workflow frictions affect your ability to do your best work or serve customers? | Single Choice | Yes | `Minor annoyance` \| `Moderate drag` \| `Significant barrier` \| `Major bottleneck` | `WFM_DiagnosticContext.OverallFrictionImpact` |
| **Q31** | If your top workflow frictions were resolved, how much would it improve your day-to-day role? | Single Choice | Yes | `Slightly` \| `Moderately` \| `Significantly` \| `Transformatively` | `WFM_DiagnosticContext.PotentialImprovementLevel` |

---

## 7. Section 6 — Friction Deep Dive 1 (`Q32–Q41`, Mandatory)

*Creates `FrictionNumber = 1` in `WFM_Frictions`.*

| Q# | Question Prompt | Input Type | Req. | Options / Validation / Branching | SharePoint Target Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q32** | **Friction 1 — Short Title:** Give this workflow friction a brief name. | Short Text | Yes | Free text | `WFM_Frictions.FrictionDescription` (Title prefix) |
| **Q33** | **Friction 1 — Detailed Description:** Describe what happens step by step, what triggers it, and why it causes delay or frustration. | Long Text | Yes | Free text | `WFM_Frictions.FrictionDescription` |
| **Q34** | **Friction 1 — Systems & Tools Involved:** Which apps, spreadsheets, forms, or inboxes are involved? | Short Text | Yes | Free text | `WFM_Frictions.ApplicationsInvolved` |
| **Q35** | **Friction 1 — Frequency:** How often does this friction occur for you? | Single Choice | Yes | `Monthly` (`0.25/wk`) \| `Fortnightly` (`0.5/wk`) \| `Weekly` (`1/wk`) \| `Daily` (`5/wk`) \| `Several times daily` (`15/wk`) | `WFM_Frictions.Frequency` (feeds `WeeklyHoursMidpoint`) |
| **Q36** | **Friction 1 — Time Per Occurrence:** Roughly how many minutes does each occurrence take or delay you? | Single Choice | Yes | `Less than 10 minutes` (`5m`) \| `10-20 minutes` (`15m`) \| `20-40 minutes` (`30m`) \| `40-60 minutes` (`50m`) \| `More than 60 minutes` (`75m`) | `WFM_Frictions.DurationBand` (feeds `WeeklyHoursMidpoint`) |
| **Q37** | **Friction 1 — People Affected:** Roughly how many people in your team or organisation experience this same friction? | Single Choice | Yes | `Just me (1)` \| `2-4 people` \| `5-10 people` (`BroadlyAffected`) \| `More than 10 people` (`BroadlyAffected`) | `WFM_Frictions.PeopleAffected` (feeds `TriageFlags`) |
| **Q38** | **Friction 1 — Operational Impact:** What is the impact when this friction happens (e.g., delays, errors, rework, customer impact)? | Single Choice | Yes | `Low` \| `Medium` \| `High` (`HighImpact`) \| `Critical` (`HighImpact`) | `WFM_Frictions.ImpactLevel` (feeds `TriageFlags`) |
| **Q39** | **Friction 1 — Root Cause:** What do you think is the main underlying cause? | Single Choice | Yes | `Manual data entry / copy-paste` \| `Systems not talking to each other` \| `Unclear process or ownership` \| `Missing or inconsistent information from others` \| `Approval bottlenecks` \| `Tool limitations or slow systems` \| `Lack of training` \| `Other` | `WFM_Frictions.RootCause` |
| **Q40** | **Friction 1 — Current Workaround:** How do you currently work around this issue? | Long Text | No | Free text | `WFM_Frictions.CurrentWorkaround` |
| **Q41** | Would you like to report a **second** workflow friction in detail? | Single Choice | Yes | `Yes` (proceeds to Q42) \| `No` (**Branches to Q61**) | Branching trigger (`FrictionNumber = 2`) |

---

## 8. Section 7 — Friction Deep Dive 2 (`Q42–Q51`, Conditional on `Q41 = Yes`)

*Creates `FrictionNumber = 2` in `WFM_Frictions`. Identical field schema and midpoint/triage mappings to Section 6.*

| Q# | Question Prompt | Input Type | Req. | Options / Validation / Branching |
| :--- | :--- | :--- | :--- | :--- |
| **Q42** | **Friction 2 — Short Title:** Give this workflow friction a brief name. | Short Text | Yes | Free text |
| **Q43** | **Friction 2 — Detailed Description:** Describe what happens step by step, what triggers it, and why it causes delay or frustration. | Long Text | Yes | Free text |
| **Q44** | **Friction 2 — Systems & Tools Involved:** Which apps, spreadsheets, forms, or inboxes are involved? | Short Text | Yes | Free text |
| **Q45** | **Friction 2 — Frequency:** How often does this friction occur for you? | Single Choice | Yes | `Monthly` \| `Fortnightly` \| `Weekly` \| `Daily` \| `Several times daily` |
| **Q46** | **Friction 2 — Time Per Occurrence:** Roughly how many minutes does each occurrence take or delay you? | Single Choice | Yes | `Less than 10 minutes` \| `10-20 minutes` \| `20-40 minutes` \| `40-60 minutes` \| `More than 60 minutes` |
| **Q47** | **Friction 2 — People Affected:** Roughly how many people experience this same friction? | Single Choice | Yes | `Just me (1)` \| `2-4 people` \| `5-10 people` \| `More than 10 people` |
| **Q48** | **Friction 2 — Operational Impact:** What is the impact when this friction happens? | Single Choice | Yes | `Low` \| `Medium` \| `High` \| `Critical` |
| **Q49** | **Friction 2 — Root Cause:** What do you think is the main underlying cause? | Single Choice | Yes | Same 8 root-cause options as Q39 |
| **Q50** | **Friction 2 — Current Workaround:** How do you currently work around this issue? | Long Text | No | Free text |
| **Q51** | Would you like to report a **third** workflow friction in detail? | Single Choice | Yes | `Yes` (proceeds to Q52) \| `No` (**Branches to Q61**) |

---

## 9. Section 8 — Friction Deep Dive 3 (`Q52–Q60`, Conditional on `Q51 = Yes`)

*Creates `FrictionNumber = 3` in `WFM_Frictions`. Identical field schema and midpoint/triage mappings to Section 6; advances automatically to Q61.*

| Q# | Question Prompt | Input Type | Req. | Options / Validation |
| :--- | :--- | :--- | :--- | :--- |
| **Q52** | **Friction 3 — Short Title:** Give this workflow friction a brief name. | Short Text | Yes | Free text |
| **Q53** | **Friction 3 — Detailed Description:** Describe what happens step by step, what triggers it, and why it causes delay or frustration. | Long Text | Yes | Free text |
| **Q54** | **Friction 3 — Systems & Tools Involved:** Which apps, spreadsheets, forms, or inboxes are involved? | Short Text | Yes | Free text |
| **Q55** | **Friction 3 — Frequency:** How often does this friction occur for you? | Single Choice | Yes | `Monthly` \| `Fortnightly` \| `Weekly` \| `Daily` \| `Several times daily` |
| **Q56** | **Friction 3 — Time Per Occurrence:** Roughly how many minutes does each occurrence take or delay you? | Single Choice | Yes | `Less than 10 minutes` \| `10-20 minutes` \| `20-40 minutes` \| `40-60 minutes` \| `More than 60 minutes` |
| **Q57** | **Friction 3 — People Affected:** Roughly how many people experience this same friction? | Single Choice | Yes | `Just me (1)` \| `2-4 people` \| `5-10 people` \| `More than 10 people` |
| **Q58** | **Friction 3 — Operational Impact:** What is the impact when this friction happens? | Single Choice | Yes | `Low` \| `Medium` \| `High` \| `Critical` |
| **Q59** | **Friction 3 — Root Cause:** What do you think is the main underlying cause? | Single Choice | Yes | Same 8 root-cause options as Q39 |
| **Q60** | **Friction 3 — Current Workaround:** How do you currently work around this issue? | Long Text | No | Free text |

---

## 10. Section 9 — Recommendations & Closing (`Q61–Q66`)

| Q# | Question Prompt | Input Type | Req. | Options / Validation | SharePoint Target Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q61** | If you could fix or automate **one thing** in your workflow tomorrow, what would deliver the biggest value? | Long Text | Yes | Free text | `WFM_DiagnosticContext.OneThingToImprove` |
| **Q62** | Which type of improvement would help your team most right now? | Single Choice | Yes | `Automation of repetitive tasks` \| `Better integration between systems` \| `Process simplification and clearer rules` \| `Better training and guidance` \| `AI assistant tools for drafting or analysis` | `WFM_DiagnosticContext.PriorityImprovementArea` |
| **Q63** | How much do you think your wider organisation would benefit from targeted workflow automation? | Single Choice | Yes | `Not much` \| `Somewhat` \| `Significantly` \| `Transformatively` | `WFM_DiagnosticContext.OrgAutomationBenefit` |
| **Q64** | How much do you think your wider organisation would benefit from practical, well-governed AI tools? | Single Choice | Yes | `Not much` \| `Somewhat` \| `Significantly` \| `Transformatively` | `WFM_DiagnosticContext.OrgAIBenefit` |
| **Q65** | Is there anything else you would like to share about your workflows, tools, or ideas for improvement? | Long Text | No | Free text | `WFM_DiagnosticContext.AdditionalComments` |
| **Q66** | Are you happy for a River City Digital adviser to contact you briefly if clarification on any of your answers would help? | Single Choice | Yes | `Yes` \| `No` *(Must be `Yes` before any follow-up outreach)* | `WFM_Respondents.FollowUpConsent` |

---

## 11. Survey Interpretation Updates — AI Opportunity Assessment, Managed AI Services & Productisation Strategy

* **Purpose:** Update survey interpretation logic to support AI Opportunity Assessment, Managed AI Services and Productisation Strategy.

* **New Mapping Layer:**
  * Workflow Friction Analysis
  * AI Readiness Analysis
  * AI Opportunity Detection
  * Managed Service Potential Analysis
  * Productisation Potential Analysis

* **New Scoring Domains:**
  * **AI Readiness:**
    * Familiarity
    * Confidence
    * Sentiment
    * Governance Awareness
    * Adoption Willingness
  * **Managed Service Signals:**
    * Long-term support demand
    * Knowledge dependency
    * Ongoing operational complexity
    * Content maintenance needs
    * Policy maintenance requirements
  * **Productisation Signals:**
    * Repeatability
    * Standardisation
    * Cross-customer applicability
    * Industry relevance

