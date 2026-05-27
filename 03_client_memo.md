# Phase 3 — Client Recommendation Memo

## GDPR Audit Pack | Ecommerce Company GmbH

---

**To:** Ecommerce Company GmbH — Legal Counsel and CTO  
**From:** Privacy Advisory  
**Re:** GDPR compliance status of the personalisation and analytics stack  
**Date:** May 2026  
**Classification:** Confidential — attorney-client privileged where applicable

---

## Bottom line

**Go with conditions — but do not transfer data to DataPulse again until the SCC gap is remediated.**

The personalisation engine is commercially sound and the underlying data processing purposes are legally defensible. However, two issues create immediate legal exposure that cannot be deferred: the international transfer to DataPulse is currently operating without a valid legal mechanism, and a DPIA is overdue. Both of these are not technical recommendations — they are compliance obligations the DPA could act on today if a complaint were filed. The rest of the conditions are serious but can be addressed in parallel with continued operation of the on-site recommendation layer, which does not rely on the DataPulse transfer for its core function.

---

## Top three actions

**Action 1 — Replace the DataPulse DPA and SCCs before the next batch export (deadline: immediately)**

The current DPA references the 2010 SCCs, which have been invalid since December 2022. Every batch transfer of event data to DataPulse since that date has been conducted without a valid Chapter V mechanism. Replace the DPA with a new agreement incorporating the 2021 Commission SCCs (Module 2, controller-to-processor) and complete a Transfer Impact Assessment covering DataPulse's obligations under US surveillance law (particularly FISA Section 702 and Executive Order 14086). Until the new DPA and TIA are signed and in place, suspend the weekly batch exports. The on-site real-time inference API can continue to operate if DataPulse's inference endpoint is covered by a separate and currently valid instrument — this must be confirmed with DataPulse in writing within five business days.

**Action 2 — Conduct a DPIA before any expansion of the personalisation scope (deadline: before the next feature release)**

Three or more EDPB criteria for mandatory DPIA are met: large-scale profiling, dataset combination, innovative technology, and cross-border transfer with identified obstacles. A DPIA is required under Article 35. This is not optional and cannot be substituted by an internal risk log. The DPIA should cover at minimum: the affinity score generation process, the batch transfer to DataPulse, the email personalisation pipeline, and the latent Article 9 inference risk from the product catalogue. If the DPIA identifies high residual risks that cannot be mitigated, you will need to consult with HmbBfDI before proceeding. Budget four to six weeks for a properly documented DPIA with legal sign-off.

**Action 3 — Audit and update the cookie banner and privacy notice (deadline: within 60 days)**

The legitimate interests basis for on-site personalisation is valid only if the underlying cookie consent layer is compliant with the TDDDG. If the current cookie banner does not offer a genuine "reject all" option with no consent wall, the entire behavioural data collection for personalisation is unlawful and legitimate interests cannot be applied. Commission a technical and legal audit of the cookie banner. Simultaneously, update the privacy notice to: (a) explicitly describe the AI-derived affinity score as a processing activity, (b) disclose the batch transfer to DataPulse as a separate purpose, and (c) revise the marketing email consent wording to cover AI-personalised content specifically. Add a one-click opt-out from all personalisation to the user preference centre.

---

## Residual risks

Even if all three actions above are completed in full, the following risks remain and cannot be fully eliminated:

**Risk 1 — Inferred Article 9 data.** The product catalogue contains health-adjacent categories. The AI model will continue to generate affinity scores that may amount to inferred health data for individual users. There is no clean technical fix that eliminates this risk while preserving the commercial value of health-category recommendations. The DPIA should formally document this residual risk and specify the product-category exclusions or score-level controls that reduce — but do not eliminate — the probability of a successful Article 9 challenge.

**Risk 2 — DataPulse's own data use.** The DPA constrains DataPulse to processing Ecommerce Company's data only on Ecommerce Company's instructions. However, Ecommerce Company has never exercised its audit rights under the DPA and has no independent verification that DataPulse does not use Ecommerce Company's data for its own model improvement or benchmarking. If DataPulse is acting as a joint controller or independent controller for any purpose, Ecommerce Company is exposed to a joint liability finding. This risk can be reduced but not eliminated through contractual strengthening and a right-to-audit exercise.

**Risk 3 — Access and erasure fulfilment across processors.** Ecommerce Company cannot currently respond to a data subject access request with a complete picture of that subject's data because the affinity scores stored in DataPulse's environment are not accessible through Ecommerce Company's CRM. Similarly, erasure requests cannot be confirmed as complete within 30 days. These are operational gaps with no immediate technical fix. Until a real-time data subject rights API is built between Ecommerce Company's systems and DataPulse, there is an ongoing risk of non-compliant response times and incomplete access responses.