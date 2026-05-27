# Phase 2 — Mini GDPR Audit Worksheet

## GDPR Audit Pack | Ecommerce Company GmbH

---

## Section A — Data Map

| Field | Answer |
|---|---|
| **Categories of personal data** | (1) Behavioural / clickstream data (pages viewed, search queries, cart events). (2) Purchase history (product IDs, order amounts, delivery address, payment method type). (3) Account identifiers (name, email, hashed password, language preference). (4) Device and network data (truncated IP, user-agent, screen resolution). (5) AI-derived preference scores (product affinity vectors, stored as profile attributes). |
| **Sources** | First-party cookies set by Ecommerce Company's own domain. User-submitted account registration forms. Payment and order processing systems. DataPulse inference API (returns recommendation scores that are then stored back in Ecommerce Company's systems). |
| **Purpose 1: On-site personalisation** | Serve a "Recommended for you" product carousel based on the user's session and account history. |
| **Lawful basis — Purpose 1** | **Legitimate interests (Article 6(1)(f))** — LIA: *Purpose*: improving relevance of product display for the user and increasing conversion for Ecommerce Company. *Necessity*: personalisation cannot be achieved without processing behavioural data; anonymised aggregate data would not produce individual recommendations. *Balancing*: users have a reasonable expectation of some personalisation when using an e-commerce platform; Ecommerce Company offers a preference centre and opt-out. Legitimate interests is defensible here, but only if the cookie layer is separately compliant (see ePrivacy note in Section C). |
| **Purpose 2: Personalised marketing emails** | Populate weekly email with dynamically selected products and AI-generated subject line tailored to the user's top affinity category. |
| **Lawful basis — Purpose 2** | **Consent (Article 6(1)(a))** — Marketing emails require consent under both GDPR and the German UWG (Gesetz gegen den unlauteren Wettbewerb). Ecommerce Company currently collects consent at account registration. However, the consent form does not specifically disclose that email content is personalised using AI-derived affinity scores. **This is a gap: the consent is likely not sufficiently specific under Article 7 and Recital 32.** |
| **Purpose 3: Model retraining (batch transfer to DataPulse)** | Weekly export of pseudonymised event data to DataPulse for collaborative filtering model retraining. |
| **Lawful basis — Purpose 3** | **Legitimate interests (Article 6(1)(f))** — Same LIA rationale as Purpose 1, since retraining is a technical extension of the personalisation purpose. However, this must be explicitly covered in the privacy notice as a separate processing activity. Currently it is not. **Gap flagged.** If a regulator viewed the batch transfer as a separate, secondary purpose, consent or a compatible purpose assessment under Article 6(4) would be required. |
| **Purpose 4: Analytics and aggregate reporting** | Session-level and cohort-level analytics for business intelligence (conversion rates, funnel analysis). |
| **Lawful basis — Purpose 4** | **Legitimate interests (Article 6(1)(f))** — Analytics for business improvement is a widely accepted legitimate interest, provided data is pseudonymised or aggregated before use. Ecommerce Company truncates IP addresses, which supports this basis. |
| **Retention period — Purpose 1 (on-site personalisation)** | Session cookie: deleted at browser close. Persistent first-party cookie: 12 months. Account-linked behavioural data: retained for 24 months from last account activity, then deleted. **Gap: there is no documented retention policy for AI-derived preference scores. These appear to be retained indefinitely.** |
| **Retention period — Purpose 2 (marketing emails)** | Email address and consent record: retained until consent is withdrawn, plus 3 years for proof of consent. Personalisation payload per email: not separately retained beyond the send event log (30 days). |
| **Retention period — Purpose 3 (model retraining)** | Batch export files: retained by DataPulse for 90 days per the DPA, then deleted. **Gap: Ecommerce Company cannot verify DataPulse's deletion; no audit right is exercised.** |
| **Retention period — Purpose 4 (analytics)** | Aggregate reports: indefinite. Session-level pseudonymised logs: 13 months. |
| **Recipients and sub-processors** | (1) **DataPulse Inc.** (USA) — processor for recommendation inference and model retraining. (2) **SendGrid / Twilio** (USA) — processor for email delivery. (3) **AWS Frankfurt** — processor for cloud infrastructure (EU, no transfer concern). (4) Internal Ecommerce Company teams: marketing, engineering, data science (no external disclosure). |
| **International transfers and transfer mechanism** | Two transfers to the USA: DataPulse Inc. and SendGrid. Both are nominally covered by Standard Contractual Clauses (SCCs). However, the DataPulse DPA was signed in 2021 using the pre-2021 SCCs, which became invalid on 27 December 2022. **This transfer is currently operating without a valid transfer mechanism — a significant compliance gap.** A Transfer Impact Assessment (TIA) has also never been conducted for DataPulse. SendGrid's DPA was updated in 2023 and references the new Module 2 SCCs (controller-to-processor); this transfer appears valid, subject to a TIA being documented. |

