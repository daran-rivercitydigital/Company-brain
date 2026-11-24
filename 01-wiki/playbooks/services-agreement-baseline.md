# Playbook: Services Agreement Baseline

> **Sources:** Services Agreement commercial working draft v0.2 (9 November 2026); WFM-001 Controlled Exception Register v0.2 (10 November 2026)  
> **Compiled:** 2026-11-23 | **Status:** Not approved for signature  
> **Authority:** [Master Business Architecture](./rcd-master-business-architecture.md) §5.1, §11 and §14. Where this draft and v8.2 conflict, v8.2 governs until a lawyer-settled clause replaces it  
> **Pilot application:** [Client-WKO-01](../clients/client-wko-01.md)  
> **Controls:** [Privacy, Security and AI Controls](../nz-compliance/privacy-security-ai-controls.md)

This is the reusable standing-terms model. Engagement-specific variations belong in an Engagement Schedule, and only by naming the clause varied. Bracketed and OPEN provisions are not agreed. A qualified New Zealand commercial and privacy lawyer must settle them before any signature. This article is an operating extract, not a signable contract and not legal advice.

Personal names, contact details and the NZBN left open in the source are omitted.

## 1. Document order and formation

If documents conflict, the Engagement Schedule prevails for that engagement only, then this Agreement, then any referenced supporting document.

* The Agreement authorises no work by itself. Each Workflow Friction Map, Proof-of-Value, implementation, managed service, retainer or training engagement needs its own Schedule, signed or accepted in writing.
* No later stage is automatic.
* Services are performed with reasonable care and skill. Dates are estimates unless a Schedule names a fixed date.
* Delivery starts on the Assessment Ready Date defined in the Schedule.
* RCD may rely on customer information and will identify material assumptions and evidence limitations where reasonably practicable.
* Subcontractors are permitted. RCD stays responsible and must pass confidentiality, privacy and security duties to them. The draft does not require customer disclosure. The architecture does require disclosure of partners who access systems or data. Keep the architecture duty until the lawyer settles the clause.
* Each Schedule states, in plain language, the deliverables, expected timeframe, customer inputs, and limits on clarification, revisions and meeting time.

Business Day means a day other than Saturday, Sunday or a public holiday observed in Auckland.

## 2. Definitions that the architecture did not yet fix

The architecture uses "accepted delivery" without a review period. The draft supplies these working definitions. They are contract defaults, not a new architecture decision.

| Term | Working meaning |
| --- | --- |
| Review Period | Ten Business Days starting the day after RCD notifies the customer that a Deliverable is ready for review, unless the Schedule states another period |
| Material Non-Conformance | Failure to meet the express scope or acceptance criteria. Disagreement with a professional judgement, ranking or recommendation is not, by itself, a non-conformance |
| Accepted Delivery | The earlier of written acceptance and the last day of the Review Period if no Material Non-Conformance notice was given |
| Principal Deliverable | The Schedule names which deliverable's acceptance is Accepted Delivery when several outputs exist |
| Joint Investment Gate | A facilitated meeting to present ranked recommendations and let the customer decide what to pursue, hold or drop. Attendance commits neither party to later work |
| Permitted Recipient | A professional adviser, or a provider engaged to advise on or implement the recommendations, bound by a professional or written confidentiality duty |
| RCD Background IP | Methods, frameworks, scoring logic, templates, tools, know-how and reusable components existing before, or developed independently of, the engagement |

A Joint Investment Gate, readout or data close-out does not extend the Review Period or condition acceptance unless the Schedule says so.

Correction of a substantiated in-scope Material Non-Conformance is followed by a new Review Period on the corrected deliverable only. The suggested length of that second period is five Business Days and is OPEN.

## 3. Payment, change, suspension and exit

Standing position, unless a Schedule expressly names clause 5.3 or 5.4 and states the replacement:

* Fees are in New Zealand dollars and exclude GST unless stated otherwise.
* Pay a correct invoice within 14 calendar days, without set-off except where the law requires it.
* Fixed-price work is 50% upfront. Engagements scheduled to finish within 30 calendar days invoice the remainder on Accepted Delivery. Longer engagements use the Schedule milestones.
* Do not reserve capacity or start delivery until the upfront amount has cleared and the Assessment Ready Date conditions are met.
* A non-refundable capacity reservation applies only if the Schedule expressly states it.
* Pass-through costs, licences, consumption and travel are extra and are not discounted unless the Schedule says so.
* If an undisputed amount is more than seven days overdue, RCD may suspend the affected services after written notice. Interest, collection costs and the exact notice mechanics are OPEN.
* A material change to scope, participants, assumptions, deliverables, dates or dependencies needs a written Change Request stating the change, reason, fee impact, timing impact and any changed risk or acceptance criteria. Work on the change waits for both parties' written approval.

