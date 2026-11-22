# Playbook: RCD Master Business Architecture

> **Source:** RCD Master Business Architecture, current state v8.2 (updated through 20 November 2026)  
> **Compiled:** 2026-11-23 | **Owner:** Founder | **Status:** Working single source of truth  
> **Stage:** Pre-incorporation and demand validation  
> **Technology implementation:** [Technology Stack Requirements](../architecture/technology-stack-requirements.md)  
> **Control baseline:** [Privacy, Security and AI Controls](../nz-compliance/privacy-security-ai-controls.md)

This article is the business baseline for how River City Digital (RCD) is established, sold, delivered, operated and productised. It supersedes architecture v7.1 except where a later decision is explicitly recorded. It is an operating design, not legal, privacy, tax, accounting, insurance or certification advice.

Where this article and the technology stack conflict, this article governs the required outcome and control. The technology article governs the implementation choice unless an explicit architecture decision says otherwise. A development application may be added in the technology article without reopening this baseline if it does not change the customer promise, commercial model, data classification, processing obligations, production controls, human-accountability model or founder approval authority.

## 1. Positioning

RCD is a Waikato-based, founder-led, productised AI implementation business for professional-services and mid-market firms. It sells business capacity, workflow improvement and controlled AI adoption. It is not SaaS-first and not open-ended consulting.

* **First learning vertical:** accountancy and advisory.
* **First repeatable hypothesis:** ledger-to-advisory preparation, kept demand-led rather than pre-built.
* **Operating constraint:** RCD remains a side business. Normal capacity is two concurrent paid engagements and one active implementation.
* **Core control principle:** code calculates; AI explains; the adviser judges.
* **Compliance posture:** designed to meet or exceed ISO 27001, SOC 2 and ISO 42001 baselines. Certification or attestation is not claimed.
* **Validation cohort:** the first three customers after the Pilot are Founding Partners. Customer 1 proves value, Customer 2 proves reuse, and Customer 3 proves repeatability before an evidence-based scale gate. The Pilot is [Client-WKO-01](../clients/client-wko-01.md), not a Founding Partner.

Strategic sequence:

1. Make discovery affordable and scalable.
2. Identify economically material workflow friction.
3. Jointly select 1, 3 or 5 opportunities to prove.
4. Charge for bounded Proofs of Value (PoVs) and credit 50% when the same workflow enters implementation within 90 days.
5. Deliver fixed-price implementation by confirmed complexity band.
6. Pass a formal acceptance gate into Managed AI Operations.
7. Measure customer value, reuse, margin, founder effort and delegated-delivery performance.
8. Productise and expand capacity only after repeated paid evidence.

## 2. Decision standards

| State | Meaning |
| --- | --- |
| Agreed | Current governing position. |
| Provisional | Usable launch assumption with an explicit validation trigger. |
| Open | Unresolved decision requiring future resolution. |
| Parked | Deferred until its documented trigger occurs. |

Apply an existing decision or established standard automatically. Extrapolate a governing principle consistently and name the standard used. Treat operational detail that depends on evidence as Provisional. Leave Parked items parked. Ask a new question only when the answer could materially change the commercial model, customer promise, product architecture, risk position, operating model, founder-capacity model or underlying architecture.

Exceptions must be materially justified, explicitly approved and documented. They stay customer-specific unless repeated evidence supports changing the standard. Record rationale, impact, risk treatment, expiry or review point, and affected sections.

Review after each Founding Partner, at the Customer-3 repeatability gate, annually, and on any material change. Every Provisional decision must then be converted to Agreed, revised, or explicitly retained as Provisional.

## 3. Product portfolio

Commercial stages are independently valuable and independently purchased.

| Layer | Product | Purpose | Commercial treatment |
| --- | --- | --- | --- |
| Discover | Workflow Friction Map (WFM) | Business-wide survey, materiality filter and ranked opportunity portfolio | Independent product; public fixed tiers after economic validation |
| Advise | AI Strategy Retainer | Fractional AI strategy, governance and realised-value review | Monthly; public from-price; excluded from Founding Partner discount |
| Enable | AI Training and Adoption | Productised workshops and implementation-specific handover | Public from-price; exact SKU after qualification; excluded from Founding Partner discount |
| Prove | Proof-of-Value | Bounded paid working demonstration | Proposal-based; internal Simple / Standard / Complex anchors |
| Implement | AI Workflow Implementation | Fixed-price production delivery | Proposal-based; internal anchors |
| Operate | Managed AI Operations | Tiered recurring production service | Provisional pending production evidence |

