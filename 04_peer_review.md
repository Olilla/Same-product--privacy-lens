# Phase 4 — Peer Review

## GDPR Audit Pack | Reviewer: Olalla
**Memo reviewed:** SaasX GmbH — LLM Fine-Tuning on Support Logs

---

## Rubric scores

| Criterion | Score (1–3) | Comment |
|---|---|---|
| Clear bottom-line recommendation | **3** | "Go with conditions" is stated immediately and unambiguously. The one-sentence reason ("would begin in breach of GDPR on at least three independent grounds") is specific enough to land without reading further. No vagueness. |
| Lawful basis selection is justified | **2** | Art. 6(1)(f) for the fine-tuning purpose (P2) is flagged correctly as uncertain and requiring an LIA, which is honest. However, the memo does not address the lawful basis for the *ongoing model operation* phase (P3) separately — it is implied but never stated. A CTO reading this memo would not know whether the live inference pipeline has its own basis or inherits it from P2. That gap should be closed. |
| Top actions are specific and sequenced | **3** | The three actions are well-ordered (pseudonymisation first, then DPA/transfer mechanism, then DPIA + notices) and the sequencing logic is explicit. The instruction to "budget for redaction before you budget for compute" is exactly the kind of concrete framing a non-legal CTO needs. |
| Residual risks are named honestly | **3** | The erasure-against-model-weights risk is the hardest and most honest call in the memo — it does not soften the fact that pseudonymisation reduces but does not solve it. DPF instability is flagged with the right historical context (two predecessors invalidated). The HmbBfDI assertiveness note is a genuine value-add that most memos would omit. |
| Law stacking is addressed (AI Act / ePrivacy) | **2** | The main memo body does not mention the AI Act or ePrivacy — these appear only in the worksheet (Section C), not in the client-facing document. For a reader who only sees the memo, the AI Act transparency obligation (Art. 50) and the potential high-risk classification question are invisible. At minimum, one sentence in the DPIA action item should flag that the AI Act may require a separate fundamental rights impact assessment alongside the GDPR DPIA. ePrivacy is correctly scoped as not triggered in the training phase, but the deployed interface risk is not carried forward into the memo. |

---

## Client response

As the client (Legal Team, SaasX GmbH), I accept the recommendation and the sequencing of the three actions. The pseudonymisation-first framing is persuasive and gives the engineering team a clear first task.

I have one challenge: **Action 3 instructs us to complete a DPIA in parallel with Actions 1 and 2, but the memo does not tell us who owns the DPIA or what the minimum scope is.** In practice, our ML engineering team will ask whether the DPIA needs to be finalised before data upload begins or only before model go-live. The worksheet says "before processing begins," but the memo says "before go-live" — those are two different dates and the gap between them is where the compliance risk lives. Please clarify the trigger point.

One additional ask: the memo references the HmbBfDI's assertive posture but does not tell us whether we should proactively consult the authority under Art. 36 (prior consultation) if the DPIA concludes with high residual risk. That decision point should be addressed explicitly so senior management can allocate time and resource for it if needed.