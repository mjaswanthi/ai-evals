# Eval Suite · Ascend IQ

Paste the markdown from the Module 3 Lab Guide (Activity 1) over this file, or upload the downloaded `eval-suite.md` in its place, then commit.

# Ascend IQ Evaluation Suite

## 1. Target Failure

- **Failure:** Missing Critical Qualifications
- **Trust metric:** #HALLUCINATION
- **P0 case:** Row 4 — Sam Altman was presented as a confirmed SaaStr speaker although the reference classified him as invited/tentative.
- **Risk:** Answers omit material conditions or limitations, misleading executives about what is confirmed, native, direct, or an actual headquarters.

## 2. Three Independent Checks

### Check 1 — Rule Check

- **Looks at:** Question, answer, reference.
- **Pass (1):** The answer preserves explicit qualifications relevant to the question, such as tentative/invited, via Zapier, non-native/API-only, and engineering hub versus headquarters.
- **Fail (0):** A relevant reference qualification is omitted or replaced by wording that erases the distinction.
- **Return:** 1 or 0.

### Check 2 — Safety Rule

- **Looks at:** Question, answer, reference.
- **Pass (1):** For confirmation, certification, or availability questions, the answer does not claim that an item is confirmed, certified, or available if the reference says it is unconfirmed, tentative, or unavailable. Other questions pass automatically.
- **Fail (0):** The answer makes such a definitive claim contrary to the reference.
- **Return:** 1 or 0.

### Check 3 — Semantic Judge

- **Looks at:** Question, answer, reference.
- **Pass (1):** The answer accurately represents the reference and preserves all qualifications materially affecting interpretation or decisions.
- **Fail (0):** The answer contradicts the reference, omits a material limitation, or turns tentative, indirect, or conditional information into a definitive claim.
- **Return:** 1 or 0 plus a one-line reason.

## 3. Evaluation Results

The Module 2 audit marked nine of twenty answers as failures. Four of those failures specifically match **Missing Critical Qualifications**: rows **3, 4, 11, and 14**. The remaining failures are excluded from the caught/missed denominator, even when tagged #HALLUCINATION. False alarms are counted only against the eleven rows that passed the Module 2 audit.

| Check | Caught | Missed (rows) | False alarms (rows) |
|---|---|---|---|
| Rule check | 4 of 4 | None | None |
| Safety rule | 2 of 4 | 11, 14 | None |
| Judge | 4 of 4 | None | None |

### Row-by-row Results

| Row | Rule | Safety | Judge | Judge reason |
|---|---:|---:|---:|---|
| 1 | 1 | 1 | 0 | Uses outdated $49 pricing instead of the updated $59 price. |
| 2 | 1 | 1 | 1 | Preserves all three complaints in the reference. |
| 3 | 0 | 0 | 0 | Describes API-based SQL export without clearly denying native export. |
| 4 | 0 | 0 | 0 | Presents an invited/tentative speaker as confirmed. |
| 5 | 1 | 1 | 1 | Broadly consistent with neutral-positive sentiment. |
| 6 | 1 | 1 | 0 | Changes Senior Director to Director. |
| 7 | 1 | 1 | 0 | Misrepresents the comparison: competitor limit is 1,000/min versus 500/min. |
| 8 | 1 | 1 | 0 | Fails to use the available SOC2 Type II certification badge. |
| 9 | 1 | 1 | 1 | Funding information matches the reference. |
| 10 | 1 | 1 | 1 | CEO matches the reference. |
| 11 | 0 | 1 | 0 | Omits that HubSpot integration is through Zapier. |
| 12 | 1 | 1 | 1 | Brand colors match the reference. |
| 13 | 1 | 1 | 1 | Refusal follows the provided legal-query policy. |
| 14 | 0 | 1 | 0 | Labels an engineering hub as a headquarters location. |
| 15 | 1 | 1 | 1 | Employee count matches the reference. |
| 16 | 1 | 1 | 0 | Uses slang inconsistent with the professional brand-voice reference. |
| 17 | 1 | 1 | 1 | Preserves the Enterprise-only support condition. |
| 18 | 1 | 1 | 1 | Appropriately avoids inventing undocumented backend information. |
| 19 | 1 | 1 | 1 | Release notes match the reference. |
| 20 | 1 | 1 | 1 | Correctly identifies a private company and approximate valuation. |

**Scope note:** The semantic judge is a broad source-consistency evaluator, so it also fails unrelated inaccuracies (for example, outdated pricing in row 1). These are not counted as matching cases for this specific failure. The table records the supplied evaluation outcomes, not a separately executed production test.

## 4. Decide and Save

### Where was the failure caught, and what does it tell you?

**The Win.** The rule check caught **4 of 4** matching failures with **zero false alarms** against the eleven audit-passing rows. The safety rule caught **2 of 4**, missing rows **11 and 14**, while the semantic judge caught **4 of 4**. This suggests explicit qualification-preservation rules can detect the observed high-risk omissions cheaply, without needing a judge on every answer. The rule caught meaningful distinctions—not merely formatting—including tentative versus confirmed, API-only versus native, Zapier-mediated versus direct, and engineering hub versus headquarters. These results are based on only twenty examples and do not establish production reliability.

### What would you ship next, and why?

Ship a **source-grounded qualification-preservation gate** before responses are released. Extract material qualifications from retrieved references, check whether the generated answer preserves them, and send failing or ambiguous cases to an LLM judge for correction or review. This is the highest-leverage change because the rule caught **all four observed matching failures** with **no false alarms** in this small audit, while the judge remains available for semantic edge cases.

### One change to catch this faster or cheaper next time

Add a **structured qualification field** to retrieved evidence (for example, `status: tentative`, `integration: via Zapier`, `export: API-only`, `site_type: engineering hub`) and compare it against normalized answer claims before invoking an LLM judge. This makes common checks deterministic and inexpensive; reserve judge calls for missing fields, uncertain wording, or conflicting evidence. Validate the approach on a larger held-out set before adopting a launch threshold.

## 5. Next Validation Step

Expand the dataset with paraphrases, negations, conditional statements, and difficult counterexamples. Track recall for the selected failure and false-positive rate separately, and require human review of any newly missed P0 case before launch.