WFM is the diagnostic hub. It may route into PoV and implementation, the Strategy Retainer, Training and Adoption, or a combination. The customer selects 1, 3 or 5 workflows for paid PoV. Each PoV ends Proceed, Revise or Stop. Approved work passes a Delivery Stage Gate into fixed-price implementation, then a Go-Live Acceptance Gate, then Managed AI Operations where applicable. Annual reassessment continues the Discover, Prove, Implement, Operate, Reassess cycle.

New services start as bounded customer-specific work and enter the catalogue only after repeated demand, acceptable economics, meaningful reuse, reduced effort and sustainable capacity. Price the customer outcome, not the reduced internal effort from reuse. Recover reusable product and IP investment through portfolio margin, not a customer-specific IP charge.

### 3.1 Direct-to-PoV exception

WFM remains the primary route. It is not mandatory when bounded qualification establishes equivalent evidence for value, feasibility, risk and investment approval (Q274–Q279, Agreed).

* A Qualification Record must cover business value, workflow scope, feasibility, data readiness, key risks, human oversight and decision authority.
* A qualified opportunity may go to the Joint Investment Gate or be added into a WFM. WFM is the preferred path because it tests the opportunity across more staff and gathers the full evidence set.
* Free pre-sales discovery qualifies and routes only. Substantive analysis, ranked recommendations and workflow design require a paid WFM or PoV.
* The customer-facing proposition is WFM-centred. Other services are introduced only when discovery shows a relevant need.

## 4. Workflow Friction Map

The customer does not need to know its workflow count in advance. RCD groups evidence into shared workflow contexts, creates Primary Friction Records, and ranks economically material opportunities.

| Band | Surveys issued | Detailed shortlist | Provisional anchor + GST | Founder ceiling | Modelled margin |
| --- | --- | --- | --- | --- | --- |
| Micro | Up to 10 | Top 5 | $1,500 | 5h routine; 6th hour contingency | 53.3% |
| Small | Up to 15 | Top 7 | $2,500 | 8h | 55.0% |
| Growth | Up to 25 | Top 10 | $3,500 | 11h | 55.7% |
| Business | Up to 40 | Top 15 | $5,000 | 15h | 57.5% |
| Large | Up to 60 | Top 20 | $7,000 | 20h | 59.3% |
| Enterprise | Scoped | Scoped | Internal from $10,000; public Contact us | Scoped | At least 50% |

* Price is set by surveys issued, not responses completed. Report participation so the customer understands the evidence base.
* Direct technology cost is modelled at up to 5% of book price until actual cost is known.
* Sampling baseline by headcount: survey all up to 10 people; then 10, 15, 25, 40 and 60 across the bands above; 500+ is a scoped Enterprise assessment. This is a coverage mechanism, not a claim of statistical significance.
* Survey target is 10–15 minutes. Responses are confidential but identifiable to RCD for clarification. Customer-facing outputs stay at process or function level and do not attribute comments to individuals.
* Annual value uses conservative recoverable benefit, labelled Measured, Customer estimate, RCD estimate, or Unquantified benefit.
* Comparable non-retainer refresh is 20% off prevailing book price. An annual refresh is included in the Strategy Retainer. No WFM fee credit applies to downstream services.
* Survey allocations, thresholds, scoring, shortlist sizes and anchors stay Provisional until recalibrated after Customers 1–3.

Follow-up caps are 15 minutes each: Micro 2 staff + 1 executive; Small 3 + 1; Growth 5 + 1; Business 7 + 2; Large 10 + 2. Joint Investment Gate limits: Micro and Small 1 hour; Growth 1.5 hours; Business and Large 2 hours.

| Internal add-on | Standard + GST | Founding Partner + GST |
| --- | --- | --- |
| Four additional 15-minute interviews | $500 | $400 |
| Three additional Opportunity Cards | $750 | $600 |
| One-hour Joint Investment Gate extension | $500 | $400 |
| Bespoke analysis | From $1,000 fixed proposal | 20% off, subject to margin validation |
| Additional surveys | Move to the higher tier | Move to the discounted tier |

