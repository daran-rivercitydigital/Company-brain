# Schedule: Privacy & Data Processing Baseline (`RCD-PDS-001`)

> **Document ID:** RCD-PDS-001 | **Version:** 1.0 | **Effective Date:** 2026-11-25  
> **Owner:** River City Digital | **Status:** Commercial Working Baseline (Pending NZ Legal Validation)  
> **Compliance Alignment:** New Zealand Privacy Act 2020 (IPPs 1–13), ISO/IEC 27001:2022, SOC 2 Type I/II

---

## 1. Purpose, Scope & Precedence
This Privacy & Data Processing Schedule (**Schedule**) forms part of the Standing Services Agreement (`RCD-MSA-[nnnn]`) between **River City Digital** (**Processor / Agent**) and the **Customer** (**Agency / Controller**). It governs the collection, storage, AI-assisted processing, retention, and destruction of **Customer Data** and **Personal Information** during any Engagement Schedule (including Workflow Friction Maps, Proofs of Value, Implementations, Retainers, and Training).

* **Precedence:** Where this Schedule conflicts with the Master Services Agreement regarding privacy, security, AI handling, or data retention, this Schedule prevails unless varied in writing by both parties.

---

## 2. Roles & New Zealand Privacy Act 2020 Alignment
* **Agency / Processor Relationship (Section 11):** Under the **Privacy Act 2020**, the Customer remains the primary **Agency** responsible for establishing lawful purpose (IPP 1) and collection authority (IPPs 2–4) for its staff and operational data. River City Digital holds and processes Personal Information solely as an **Agent** on the Customer's documented instructions and does not use or disclose it for River City Digital's own purposes (Section 11(2)).
* **Data Minimisation (IPP 1 & IPP 8):** The Customer must not supply special-category, clinical, payment-card, or unrelated sensitive personal information unless expressly agreed in an Engagement Schedule with heightened controls.
* **Survey Anonymity & Staff Protection:** Where an engagement includes staff surveys or interviews (e.g., Workflow Friction Map), individual responses remain identifiable to River City Digital strictly during active analysis for clarification. Deliverables present aggregated, non-attributed findings only; respondent-level raw responses are never disclosed to Customer leadership.

---

## 3. AI Processing & Zero-Training Guardrails
River City Digital enforces strict technical and contractual controls over all artificial intelligence tooling used during service delivery:

1. **Zero Public Consumer AI:** **Zero Customer Data** or Personal Information may be submitted to free or consumer AI interfaces, public chatbots, or unapproved third-party web tools.
2. **Zero Model Training:** All approved commercial AI environments (including Microsoft 365 tenant services and enterprise API endpoints configured with Zero Data Retention / Privacy Mode) are strictly configured so Customer Data is **never used to train, fine-tune, or improve foundation models**.
3. **Human-in-the-Loop Accountability:** AI tools assist only with transcription, clustering, drafting, and pattern synthesis under direct human supervision. River City Digital reviews and approves all rankings and recommendations; the Customer retains sole decision-making accountability.

---

## 4. Technical & Organisational Security Controls (ISO 27001 / SOC 2)
* **Onshore / Approved Data Residency (IPP 12):** Primary operational storage and survey intake reside within River City Digital's encrypted **Microsoft 365 tenant (New Zealand / Australia cloud regions)**. Any cross-border sub-processor required for a specific Engagement Schedule is disclosed in advance in that Schedule.
* **Tenant & Engagement Segregation:** Each Customer engagement is isolated in dedicated, access-controlled SharePoint/OneDrive containers. Local staging buffers used for structured synthesis are excluded from version control and purged immediately upon compilation.
* **Identity & Access Control:** Protected by mandatory Multi-Factor Authentication (MFA/2FA), least-privilege role assignment, encrypted device storage, and strict prohibition of credentials or secrets in source repositories.

---

## 5. Sub-Processors
The Customer grants general authorisation for River City Digital to engage its core infrastructure sub-processors strictly under equivalent security and zero-training obligations:

| Sub-Processor | Service Role | Primary Hosting / Residency Region |
| :--- | :--- | :--- |
| **Microsoft Corporation (M365)** | Forms, SharePoint, OneDrive, Power Automate, Office | New Zealand / Australia (Azure ANZ) |
| **Approved Enterprise LLM Providers** | Enterprise API / Privacy-Mode Text Synthesis (Zero Training) | Approved commercial endpoints (disclosed per Schedule) |

*(River City Digital will notify the Customer before adding or replacing any sub-processor handling Customer Data.)*

---

## 6. Notifiable Privacy Breaches (Privacy Act 2020 Part 6)
* **Prompt Notification:** River City Digital will notify the Customer **without undue delay** (and within **24 hours**) upon confirming any unauthorised access, disclosure, loss, or alteration of Customer Data.
* **Cooperation & Remediation:** River City Digital will immediately contain the incident, preserve forensic logs, and provide all technical facts reasonably required for the Customer to assess whether the breach meets the **serious harm** threshold for notification to the **Office of the Privacy Commissioner (OPC)** and affected individuals under Part 6 of the Privacy Act 2020.

---

## 7. Retention, Return & 30-Day Destruction Protocol
* **Active Retention:** Customer Data is retained only for the active duration of the Engagement Schedule.
* **30-Day Purge Clock:** Unless a longer period is required by New Zealand law or specified in an Engagement Schedule, River City Digital will permanently delete all raw survey responses, transcripts, and working files within **30 calendar days** of Accepted Delivery (or termination).
* **Data Close-Out Confirmation:** Upon completion of deletion, River City Digital issues a written **Data Close-Out Confirmation** to the Customer. Sanitised, non-identifiable architectural learnings may be retained in River City Digital's internal knowledge base provided zero Customer Confidential Information or Personal Information remains.

---

## 8. Customer Engagement Parameters (Completed per Schedule)
* **Customer Legal Name & NZBN:** `[Customer Name / NZBN]`
* **Engagement Schedule Reference:** `[RCD-XXX-ENG-0000]`
* **Categories of Data Subjects:** `[e.g., Customer employees, operational managers]`
* **Categories of Personal Information:** `[e.g., Business name, work email, role title, workflow friction responses]`
* **Approved Cross-Border Sub-Processors (if any):** `[None / Specify]`
