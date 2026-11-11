# Eval Spec · Ascend IQ

# Eval Spec · Missing Critical Qualifications (#HALLUCINATION), an output risk

| Part | Spec |
|---|---|
| Target risk | Missing Critical Qualifications (#HALLUCINATION), an output risk: Ascend IQ omits or misstates source qualifications that materially change the answer, such as tentative confirmation status, API-only capabilities, third-party integrations, or office classifications. |
| Evaluator | Source-grounded qualification-preservation rule (question + answer + reference), with an independent LLM judge for ambiguous cases. Extract relevant qualifiers from the reference and check that the answer preserves their meaning; return 1 for pass and 0 for fail. |
| Threshold | **Ship only if the rule detects 4 of 4 known missing-qualification cases (100% recall) and produces 0 false alarms among the 11 audit-passing rows.** Lab 1 supports this initial regression gate: rule check 4 of 4 caught, 0 missed, 0 false alarms; safety rule 2 of 4 caught; judge 4 of 4 caught. This is a small-sample gate, not proof of production reliability. |
| Business stakes | Missing qualifications can make tentative speakers appear confirmed, API-only functionality appear native, and indirect integrations appear direct. VP-level clients may make costly planning, purchasing, or partnership decisions based on these misleading claims, increasing churn and reputational risk for a $50,000/year B2B product. |
| Owner | AI Engineering implements and enforces the pre-release rule; AI QA owns the regression dataset, independently reviews misses and false alarms, and monitors performance; Product Management owns the ship-or-hold decision. |

## Messages

**Engineering · acceptance criteria:** For each response, compare the question and answer with the verified reference; if a qualification material to the question (such as tentative status, API-only export, Zapier mediation, or engineering-hub status) is omitted or contradicted, return 0 and block the answer; otherwise return 1. Ship only when this rule catches all 4 of 4 known cases and causes 0 false alarms among the 11 audit-passing rows; send ambiguous cases to the independent LLM judge.

**Design · what the user sees:** When the check blocks an answer, do not show the unsupported statement as a confirmed fact; display “We’re verifying an important detail before answering” and, when the source supports it, present a corrected answer that explicitly labels the relevant limitation or uncertainty.

**Leadership · risk and return:** This check reduces the chance that executives act on confident but misleading market intelligence, protecting customer trust, renewal revenue, and brand reputation. In Lab 1 the low-cost rule caught 4 of 4 known cases with 0 false alarms, so it is a promising first gate while broader validation continues.