Publish validated WFM tier prices. Keep add-on prices internal. Enterprise remains Contact us.

### 4.1 Minimum sellable WFM (MSP1–MSP6, Agreed)

The minimum sellable WFM is the smallest customer-facing implementation that can be sold, contracted and delivered safely. Document hierarchy: this architecture prevails, then the separate WFM Product Design, then operational artefacts, then customer configuration.

| Decision | Selected design |
| --- | --- |
| MSP1 | Technology choices live in the technology stack and must not change the customer promise, commercial model, human gates or mandatory controls. |
| MSP2 | One reusable adaptive survey, 10–15 minutes, up to three detailed friction examples per respondent. Respondents are not asked to design AI solutions. |
| MSP3 | Economic materiality gate, then weighted Value x Feasibility, with material risk as a modifier. Scoring is an internal aid. Progress / Consider / Defer requires RCD judgement. |
| MSP4 | Executive WFM Report Pack as standardised PowerPoint and PDF. Excel stays internal. |
| MSP5 | Stage-gated and automation-first. Founder effort focuses on exceptions, judgement, risk, QA and the investment decision. |
| MSP6 | Automate administration, evidence preparation, deterministic calculations, draft artefacts and validation capture. Founder approval remains mandatory for consolidation, recoverability, capacity value, materiality, promotion, risk, complexity, ranking and customer recommendations. |

Recovered staff time is not automatically valued at salary cost. Identify the most credible economic use of recoverable capacity and do not count mutually exclusive uses twice. Where monetisation is speculative, keep the benefit unquantified.

A manual or template step may be used for Customer 1 where automation is incomplete, provided the method is standardised, time is captured, privacy and accuracy hold, and the gap is recorded. Customer-required effort is Customer Delivery COGS. Only incremental work done for broader reuse is RCD Product/IP Investment.

### 4.2 Primary Friction Record

The Primary Friction Record (PFR) is the canonical internal object for one distinguishable item of workflow friction. It does not by itself establish an opportunity, root cause, saving, ROI or solution.

Evidence chain: Source Evidence, Primary Friction Record, Assessment, Opportunity, Executive Opportunity Card, Joint Investment Gate.

* Evidence stays separate from interpretation and traceable to an approved source.
* A PFR is one friction mechanism, not one comment and not a proposed solution.
* Possible causes stay hypotheses until evidenced.
* Promotion to an Opportunity requires enough evidence for materiality, credible economic use, feasibility and risk.
* Deterministic rules calculate from recorded inputs. AI may suggest grouping, duplicates, wording, gaps and possible causes, and must not invent missing numbers.
* State friction as where it occurs, what happens, and the operational effect. Do not write it as a tool recommendation or a vague judgement.

Exact field names and physical storage remain Provisional pending the WFM MVP and Customer 1 evidence. The detailed schema lives in the separate PFR data standard.

## 5. Proof-of-Value and implementation

Unified Simple / Standard / Complex classification applies to PoV, implementation and enhancements. Classify by the highest material production-delivery driver across workflow breadth, integrations, data, transformation, AI, deterministic rules, human oversight, exceptions, security and privacy, criticality, deployment, testing, monitoring and recovery. Do not classify by customer size, transaction volume or feature count alone. Use the lowest band that safely contains the complete production-ready scope, including required controls.

| Band | PoV anchor + GST | PoV founder ceiling | Implementation anchor + GST | Implementation founder ceiling |
| --- | --- | --- | --- | --- |
| Simple | From $5,000 | 16h | From $12,000 | 32h |
| Standard | From $10,000 | 30h | From $25,000 | 70h |
| Complex | From $18,000 | 52h | From $50,000 | 140h |
| Portfolio | Fixed proposal | Scoped | Fixed proposal | Scoped |

