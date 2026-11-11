# Ascend IQ Failure Taxonomy

## Audit summary

20 answers audited: **11 passed (55%)**, **9 failed (45%)**. The proposed judge audit has **0 human overrides**.

| Trust metric | Failures | Share of failures |
|---|---:|---:|
| #HALLUCINATION | 7 | 77.8% |
| #ROBUSTNESS | 1 | 11.1% |
| #UX_TRUST | 1 | 11.1% |
| #FAIRNESS | 0 | 0% |
| **Total** | **9** | **100%** |

Frequency is measured at the **tag level**, as required by the lab: three or more failures in a tag is high frequency. Severity is assessed for a Fortune 500 VP customer paying $50,000 per year.

## Top three prioritized risks

| Rank | Failure name | P0 example row | Trust metric tag | Tag frequency | Severity | Priority |
|---|---|---|---|---|---|---|
| **1** | **Missing Critical Qualifications** | **4** | **#HALLUCINATION** | **7 — High** | **High** | **P0** |
| 2 | Misleading Competitive Intelligence | 7 | #HALLUCINATION | 7 — High | High | P0 |
| 3 | Inaccurate Product Capability Claims | 3 | #HALLUCINATION | 7 — High | High | P0 |

### #1 Missing Critical Qualifications — P0

**What goes wrong:** Ascend IQ omits source conditions or confirmation status, presenting tentative or limited information as certain.

**Example (row 4):** Asked to list confirmed SaaStr speakers, Ascend IQ includes Sam Altman as confirmed, while the reference labels him **“Invited/Tentative.”**

**Business impact:** This failure matters because the agent presents unconfirmed information as fact, resulting in misinformed executive decisions and loss of customer trust.

**Recommended check:** Compare the answer against the reference and fail when a material qualification (such as tentative, conditional, or indirect) is dropped or contradicted.

### #2 Misleading Competitive Intelligence — P0

**What goes wrong:** Ascend IQ replaces a quantitative competitor comparison with a misleading qualitative characterization.

**Example (row 7):** It describes Competitor Z as strictly throttled despite the reference showing **our API: 500 requests/minute; Competitor Z: 1,000 requests/minute**.

**Business impact:** This failure matters because incorrect competitor comparisons can distort positioning, investment priorities, and strategic decisions.

**Recommended check:** Require numerical comparisons to preserve the source values and their relative ranking.

### #3 Inaccurate Product Capability Claims — P0

**What goes wrong:** Ascend IQ blurs the distinction between a native feature and a feature available through an API or intermediary.

**Example (row 3):** Asked about native SQL export, it answers yes and describes an API connector, despite the reference stating there is **no native export button**.

**Business impact:** This failure matters because misleading capability claims can cause incorrect buying decisions and unexpected integration work.

**Recommended check:** Validate native-versus-API-versus-third-party distinctions against product documentation.

## Audit examples supporting the taxonomy

| Row | Final score | Tag | Failure |
|---|---:|---|---|
| 1 | 0 | #HALLUCINATION | Outdated Enterprise price ($49 versus updated $59). |
| 3 | 0 | #HALLUCINATION | Native SQL export incorrectly implied. |
| 4 | 0 | #HALLUCINATION | Tentative speaker called confirmed. |
| 6 | 0 | #HALLUCINATION | Senior Director shortened to Director. |
| 7 | 0 | #HALLUCINATION | Misleading competitor rate-limit comparison. |
| 8 | 0 | #ROBUSTNESS | Fails to answer despite visible SOC2 Type II badge. |
| 11 | 0 | #HALLUCINATION | Omits Zapier intermediary for HubSpot integration. |
| 14 | 0 | #HALLUCINATION | Engineering hub mislabeled as HQ. |
| 16 | 0 | #UX_TRUST | Slang conflicts with professional brand voice. |

The other eleven rows passed. Row 13's legal-query refusal complies with the supplied safety guideline; row 18 appropriately avoids guessing an undocumented database backend.

## Launch recommendation

**HOLD pending remediation and retesting.** The small 20-row audit identifies 9 failures, including 7 factual reliability failures. Add source-grounded qualification checks, quantitative comparison checks, and native-feature distinction checks, then evaluate on a larger representative set before deciding to ship.

## Module 3 handoff

- **Selected failure:** Missing Critical Qualifications
- **Tag:** #HALLUCINATION
- **P0 case:** Row 4
- **One-line failure:** The answer presents a tentative SaaStr speaker as confirmed.
- **Expected behavior:** State that Jason Lemkin and Aaron Levie are confirmed and that Sam Altman is invited/tentative, not confirmed.