Stopping before Accepted Delivery, unless the Schedule says otherwise:

| Who stops | Working money outcome | Status |
| --- | --- | --- |
| Customer, or RCD for the customer's breach | Customer pays for services performed to the end date, plus pre-approved committed non-cancellable third-party costs, up to the Contracted Fee. Value by the Schedule's stage table or, if none, in proportion to stages completed. Amounts already paid are applied first. Refund any excess except a stated non-refundable capacity reservation | OPEN for enforceability |
| RCD other than for breach or non-payment, or the customer for RCD's breach | Refund amounts paid for services not delivered. Do not invoice undelivered work. Whether RCD may invoice for stages already delivered in usable form is OPEN | OPEN |

Rescheduling baseline, OPEN for the lawyer: no charge with at least five Business Days' notice. Later customer changes may incur 50% of the affected fees, or 100% within two Business Days, with reasonable treatment of genuine exceptional circumstances.

Either party may end the master agreement on 30 days' written notice. Existing Schedules continue unless ended separately. A Schedule may be ended for material breach not remedied within 10 Business Days, or immediately for insolvency or a breach that cannot be remedied. RCD may also suspend to protect systems, customer data or people.

Deletion timing on an early end runs from the end date. See the [control baseline](../nz-compliance/privacy-security-ai-controls.md).

## 4. Privacy, AI, IP and liability

These clauses are in the working draft and still need qualified New Zealand review. They do not certify anything.

* Each party complies with applicable New Zealand privacy law. The clause is not a certification or attestation.
* Minimise customer data, separate it by customer and engagement, apply least privilege, and use it only to provide the services and meet lawful obligations.
* Do not place customer data in public consumer AI services or allow it to train public models.
* The Schedule names approved tools and providers, including any AI service, where data is processed and stored, including whether that is outside New Zealand, and the retention period and deletion date.
* Survey responses may stay identifiable to RCD so RCD can clarify them. Deliverables do not name respondents or attribute comments. The customer does not receive respondent-level data. The customer tells participants this before they respond, using wording RCD supplies. Notice and consent wording is OPEN.
* Incident notice in this draft is limited to a confirmed privacy or security incident that materially affects customer data, followed by reasonable cooperation. The architecture standard is wider: notify without undue delay when a material effect is confirmed or reasonably suspected, and complete a post-incident review within five business days. Do not narrow the standard by using the draft until the lawyer settles it.
* Deterministic rules, automation and approved commercial AI may support analysis and drafting. RCD stays accountable for material assumptions, rankings, risks, recommendations and deliverables. Consequential outputs are not actioned solely on an automated output. The customer makes its own decisions.
* The customer owns or controls its data. RCD owns Background IP and reusable methods developed while performing services, provided they do not disclose customer Confidential Information.
* Until the engagement fees are paid, the customer may use deliverables only to review them. After payment, the customer may use, copy and internally adapt customer-specific deliverables, and may share them in confidence with Permitted Recipients on the stated conditions. Background IP, internal models, scoring logic and raw evidence are not licensed. This payment condition conflicts with the architecture rule that handover is not conditional on the final invoice. Leave it OPEN.
* No exclusivity. The customer may buy later stages from anyone.
* Neither party uses the other's name, logo, testimonial or case study externally without prior written approval.
* Where a Schedule identifies a Founding Partner, that customer gives reasonable structured feedback at agreed gates. Learnings used across customers are anonymised and aggregated.
* No warranty of savings, ROI, feasibility, regulatory compliance, error-free operation, funding eligibility or implementation success.
* Liability cap, exclusions and carve-outs are an OPEN legal section. The bracketed working baseline, not agreed, is the architecture baseline: fees for the affected services over 12 months, and during implementation not less than the implementation fee. Candidate carve-outs for the lawyer include fraud, wilful misconduct, death or personal injury, confidentiality, privacy and security, IP infringement and unpaid fees. The privacy, confidentiality and security super-cap is modelled at about twice the standard cap. Nothing limits liability that cannot lawfully be limited.
* Default insurance position: hold professional-indemnity and cyber cover appropriate to the services before delivery. Each Schedule states whether cover is held at the effective date. If it states that cover is not held, the maintenance promise does not apply to that engagement and the Schedule's disclosure and acknowledgement apply instead. Limits and any evidence obligation stay OPEN.

## 5. Disputes, notices and boilerplate

* Notify the dispute. Authorised representatives meet in good faith within five Business Days. If still unresolved after 10 Business Days, mediate in New Zealand before court proceedings, except urgent interim relief or debt recovery. Mediation mechanics are OPEN.
* Independent contractors. No employment, agency, partnership, joint venture or fiduciary duty.
* Assignment needs consent, not to be unreasonably withheld, except a solvent reorganisation or sale with notice.
* Force majeure does not excuse payment already due.
* Notices go to the Schedule contacts by email. Deemed receipt is OPEN. The working proposal is the next Business Day after sending unless a delivery-failure message is received.
* Variations in writing. Severance. No waiver by silence. Entire agreement. New Zealand law and non-exclusive New Zealand jurisdiction. Counterparts and electronic signatures, subject to law.
* Do not charge GST until registration is confirmed. The accountant confirms GST status before the first invoice.