* PoV direct COGS ceiling is up to 10%. Implementation routine direct COGS allowance is up to 15%.
* Every anchor must pass the 50% contribution-margin floor using founder labour at $125/hour before use.
* PoV and implementation prices stay proposal-based and are not published.
* A standard PoV includes scope and success criteria, readiness, lightweight design, reusable configuration, bounded build, test and demo, value and feasibility assessment, Proceed / Revise / Stop, implementation classification and price, and a customer readout.
* Do not contract a PoV unless a viable downstream implementation can absorb the PoV credit and any discount without dropping below the margin floor.
* 50% of the actual PoV professional-service fee is credited when the same workflow starts implementation within 90 calendar days. Exclude GST, third-party costs, travel and pass-through charges. The credit has no cash value and cannot move to another workflow or service.
* Apply percentage discounts first, then deduct the credit from the final implementation milestone invoice.
* Measure implementation margin after discounts and credits. On a phased programme, allocate the credit across binding phases when the first implementation contract is accepted. Optional later phases do not receive reserved credit.
* Multi-workflow portfolios are the sum of bands. Discount only where shared delivery creates demonstrated efficiency. Pass 50% of validated delivery-cost savings to the customer and retain 50%, subject to the margin floor.
* Founder labour, partner delivery and routine direct costs share one band envelope.
* Apply the provisional classification through Customers 1–3, record exceptions, and formalise or revise it after Customer 3.

### 5.1 Fixed-price payment

This schedule supersedes earlier 40/40/20 and 40/30/30 models.

* Up to 30 calendar days: 50% upfront and 50% invoiced on accepted delivery.
* Longer than 30 calendar days: 50% upfront, with the remainder across agreed milestones and the final payment on delivery.
* Delivery starts only after the upfront payment clears. That 50% is non-refundable once capacity is reserved.
* Standard payment term is 14 calendar days.
* Final deliverables are handed over at accepted delivery. The final invoice is not a precondition to handover.
* If the customer cancels after commencement, RCD may invoice completed work and committed non-cancellable cost above the upfront payment, up to the contracted total.
* If RCD cancels, refund fees for undelivered work.
* Recurring services are billed monthly in advance and are outside this model.
* Material scope changes need a documented impact assessment and written approval before changed work starts.
* After written notice, work may be suspended when an invoice is more than seven days overdue. Production suspension must protect continuity, security and data.
* Rescheduling is free with at least five business days' notice. Later cancellation may incur 50% of affected booked fees, or 100% within two business days, subject to reasonable treatment of genuine exceptional circumstances.
* Unaccepted proposals are valid for 30 days unless stated otherwise.

### 5.2 Go-live acceptance

Require functional acceptance, customer UAT, validated integrations, implemented security and privacy controls, validated AI and human-oversight controls, tested exception handling, operational logging and monitoring, backup and recovery where applicable, a runbook and support owner, and recorded customer approval to go live.

### 5.3 PoV development portability

A development application may accelerate a PoV and must not become an unreviewed production dependency. Code, configuration, schemas, tests, prompts, evaluations, architecture decisions and runbooks required to continue delivery must stay exportable and version-controlled.

* GitHub is the engineering system of record regardless of workbench.
* A development workspace may not approve its own production promotion.
* Development runtime and production runtime are separate decisions at the Proceed / Revise / Stop and Go-Live gates.
* Synthetic or de-identified data is the default. Customer Confidential or Restricted data needs the approvals in the technology architecture and the engagement terms.
* RCD must be able to continue delivery without undocumented workspace state, proprietary checkpoints or inaccessible configuration.

Replit is a Provisional PoV development application, not the default production runtime. Controls are in the [technology stack](../architecture/technology-stack-requirements.md).

## 6. Managed AI Operations

| Tier | Hypothesis + GST / month | Boundary | Steady-state max COGS | Founder intervention |
| --- | --- | --- | --- | --- |
| Essential | $995 | One production workflow; monitoring, maintenance, RCD defect correction, reporting and defined BAU | $398 | Up to 1.5h / month |
| Growth | $1,995 | Up to three workflows; active optimisation, one bounded minor change and enhanced reporting | $798 | Up to 3h / month |
| Scale | From $2,995 | Up to five workflows inside the agreed envelope; up to two minor changes | $1,198 at entry price | Up to 5h / month |

