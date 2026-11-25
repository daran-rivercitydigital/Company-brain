# Skill: Pre-Sales Discovery Scoring & Commercial Routing (`SKILL-003`)

> **Skill ID:** SKILL-003 | **Version:** 1.0 | **Effective Date:** 2026-11-25  
> **Upstream Playbooks:**  
> * [Prospect Qualification & Meeting Validation](../01-wiki/playbooks/prospect-qualification-validation.md)  
> * [Standing Services Agreement Commercial Baseline](../01-wiki/playbooks/standing-services-agreement-baseline.md)  
> * [WFM-001 Controlled Exceptions & Micro-Tier Margin Model](../01-wiki/playbooks/wfm-pilot-exceptions-and-margin.md)  
> * [Privacy & Data Processing Baseline (`RCD-PDS-001`)](../01-wiki/nz-compliance/privacy-data-processing-schedule.md)

---

## 1. Trigger & Purpose
Run this skill whenever raw discovery call notes, qualification sheets, or pre-sales intake transcripts are staged in `00-raw/` (or pasted in a local/approved session). The agent evaluates commercial fit, flags NZ Privacy Act / delivery risks, selects the commercial route, and drafts a pseudonymized client record ready for **Founder Sign-Off (`Proceed` / `Revise` / `Stop`)**.

---

## 2. Hard Guardrails (Non-Negotiable)
1. **No Free Consulting Boundary:** Never generate free diagnostic analysis, ranked opportunity cards, tool recommendations, or workflow redesigns in pre-sales outputs. Discovery establishes **fit**, **presenting problem**, and **commercial route** only.
2. **Strict PII Redaction & Pseudonymization:** Strip all personal names, email addresses, phone numbers, street addresses, and NZBN/IRD identifiers before writing to `01-wiki/clients/`. Assign a regional pseudonym code (e.g., `Client-WKO-02`, `Client-AKL-01`, `Client-BOP-01`).
3. **Zero Public AI / Local Execution:** Process raw discovery notes only inside approved local or privacy-mode environments.

---

## 3. Execution Steps (Mandatory Sequence)

### Step 1: Context Check
1. Read `index.md` to verify existing client codes in `01-wiki/clients/` and avoid duplicate entries.
2. Read the raw discovery notes provided.

### Step 2: Score the 6 Discovery Evidence Dimensions
Evaluate the raw notes against River City Digital's six core discovery prompts and assign a confidence rating (**High**, **Medium**, **Low**, or **Missing**):

| Dimension | Core Question | Evidence Extracted | Confidence |
| :--- | :--- | :--- | :--- |
| **1. Time Friction** | Where are skilled people losing time? | `[Summarise friction]` | `High / Med / Low / Missing` |
| **2. Outcome** | What business outcome matters most? | `[Summarise target KPI/outcome]` | `High / Med / Low / Missing` |
| **3. Blast Radius** | Which teams, processes, or customers are affected? | `[Summarise scope]` | `High / Med / Low / Missing` |
| **4. Urgency** | Why address this now? | `[Summarise catalyst/deadline]` | `High / Med / Low / Missing` |
| **5. History** | What has already been tried? | `[Summarise prior attempts]` | `High / Med / Low / Missing` |
| **6. Economics** | Is there a genuine budget and decision path? | `[Summarise budget/authority]` | `High / Med / Low / Missing` |

### Step 3: Evaluate Mandatory Pass/Fail Qualification Gates
Score each gate as **PASS**, **CONDITIONAL (Needs Info)**, or **FAIL**:
* **Gate 1 — Clear Problem & Outcome:** Business friction and desired outcome are concrete.
* **Gate 2 — Market & Waikato/NZ Fit:** Aligns with River City Digital's target SME profile.
* **Gate 3 — Capacity Fit:** Deliverable within current Founder capacity without breaching delivery SLAs.
* **Gate 4 — Scope Boundary:** Can be scoped cleanly without giving away free substantive analysis.
* **Gate 5 — Margin & Pricing Floor:** Meets standard **>= 50% gross margin** floor (or >= 40% only if an approved Founding Partner exception applies within Customer 1–3 cohort).
* **Gate 6 — Risk & NZ Privacy Posture:** Data sensitivity is manageable under `RCD-PDS-001` (no unapproved clinical/special-category PII or cross-border blockers).
* **Gate 7 — Decision Authority:** Economic buyer / decision path is identified.

### Step 4: Select Commercial Route
Apply the deterministic routing logic:
* **Workflow Friction Map (WFM) [Default]:** Select when wider evidence is needed across staff/processes, or the opportunity portfolio is unclear. Recommend tier (`Micro` <= 12 staff @ NZD 1,500 + GST standard, or larger tier per architecture).
* **Direct-to-PoV (Exception Only):** Select **only** if the workflow is tightly bounded AND all Joint Investment Gate evidence is already proven (quantified value, owner, technical feasibility, data readiness, risks, human-in-the-loop rules, decision authority).
* **AI Strategy Retainer:** Select when a genuine ongoing governance/advisory need is established.
* **AI Training & Adoption:** Select when a defined team capability/upskilling need is established.
* **No Engagement / Revisit:** Select if any critical Gate (`Gate 1`, `Gate 5`, `Gate 6`, or `Gate 7`) fails.

### Step 5: Generate Outputs & Synchronize Wiki
1. **Create/Merge Client Profile (`01-wiki/clients/client-<region>-<nn>.md`):** Write the sanitized, pseudonymized discovery scorecard, recommended commercial route, open questions, and a pending **Founder Sign-Off Block** (`Decision: [ ] Proceed  [ ] Revise  [ ] Stop`).
2. **Capture Meeting Validation Metrics:** Log (a) propositions immediately understood, (b) high-interest outcomes, (c) objections/risks raised, and (d) willingness-to-pay signals.
3. **Update `index.md` & `log.md`:** Add the new client entry to `index.md` under `### Clients` and append a timestamped audit entry to `log.md`.
4. **Confirm Purge:** Remind the Founder to delete raw discovery notes from `00-raw/` before pushing to GitHub.