## 6. Privacy schedule timing

On 10 November 2026 the founder recorded a timing choice, not a new architecture decision: keep privacy inside the agreement and its engagement schedule for the first engagement, and create the separate Privacy and Data Processing Schedule before Customer 2. The standard pack in the architecture still includes that separate schedule. Status of the timing choice: Provisional.

## 7. Superseded first-engagement exception model

WFM-001 Exception Register v0.2 (10 November 2026) was an internal record against Master Business Architecture v7.4.1. It is not for the customer. It created no new architecture or price-book decision. The founder had not signed the three exception records in that file. Architecture v8.2 (20 November 2026) later reclassified the first engagement as a Pilot outside the Founding Partner cohort and left the fee unfixed. Do not use the register's prices.

What the register proposed, and what governs now:

| Proposal in the 10 Nov register | Figure it used | Governing position after v8.2 |
| --- | --- | --- |
| Treat the engagement as Founding Partner Customer 1, Micro book | $1,500 + GST, 20% discount to $1,200 + GST | [Client-WKO-01](../clients/client-wko-01.md) is the Pilot, not a Founding Partner. No discount. Micro book in v8.2 stays $1,500 + GST and is not the Pilot price |
| Modelled cost at 5 founder hours | $625 labour at $125/hour plus $75 technology allowance (5% of book). Margin 41.7%. A 6th hour at $825 cost drops margin to 31.3% and fails the 40% exception. Headroom about ten minutes | The Pilot has no margin floor. The $1,200 model is retired. Still capture hours against the relevant ceiling as Customer Delivery COGS |
| CE-001. No upfront payment. 100% on Accepted Delivery. Start on the Assessment Ready Date | Credit risk until after the review period and the 14-day term | The same payment shape is a proposed Pilot-only term. It is not the standard |
| CE-002. Contract as a sole trader. Incorporate afterwards. No novation. Later stages are papered with the new entity | Personal liability. Discount term may straddle the entity change | Who contracts with the Pilot remains Open. The later Pilot draft names the limited company. Resolve before signature |
| CE-003. Deliver without PI or cyber cover, with written acknowledgement, liability capped at the fee | Claims outside an unenforceable cap reach personal assets | Pilot-only, and only with a clear written disclosure. Obtain a broker quote. Cover is required before Customer 1 |

The register's own combined-concession test said the discount, no upfront payment, sole-trader contracting and no insurance were individually workable and jointly left almost no buffer. That result is why those items stay customer-specific and why the Founding Partner price was not carried into v8.2.

Alignment notes that remain useful:

* The 10 Business Day Review Period is a contract default. Add the definition at the next editorial pass of the architecture. Do not treat it as already an Agreed architecture decision.
* Customer-facing decks and the Founding Partner one-pager still describe 50% upfront. Do not send them for the Pilot without a customer-specific note. One deck slide called responses confidential while another said they are identifiable to RCD. Use the identifiable-to-RCD, non-attributed wording.
* Product Design and the runbook assume a cleared upfront payment before initialisation. Under a no-upfront exception the founder releases delivery manually. That is an engagement note, not a standard change.
* A flat liability cap equal to one WFM fee matches "12 months of affected-service fees" for a single WFM fee. It does not satisfy the modelled 2x privacy, confidentiality and security super-cap. With no insurance, that gap is for the lawyer.
* Log Pilot hours in the investment tracker as Customer Delivery COGS, cohort Pilot, product Workflow Friction Map. Review them against the planned ceiling during delivery.
* Decide the approved AI service, if any, before kick-off. Confirm the Microsoft 365 processing location before customer evidence is stored. Do not write tenant identifiers into the wiki.

## 8. Still OPEN before any signature

Lawyer: liability cap, exclusions and carve-outs, including whether a fee-level cap is enforceable without insurance; insurance disclosure; stop-partway stage values and rescheduling percentages; deemed acceptance; second Review Period; notices; mediation; interest and collection costs; Confidential Information and Permitted Recipient; survey notice and consent; cross-border processing; sole-trader to company transition if that route is used; assignment.

Accountant: GST registration and the first invoice, GST basis, invoicing, income tax if revenue is still personal, incorporation timing, transfer of IP and records, and pre-incorporation costs.

Founder: approve or retire any Pilot exception in writing; remove Founding Partner and list-price lines from the Pilot agreement; choose the contracting party; request a PI and cyber quote; create the separate privacy schedule before Customer 2.
