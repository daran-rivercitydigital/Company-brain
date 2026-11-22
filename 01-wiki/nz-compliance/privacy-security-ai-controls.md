# NZ Compliance: Privacy, Security and AI Control Baseline

> **Compiled:** 2026-11-23 from RCD architecture v8.2 and technology stack v1.1  
> **Status:** Operating design. Not a certification, attestation, or legal opinion  
> **Related:** [Master Business Architecture](../playbooks/rcd-master-business-architecture.md) · [Technology Stack Requirements](../architecture/technology-stack-requirements.md)

RCD is designed to meet or exceed ISO 27001, SOC 2 and ISO 42001 baselines. Those certifications and attestations are not claimed. Qualified New Zealand legal, privacy, tax, accounting and insurance review is still required before external reliance.

## 1. Data classification and minimisation

| Class | Treatment |
| --- | --- |
| Customer data | Defaults to Confidential |
| Secrets, credentials, recovery information and sensitive production data | Restricted |
| WFM raw assessment evidence | Access-controlled, identifiable to RCD, never attributed to individuals in customer-facing outputs |
| Operational metadata | Online for 12 months |
| Compliance and control evidence | Generally 3 years, unless a longer duty applies |

* Collect the minimum needed for the workflow assessment or production task.
* Customer-facing WFM outputs stay at process or function level.
* WFM evidence must not be used to assess individual employee performance. The participant notice is still a Pilot candidate, not yet a universal standard. See [Client-WKO-01](../clients/client-wko-01.md).
* Do not place customer data in public consumer AI services.
* Synthetic or de-identified data is the default in development workbenches.
* Metadata-first logging: health, status, timing, identifiers and exception metadata, without retaining payloads by default.

## 2. Retention and deletion

| Data | Rule |
| --- | --- |
| Processing payload | Delete within a 15-minute target after task completion |
| Retry or quarantine payload | Delete after resolution, no later than 24 hours, unless a documented exception applies. Hold the minimum necessary data |
| WFM raw evidence | Delete no later than 30 days after completion, or after the end date if the engagement ends early. Record the date in a data close-out confirmation. Lawful, dispute, security or backup exceptions must be documented |
| Continuity backup of source code | After each production release. Exclude credentials, customer data and other customers' configuration |

The source architecture still contains an older line that raw evidence is deleted no later than 10 business days after acceptance. The later agreed rule is 30 days after completion for every WFM, including the Pilot. Use 30 days and reconcile the source before Customer 1.

## 3. Access, isolation and residency

* MFA, least privilege, time-limited access, logging, confidentiality and immediate removal.
* Review privileged access quarterly. Review significant accepted risks quarterly or on material change.
* Approved managed devices are required for Confidential or Restricted access. The endpoint product is not yet selected.
* Default runtime is an RCD-owned, customer-isolated deployment. Secrets stay outside code and workflow definitions and are separated by customer.
* A development workspace cannot approve its own production promotion.
* No company-wide NZ onshore hosting region is selected. Cloud provider and region stay open until a production requirement or a customer acceptance gate forces the choice.
* Record an NZ or Australia residency requirement on the relevant client page before Confidential data enters a non-Microsoft runtime. None is recorded for [Client-WKO-01](../clients/client-wko-01.md). Microsoft 365 is the approved WFM evidence store.
* Candidate runtimes, including Vercel and Supabase, must pass the region, isolation, subprocessor, retention, backup and portability gate in the technology article before production use.

## 4. AI governance

* Code or rules calculate. AI interprets, explains and drafts.
* Meaningful human review is required before a consequential AI output is acted on. Reviewers receive source context, assumptions, limitations and uncertainty.
* Incomplete or invalid source data blocks consequential output until correction or explicit human resolution. Corrected data is revalidated before replay, with idempotency protection.
* Maintain version-controlled model, provider and prompt inventories, with a reusable prompt baseline and separate customer configuration.
* Material model, provider or prompt changes need an impact evaluation covering outcomes, quality, failure modes, privacy, security, human oversight and regression. A failed evaluation blocks promotion.
* Non-material prompt changes stay version-controlled, regression-tested and approved.
* Run prompt-injection testing and constrain tool allow-lists.
* Review AI risk, impact and evaluation six-monthly and on material events.
* Replit, Cursor and Claude Code are Provisional human-directed tools. They are not approved for Restricted data or as an autonomous production path.

## 5. Resilience and incidents

| Control | Target |
| --- | --- |
| Critical corrective action | 72 hours |
| High | 14 days |
| Medium | 60 days |
| Low | 180 days |
| Internal RPO | No more than 24 hours, until proven in two restoration tests |
| Internal RTO | No more than 1 business day, until proven in two restoration tests |
| Restoration test | Six-monthly, plus after a material change |
| Penetration test | Annual, plus material-change testing |
| Customer notification | Without undue delay where a material effect is confirmed or reasonably suspected, subject to any shorter legal duty |
| Post-incident review | Within five business days of material incident closure |

The Pilot agreement currently proposes a narrower incident duty. That proposal is customer-specific and under review. It is not the RCD standard.

Production suspension for non-payment must still consider continuity, security, data protection and safe shutdown.

## 6. Assurance still required

* New Zealand legal and privacy review of liability, IP and licensing, continuity release, termination, reliance, cross-border processing, AI disclosure, survey privacy, consent and retention.
* Accountant confirmation of GST settings, accounting platform and banking structure.
* Professional-indemnity and cyber cover before Customer 1. The Pilot may proceed only with a written insurance disclosure because cover is not yet held.
* Do not describe ISO 27001, SOC 2 or ISO 42001 alignment as certification.