* The boundary is outcome and responsibility, not hours. Founder limits are internal controls.
* Map Simple / Standard / Complex provisionally to Essential / Growth / Scale, then confirm the tier at the Go-Live operating-envelope assessment.
* 12-month term from production launch, including a 90-day pilot, then month-to-month with 30 days' notice.
* The 90-day pilot is charged at the contracted monthly price. Day-90 tier corrections are prospective, with no retrospective charges or refunds.
* Not a 24x7 human response promise. Automated monitoring may be continuous.
* Founding Partner discount of 20% applies to RCD-earned service fees only. Cohort margin may sit below the 60% steady-state target and is recalibrated after Customer 3. Steady-state COGS cap is 40% of revenue. Founding Partner COGS cap is 60% of discounted revenue.
* Any month above eight founder BAU hours triggers review on a three-month rolling average.
* RCD absorbs its own defects and standard maintenance. Customer enhancements and material third-party redesigns are separately charged.
* Unused minor changes do not roll over. Standard and Extended intervention-pack prices remain open until production evidence exists.
* Quarantined integration payloads hold the minimum necessary data and are deleted after resolution, no later than 24 hours unless a documented exception applies.

Prices, allowances, overages and pilot-transition detail remain Provisional.

## 7. AI Strategy Retainer

Publish all three tier names and only "from $3,000 / month + GST".

| Tier | Price + GST / month | Default cadence | Founder ceiling | Maximum monthly COGS |
| --- | --- | --- | --- | --- |
| Advisory | $3,000 | Monthly, with quarterly strategic depth | 8h | $1,500 |
| Strategic Partner | $5,000 | Fortnightly | 16h | $2,500 |
| Transformation Partner | $10,000 | Weekly | 30h | $5,000 |

* One common strategic-governance core. Tiers differ by breadth, cadence, depth and operating envelope.
* Three-month initial commitment, then month-to-month with 30 days' notice. The first three months are establishment, not a discounted trial.
* Combined COGS envelope equals 50% of monthly revenue. Ceilings are three-month rolling internal controls with no rollover and no customer-hour entitlement.
* Between-session advice is reasonable use inside the envelope. There is no unlimited-access or immediate-response commitment.
* One strategic WFM refresh is included annually. Engineering, PoV, training, implementation and Managed AI Operations stay separately priced.
* Excluded from the Founding Partner discount.
* PB59–PB75 are closed for launch as Provisional. Customer 1 must validate demand, effort, COGS, margin, tier fit and founder-capacity impact before the anchors are treated as final book prices. Correct design before repricing.

## 8. AI Training and Adoption

Launch courses: AI Essentials for Business, AI for Leaders and Managers, and Microsoft 365 Copilot Adoption. Each is offered as a 90-minute session and a half-day workshop, giving six SKUs. Responsible and safe AI use is embedded in every course.

| Item | Book price + GST | Capacity / envelope |
| --- | --- | --- |
| 90-minute SKU | $1,500 | Up to 20 participants; 5h founder ceiling |
| Half-day SKU | $2,750 | Up to 15 participants; 9h founder ceiling |
| AI Adoption Starter | $4,000 | 12h plus up to 10% direct COGS |
| Wider Adoption Programme | Fixed proposal | Proposal-specific ceiling; no band anchors yet |

* Public line: "Training from $1,500 + GST".
* Remote delivery is the book-price basis. Recover material on-site travel and delivery cost separately.
* Larger audiences use additional sessions or a scoped large-format delivery, not per-person overage.
* RCD retains curriculum and reusable assets. Customers receive participant materials and workshop outputs for internal use.
* Workflow-specific handover training is included in implementation. Broader capability training is purchased separately.
* Repeated-session delivery savings are shared 50/50, subject to the margin floor.
* Excluded from the Founding Partner discount.
* Measure effectiveness through capability checks and participant feedback, not individual employee performance.
* PB76–PB94 are closed for launch as Provisional. Each SKU must still pass the 50% floor.

The Adoption Starter combines leadership alignment, one 90-minute workshop, a lightweight readiness assessment, an action plan, responsible-AI actions, measures and a leadership readout.

## 9. Founding Partners, margin and the Pilot

Founding Partners are Customers 1–3 after the Pilot. They are not advertised as a public discount.

* 20% discount for 12 months from the first paid service commencement, on eligible RCD professional-service and recurring-service fees.
* Excludes the Strategy Retainer, Training and Adoption, and all third-party consumption, licences, travel, expenses and overages. Managed AI Operations RCD service fees are eligible.
* Accepted contracted prices stay protected for their original term. Renewal moves to the prevailing book price with at least 30 days' notice.
* Founding Partners give structured feedback at major stage gates and at 12 months. If agreed participation does not occur, future discount entitlement ends. Discounts already received are not recovered.
* Validation learning is anonymised by default before cross-customer use.

