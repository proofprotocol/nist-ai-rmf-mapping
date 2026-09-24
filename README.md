# PP-SPEC-033: Proof of Efficacy Mapping to the NIST AI Risk Management Framework

| Field | Value |
|---|---|
| Status | DRAFT v0.1 |
| Author | Craig Ellrod, Nebulonium, Inc. (dba HACKERverse®) |
| Date | September 24, 2026 |
| License | CC BY-ND 4.0 |
| Maps to | NIST AI 100-1, Artificial Intelligence Risk Management Framework (AI RMF 1.0), January 26, 2023 |
| Referenced by | Connecticut Public Act 26-100, Section 47(c)(2)(D) application materials; Virginia HB 797 and Colorado 4 CCR 904-6 comments |

## Cite as

Ellrod, C. (2026). PP-SPEC-033: Proof of Efficacy Mapping to the NIST AI Risk Management Framework.
Proof Economy Standards Alliance (PESA). https://doi.org/10.5281/zenodo.22944728

---

## 1. Purpose

This specification documents how Proof Protocol metrics and evidence map to the outcomes defined in the NIST AI Risk Management Framework (AI RMF 1.0). It exists so that regulators, independent verification programs, and buyers can see, subcategory by subcategory, which NIST outcomes a proof of efficacy record supports and what evidence it produces.

Several state frameworks ask independent verifiers to show how their metrics and methods align with NIST. Connecticut Public Act 26-100, Section 47(c)(2)(D), requires applicants to describe that alignment. This document is that description.

## 2. Scope

This specification defines **what is measured** and **what evidence is produced**. It does not describe how independent witnessing or evidence capture is implemented.

It covers the MEASURE function in depth, with supporting mappings to GOVERN, MAP, and MANAGE where a proof of efficacy record directly produces evidence for that outcome.

## 3. The Core Question

Proof of efficacy answers one question about any control:

> **Was there a control, and did it work?**

Terms used in this specification:

- **Control:** any safeguard, mitigation, or protocol intended to prevent, detect, or respond to a harm (for example, an egress filter, a guardrail, or a crisis-response protocol).
- **Attestation:** evidence produced by, or inside the control of, the party being assessed. Attestation can establish that a control exists. It cannot establish that the control works.
- **Proof:** evidence corroborated by one or more parties structurally independent of the party being assessed. Structural independence is a hard requirement for valid corroboration.
- **Proof of Efficacy:** corroborated evidence that a specific control, under adversarial conditions similar to deployment, performed as claimed.
- **Independent Proof of Efficacy Organization (IPEO):** a structurally independent party that produces Proof of Efficacy.

## 4. Metric Definitions

All metrics are computed against a **defined test corpus**: a documented set of adversarial cases, each paired where applicable with a benign case that the control should allow.

| Metric | Definition |
|---|---|
| **Efficacy score** | The headline measure. For every adversarial case launched from the corpus, the result is recorded as **blocked** (the control stopped it), **detected** (the control identified it but did not stop it), or **missed** (the control neither stopped nor identified it). The efficacy score reports the distribution across these three outcomes. |
| **Containment rate** | The share of adversarial cases the control blocked. |
| **Detection rate** | The share of adversarial cases the control identified, whether or not it blocked them. |
| **Miss rate** | The share of adversarial cases the control neither blocked nor identified. |
| **False-positive rate** | The share of paired benign cases the control wrongly blocked or flagged. A control cannot score well by blocking everything. |
| **Robustness** | Results for the subset of cases that attempt to suppress, evade, or bypass the control. |
| **Version-level results** | All metrics reported per version of the system and control under test, with retesting after any material change. |
| **Invalid-result status** | A result is marked **INVALID** when any part of its evidence is incomplete or broken. An invalid result is never counted as a pass and never fails silently. |

**Target levels.** Acceptable levels and target values for each metric are defined per engagement and per risk category, together with the data sources they rest on. They are not fixed by this specification.

## 5. Evidence Produced

| Artifact | Description |
|---|---|
| **Proof record** | One record per test case: control under test, system and version, case category, verdict, and timestamp. |
| **ProofStamp™** | RFC 3161 trusted timestamp bound to each verdict at the moment it is rendered, so a third party can verify when the result was produced and that it has not changed. |
| **ProofBundle™** | A packaged set of proof records, timestamps, metric results, and corpus manifest for a given engagement, suitable for regulators, auditors, insurers, and buyers. |
| **ProofRegister™** | A public register of issued proof records. |
| **Corpus manifest** | Case categories, counts, benign pairings, and corpus version for each run. |

## 6. Mapping to NIST AI RMF 1.0

NIST outcome text is summarized. Consult NIST AI 100-1 for the authoritative wording.

### 6.1 MEASURE