---

## Section B — Risk and Rights

**B1. Are any special-category data present or inferable from the outputs (Article 9)?**

No Article 9 data is deliberately collected. However, Ecommerce Company's product catalogue includes dietary supplements, personal care products for chronic skin conditions, and home medical devices. A user's purchase history or browsing pattern could allow inference of health-related conditions (e.g., diabetic care products, allergy medication). The AI-derived affinity scores may therefore constitute *inferred* health data at the individual level, particularly where the affinity vector is used to surface health-adjacent product categories in emails. This is a latent Article 9 risk. Ecommerce Company should conduct a specific assessment of whether its product taxonomy, combined with AI profiling, creates inferential special-category exposure, and should consider product-category exclusions from the recommendation model where inference risk is elevated.

**B2. Is there automated decision-making with legal or similarly significant effects (Article 22)?**

The recommendation engine does not trigger Article 22 directly: it does not accept or reject users, restrict access, set individualised prices, or produce decisions with legal consequences. Product recommendations are not "similarly significant" under the EDPB's Guidelines 05/2020, which reserve that standard for decisions affecting access to credit, employment, healthcare, or essential services. However, the fact that the system produces **differential content exposure** (some users are shown promotional offers others are not) and that this feeds back into model training is worth documenting. The assessment should be recorded in a processing register entry. No Article 22 safeguard (human review, opt-out right, explanation right) is legally required, but offering a preference centre and a clear opt-out from personalisation is good practice and reduces LIA balancing risk.

**B3. Is a DPIA required?**

Using the EDPB's nine criteria (WP248 rev.01), the following apply to Ecommerce Company's scenario:

| Criterion | Applies? | Reasoning |
|---|---|---|
| Evaluation or scoring (profiling) | **Yes** | AI-derived affinity scores are a form of profiling under Article 4(4). |
| Automated decision-making with significant effects | No | Below Article 22 threshold (see B2). |
| Systematic monitoring | Partially | Clickstream tracking is continuous but limited to Ecommerce Company's own site. |
| Sensitive data or highly personal data | Partially | Latent Article 9 inference risk (see B1). |
| Data processed on a large scale | **Yes** | 1.4 million registered users, 600,000 monthly anonymous visitors. |
| Matching or combining datasets | **Yes** | Cookie IDs merged with account IDs at login; session data merged with purchase history. |
| Data concerning vulnerable subjects | No | No targeting of minors or other vulnerable groups identified. |
| Innovative use or applying new technological solutions | **Yes** | Real-time ML inference API integrated with front-end rendering. |
| Data transfer across borders with restriction obstacles | **Yes** | Transfer to DataPulse (USA) with invalid SCCs (see Section A). |

**Three or more criteria apply, which triggers a DPIA obligation under Article 35.** Ecommerce Company must conduct a DPIA before continuing the batch transfer to DataPulse and before deploying any expansion of the personalisation scope.

**B4. Data subject friction points**