| Rule | Position |
| --- | --- |
| Founder labour | Costed internally at $125/hour even when no salary is drawn |
| Normal floor | 50% professional-services contribution margin |
| Founding Partner exception | Down to 40% where reusable IP or validation value is recorded before contract |
| Managed steady state | At least 60%, recalibrated after Customer 3 |
| Book-price integrity | The undiscounted price must stand on scope, economics and value. It must not be inflated to create discount headroom |
| Pilot | [Client-WKO-01](../clients/client-wko-01.md) sits outside both the 50% floor and the 40% exception. The exception expires at Pilot close |

Repeatability gate after Customer 3, excluding the Pilot:

| Dimension | Threshold |
| --- | --- |
| Demand | At least 2 of Customers 1–3 buy substantially the same core pattern |
| Implementation margin | At least 50% after direct cost and founder labour |
| Effort reduction | At least 30% fewer comparable delivery hours from Customer 1 to Customer 3 |
| Reuse | At least 70% without fundamental redesign |
| Managed effort | No more than 4 founder BAU hours per customer per month on a three-month rolling average |
| Capacity | Supportable within normal capacity unless a controlled exception is approved |

New implementations pause if the gate fails. RCD Advisory Flow remains a direction, not a current product. P&L Variance Commentary is the provisional first module if paid demand confirms it.

## 10. Capacity, partners and funding

Exceed normal capacity only for a bounded engagement where strategic value, economics or reusable learning is shown and existing commitments, quality, margin and founder sustainability stay protected. Otherwise use a future slot or safely activated outsourced capacity. When demand exceeds capacity, prioritise customer value, margin, reusable learning, strategic fit, delivery feasibility and capacity impact.

* RCD remains accountable for outsourced quality, security and acceptance.
* The founder retains commercial ownership, architecture authority, material risk acceptance and final production acceptance.
* Partner cost is Delivery COGS. The customer buys the RCD product, not a partner day rate.
* Disclose partners who access systems or data or who materially contribute.
* Reduce founder oversight only after repeatability, procedures, quality controls, sustainable economics and successful delegated delivery.
* Maintain pre-qualified backup cover before a critical live service depends on the founder. Planned absence does not change customer pricing.
* Government or co-funding is an enabler, never a pricing or viability dependency. Do not represent eligibility as guaranteed. Training is potentially fundable only as part of an eligible adoption or implementation programme.

Track three cost layers separately: Customer Delivery COGS, RCD Product/IP Investment, and Business/Platform Establishment. Track founder cash injections separately from time and revenue.

## 11. Establishment and contracting

The first genuine commercial yes triggers establishment, in this order: incorporate River City Digital Limited; complete IRD and GST registration; open Operating, GST and Reserve accounts; configure accounting; bind professional-indemnity and cyber cover; execute the company contract and privacy terms; receive cleared upfront payment; begin on the Assessment Ready Date.

The Pilot may start before those steps. That exception is customer-specific, under review, and does not change the sequence for Customer 1 onwards. Who contracts with the Pilot, and whether the Pilot or Customer 1 is the establishment trigger, stays Open until after the Pilot and before the Customer 1 proposal. See [Client-WKO-01](../clients/client-wko-01.md).

Standard contract pack:

* Master Services Agreement
* Privacy and Data Processing Schedule
* Workflow Friction Map order
* Proof-of-Value order or statement of work
* Implementation statement of work
* Managed AI Operations Schedule

Working liability baseline, subject to New Zealand legal validation: 12 months of affected-service fees, and not less than the implementation fee during implementation. Privacy, confidentiality and security super-cap is modelled at 2x. The customer owns its data and customer-specific artefacts. RCD owns reusable components, patterns, templates and IP. The customer receives a perpetual internal-use licence to deployed reusable components. A controlled source-code continuity release applies only for defined cessation, insolvency, permanent discontinuation or material unresolved support failure, and excludes credentials, customer data and other customers' configuration.

## 12. Open, provisional and parked

### Open before operational readiness

