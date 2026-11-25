# Playbook: WFM-001 Controlled Exceptions & Micro-Tier Margin Model

> **Source Artefact:** WFM-001 Controlled Exception Register and Alignment Check v0.2 (2026-11-10)  
> **Authority:** Subordinate to RCD Master Business Architecture; applies strictly to Pilot Engagement (`Client-WKO-01`)  
> **Confidentiality:** Internal commercial & margin model — never include in customer-facing documents.

---

## 1. Pilot Controlled Exceptions (`CE-001` to `CE-003`)

| Exception ID | Standard Departed From | Pilot (`Client-WKO-01`) Position | Risk Treatment & Expiry Gate |
| :--- | :--- | :--- | :--- |
| **CE-001** | 50% upfront payment prior to capacity reservation / delivery start. | **0% upfront; 100% invoiced on completion of Executive Review Workshop** (14-day terms). | Customer restricted to review-only licence until paid; review/retire exception model after Customer 3. |
| **CE-002** | Incorporate `River City Digital Ltd` prior to first commercial delivery. | Contract and deliver pre-incorporation as sole trader; incorporate after Pilot completes. | Personal liability capped at Contracted Fee (subject to legal review); fresh agreement upon incorporation (no novation). |
| **CE-003** | Bind Professional Indemnity (PI) & Cyber insurance before delivery. | Deliver Micro engagement without PI/Cyber cover, with explicit written customer disclosure and acknowledgement. | Strict data minimisation, NZ-only M365 storage, 30-day deletion clock, no public AI; obtain broker quote before PoV/Implementation. |

*Note on Privacy Schedule:* Integrated privacy terms inside the Agreement/Schedule are approved provisionally for Customer 1; a standalone **Privacy & Data Processing Schedule** must be created before Customer 2.

---

## 2. Micro-Tier Unit Economics & Margin Guardrails

* **Standard Book Price (Micro Tier):** NZD 1,500 + GST
* **Founding Partner Discount (20%):** -NZD 300 (or NZD 250 on NZD 1,250 list variant) -> **Pilot Fee: NZD 1,200 + GST** (12-month discount eligibility on eligible services, excluding Retainers, Training, and pass-through costs, contingent on structured feedback at kick-off, delivery, and 12 months).
* **Cost Model (5-Hour Founder Ceiling):** 5 hours @ NZD 125/hr (NZD 625) + 5% tech allowance on book price (NZD 75) = **NZD 700 total COGS**.

| Scenario | Contracted Fee | Modelled COGS | Gross Margin | Policy Threshold Check |
| :--- | :--- | :--- | :--- | :--- |
| **Standard Book Price (5 hrs)** | NZD 1,500 | NZD 700 | **53.3%** | Passes standard >= 50% floor |
| **Founding Partner (5 hrs)** | NZD 1,200 | NZD 700 | **41.7%** | Passes >= 40% exception floor (10-min buffer only) |
| **Founding Partner (6 hrs)** | NZD 1,200 | NZD 825 | **31.3%** | **Fails** exception floor (6th hour absorbed by RCD) |

**Operational Rule:** Log all Pilot delivery hours against the 5-hour ceiling in the Investment Tracker (`Customer Delivery COGS`, Cohort `Customer 1`, Product `Workflow Friction Map`).

---

## 3. Open Pre-Launch Legal & Accounting Checklist
* **NZ Commercial/Privacy Lawyer:** Validate liability cap (NZD 1,200 sole trader without insurance), 2x privacy carve-out, stop-partway stage table, deemed acceptance, survey privacy notice, and entity transition terms.
* **Accountant:** Confirm GST registration status before issuing first invoice (do not charge GST until registered) and advise on sole-trader-to-company IP/record transfer.