- **Right of access (Article 15):** Users can request a copy of their data. Ecommerce Company currently has no self-service portal for this. A user requesting access to their AI-derived affinity scores is likely to receive an incomplete response because these scores are stored in DataPulse's system, not in Ecommerce Company's CRM. Ecommerce Company, as controller, is responsible for providing complete access across all processors. This is a high-probability friction point.
- **Right to erasure (Article 17):** Users who close their account expect all data to be deleted. The retention of batch export files at DataPulse for 90 days, and the absence of a verified deletion process, means erasure requests cannot be honoured fully within the 30-day deadline. Preference scores with no defined retention period compound this risk.
- **Right to object to profiling (Article 21(2)):** Users have an unconditional right to object to direct marketing profiling. Ecommerce Company must provide a clear, one-click mechanism to opt out of all personalisation, including email personalisation. Currently the preference centre does not cover AI-driven email personalisation separately.

**B5. Controller / processor split**

| Entity | Role | Basis |
|---|---|---|
| Ecommerce Company GmbH | **Controller** | Determines the purposes and means of processing (what data, why, and how). |
| DataPulse Inc. | **Processor** | Processes data only on Ecommerce Company's instructions (inference, retraining). Acts as a processor under the DPA — but Ecommerce Company must verify DataPulse does not use Ecommerce Company's data for its own model training or product development. If DataPulse uses the data for any of its own purposes, it becomes a **joint controller or independent controller**, which would require a separate legal basis and a joint controller agreement under Article 26. |
| SendGrid / Twilio | **Processor** | Delivers emails on Ecommerce Company's instruction. No independent data use. |
| AWS Frankfurt | **Processor** | Infrastructure hosting under standard cloud DPA. |

**B6. DPA required with which vendors?**

A Data Processing Agreement under Article 28 GDPR is required with:

- **DataPulse Inc.** — existing DPA is outdated (pre-2021 SCCs). Must be replaced immediately with a new DPA incorporating Module 2 SCCs and a TIA.
- **SendGrid / Twilio** — DPA exists and is current. Should be reviewed to confirm all sub-processors are listed and that the TIA has been completed.
- **AWS Frankfurt** — AWS standard DPA (GDPR-compliant) is in place for EU processing. No gap identified.

---

## Section C — Law Stacking

**AI Act cross-check**

Ecommerce Company's recommendation engine would most plausibly fall into the **minimal risk** tier under the EU AI Act. It is not a prohibited-use system (it does not perform real-time biometric identification, social scoring, or subliminal manipulation). It does not fall within Annex III high-risk categories (which cover employment, essential services, critical infrastructure, and similar). The GPAI provisions do not apply because Ecommerce Company is deploying a purpose-built model, not a general-purpose AI. The one AI Act obligation that may apply is **Article 50 transparency** if the system generates AI-drafted text (personalised email subject lines). If the subject line is fully AI-generated and presented as if written by Ecommerce Company's marketing team, there may be an obligation to disclose AI involvement to the user. This goes beyond GDPR's transparency requirement but is aligned with it. Ecommerce Company should assess whether its email subject line generation qualifies and, if so, add a brief disclosure.

**ePrivacy check**

This is the most significant law stacking issue in the scenario. The EU ePrivacy Directive (implemented in Germany via the TDDDG, formerly TTDSG) requires **prior, informed consent** for the placement of any cookie that is not strictly necessary for the service the user has explicitly requested. Behavioural tracking cookies (used to build the affinity profile that feeds the recommendation engine) are not strictly necessary. They therefore require consent **regardless of whether GDPR's legitimate interests basis is otherwise available**.

This means Ecommerce Company's reliance on legitimate interests for on-site personalisation (Purpose 1 in Section A) is only valid if the underlying cookie consent is properly obtained first. If the cookie banner does not meet the standard of freely given, specific, informed, and unambiguous consent (no pre-ticked boxes, no consent walls, a genuine and easy "reject all" option), then the entire data collection layer for personalisation is unlawful, and legitimate interests cannot rescue it. Ecommerce Company's current cookie banner implementation must be audited separately and is outside the scope of this GDPR-only audit, but it is flagged as a blocking dependency.

**Data Act check**

Not applicable to this scenario. Ecommerce Company does not operate connected products (IoT devices), does not provide cloud-switching services, and the recommendation engine does not generate data from physical products. No Data Act obligations arise.