| NIST ref | NIST outcome (summary) | Proof Protocol element | Evidence |
|---|---|---|---|
| **MEASURE 1.1** | Metrics are selected starting with the most significant risks; risks that cannot be measured are documented. | Corpus categories prioritized by risk; out-of-scope risks stated per engagement. | Corpus manifest; scope statement |
| **MEASURE 1.2** | Appropriateness of metrics and effectiveness of existing controls are regularly assessed and updated. | Efficacy score per control, measured on a recurring basis. This is the core of proof of efficacy. | Efficacy score over time; proof records |
| **MEASURE 1.3** | Independent assessors are involved in regular assessments. | Structurally independent witnessing; fees fixed in advance and never conditioned on results. | Independence policy; proof records |
| **MEASURE 2.1** | Test sets, metrics, and tool details used in TEVV are documented. | Corpus manifest, metric definitions (Section 4), tool and version identifiers. | ProofBundle |
| **MEASURE 2.3** | Performance or assurance criteria are measured and demonstrated for conditions similar to deployment. | Testing in an environment configured to resemble the customer's deployment. | Environment descriptor in each ProofBundle |
| **MEASURE 2.4** | Functionality and behavior are monitored in production. | Continuous or recurring test runs against the deployed control. | Time series of proof records |
| **MEASURE 2.6** | The system is evaluated regularly for safety; safety metrics reflect reliability and robustness. | Miss rate and robustness results; recurring evaluation. | Efficacy score; robustness subset |
| **MEASURE 2.7** | Security and resilience are evaluated and documented. | Adversarial test corpus; containment and detection rates. | Proof records; ProofBundle |
| **MEASURE 2.13** | Effectiveness of the TEVV metrics and processes themselves is evaluated. | False-positive pairing and invalid-result status keep the measurement honest; metric definitions reviewed per version of this specification. | Invalid-result records; false-positive rate |
| **MEASURE 3.1** | Existing, unanticipated, and emergent risks are tracked based on performance in deployed contexts. | Corpus updated as new attack categories emerge; versioned corpus. | Corpus manifest version history |
| **MEASURE 4.2** | Results validate whether the system performs consistently as intended across the lifecycle. | Version-level comparison of all metrics. | Version-level results |

### 6.2 GOVERN, MAP, and MANAGE

| NIST ref | NIST outcome (summary) | Proof Protocol element | Evidence |
|---|---|---|---|
| **GOVERN 4.3** | Practices enable AI testing, incident identification, and information sharing. | Recurring adversarial testing with publishable results. | ProofRegister entries |
| **MAP 2.3** | TEVV considerations, including experimental design, are identified and documented. | Corpus design with benign pairings and category coverage. | Corpus manifest |
| **MAP 4.2** | Internal risk controls for AI system components are identified and documented. | Every proof record names the control under test. This answers the first half of the core question: was there a control? | Control identifier in each proof record |
| **MANAGE 1.1** | A determination is made whether the system achieves its intended purposes. | Per-case verdicts and efficacy score provide the evidence base for that determination. | Efficacy score; ProofBundle |
| **MANAGE 4.1** | Post-deployment monitoring plans are implemented, including change management. | Retesting triggered by material change to model, configuration, training data, or deployment context. | Version-level results |

## 7. Supporting NIST Publications (planned for v0.2)

| Publication | Planned use |
|---|---|
| NIST AI 600-1, Generative AI Profile | Extend the mapping to generative and agentic system risks. |
| NIST AI 100-2, Adversarial Machine Learning taxonomy | Label corpus categories by NIST-recognized attack type, so efficacy scores break down on a shared vocabulary. |
| NIST SP 800-53 Rev. 5, CA-2 and CA-8 | Map to control assessment and penetration testing requirements for organizations operating under 800-53. |

## 8. Alignment with State Frameworks

| Jurisdiction | Provision | Relevant sections of this spec |
|---|---|---|
| Connecticut | Public Act 26-100, Sec. 47(c)(2): acceptable risk levels, measurable metrics, target levels, ongoing evaluation, NIST alignment | 4, 5, 6 |
| Connecticut | Sec. 47(d)(4): reassessment on material change | 4 (version-level results); 6.2 (MANAGE 4.1) |
| Connecticut | Sec. 47(f)(1) and (f)(4): approval may be revoked if verification is ineffective | 3; 4 (invalid-result status); 6.1 (MEASURE 2.13) |
| California | SB 813, Gov. Code 8898.1(c)(2)(C)-(D): conflicts of interest and independence | 3; 6.1 (MEASURE 1.3) |
| Virginia | HB 797 factors (ii) measurable metrics and (iv) efficacy of mitigation requirements | 4; 6.1 |
| Colorado | HB 26-1263 annual report metrics on the efficacy and reliability of safeguards | 4 |

A common taxonomy of efficacy metrics lets results produced under one state's framework be read under another's. What works in one state can work anywhere.

## 9. Versioning

NIST has stated that AI RMF 1.0 is being revised. This mapping will be updated when the revised framework is published. Each version of this specification is anchored with a dated identifier.

---

*Proof Protocol · proofprotocol.io · CC BY-ND 4.0*