* Company-name availability, incorporation, share structure, registered office and director records.
* GST settings, accounting platform and banking provider, confirmed with a New Zealand accountant.
* Professional-indemnity and cyber quotations, including limits, exclusions, retroactive date and offshore-provider treatment.
* Reusable contract pack and targeted New Zealand legal and privacy review.
* Structured cost and pricing ledger.
* Economic validation of WFM, PoV, implementation and training anchors before they are treated as validated book prices.
* WFM survey, sampling calculator, materiality model, Value x Feasibility model and Executive Opportunity Card.
* Six training SKU assets. Adoption Starter and wider-programme pricing still need paid evidence.
* Strategy Retainer fair-use confirmation from Customer 1 evidence.
* Managed AI Operations allowances, overage packs and intervention-pack prices after production evidence.
* Funding pathways, demand-generation mechanics, first backup partner, and legal positions on liability, IP, continuity release, termination, cross-border processing, AI disclosure, survey privacy, consent and retention.

### Provisional, with triggers

Apply WFM parameters, price anchors, complexity bands, training prices, retainer boundaries and managed-service prices consistently, then convert, revise or retain them after the stated evidence: each Founding Partner, Customer 1 retainer evidence, production evidence, or the Customer-3 gate. Contractual RPO and RTO commitments convert only after two successful restoration tests.

### Parked until the trigger

True multi-tenant runtime. Final cloud provider, region and dedicated secrets platform until production requirements force a choice. Full Advisory Flow platform. Full commercial telemetry automation. Public phone route and AI voice receptionist. Self-service training. Permanent contractor model. Second simultaneous implementation until the formal capacity gate passes.

## 13. Launch gates

RCD is architecturally ready and provisionally commercially ready. It is not yet operationally ready to start Customer 1.

| Gate | Required before proceeding |
| --- | --- |
| 1. Prospect conversation | WFM-centred proposition, qualification record, Founding Partner prices, meeting-evidence capture |
| 2. Accept a WFM sale | Minimum sellable WFM assets, pricing calculator, commercial ledger, WFM order, MSA, privacy terms, and establishment readiness |
| 3. Genuine commercial yes | Incorporation, IRD and GST, banking, accounting, PI and cyber cover, required legal review, executed documents, cleared 50% upfront payment |
| 4. Deliver Customer 1 | Operational WFM, minimum access and evidence controls, cost-layer capture, validation evidence pack |
| 5. Downstream on demand | PoV, implementation, training, retainer and managed-operations assets only when that service is sold |

Business-architecture decisions are complete through Q279. Price-book decisions are complete through PB94. Do not create a new decision solely to continue numbering. The immediate workstream is minimum-sellable WFM design, artefact creation, testing and Customer 1 readiness.

## 14. Technical patterns retained here

Detailed products are in the technology article. These outcome rules stay in this baseline:

* Prefer controlled automation, then contextual AI with human approval, then a secure processing pipeline for higher-risk work.
* Default to an RCD-owned, customer-isolated runtime. One reusable codebase, external configuration, secrets separated. True multi-tenancy stays parked.
* Promotion path: build, automated test, pre-production validation, founder approval, controlled deployment, health checks, rollback.
* Deterministic calculations stay in code or rules. Meaningful human review is required before consequential AI output is acted on.
* Material model, provider or prompt changes need an impact evaluation and a passing evaluation before production.
* Customer data defaults to Confidential. Secrets, credentials, recovery information and sensitive production data are Restricted.
* Processing-payload deletion target is 15 minutes. Approved retry or quarantine retention is up to 24 hours. WFM raw evidence is deleted no later than 30 days after completion, with the deletion date recorded. Operational metadata stays online for 12 months. Compliance evidence is retained for 3 years unless a longer duty applies.
* Section 29.4 of the source still says raw evidence is deleted no later than 10 business days after acceptance. Sections 11.5 and 12.3 later set 30 days after completion for every WFM, including the Pilot. Treat 30 days as the governing standard and reconcile the source wording before Customer 1.
* Corrective-action targets: Critical 72 hours, High 14 days, Medium 60 days, Low 180 days.
* Internal recovery targets until proven twice: RPO no more than 24 hours, RTO no more than 1 business day.
* Notify affected customers without undue delay when a material incident effect is confirmed or reasonably suspected. Complete a post-incident review within five business days of material incident closure.
