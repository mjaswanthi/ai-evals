# Eval Spec - Incorrect Refund Promises (#HALLUCINATION), an output risk

| Part | Spec |
|---|---|
| Target risk | The online clothing store's AI bot promises refunds for ineligible orders or without confirming required eligibility. This is an output risk tagged #HALLUCINATION. |
| Evaluator | A deterministic rule checks the 30-day window and verified eligibility fields (unused item and original tags attached). An LLM judge evaluates ambiguous policy interpretations. |
| Threshold | **Prelaunch acceptance: catch 5 of 5 known incorrect-refund-promise cases and produce 0 false alarms on the 15 human-passing cases.** The hypothetical Lab 1 example showed rule check 3/5, safety rule 4/5, and judge 5/5; this is a proposed threshold, not a validated production guarantee. |
| Business stakes | Incorrect promises create refund disputes, support costs, potential financial losses, and customer trust damage. |
| Owner | Engineering implements and enforces the validator; QA monitors missed failures and false alarms; Product Management approves launch readiness. |

## Messages

**Engineering - acceptance criteria:** Before the bot guarantees a refund, verify that delivery was within 30 days, the item is unused, and original tags are attached. Return fail (0) and block a refund guarantee if any condition is false or unknown; return pass (1) otherwise. The prelaunch suite must catch 5/5 known failures with 0 false alarms on 15 passing cases.

**Design - what the user sees:** When eligibility is missing or fails validation, do not show a guaranteed refund. Show: "I need to check your delivery date, item condition, and tags before confirming whether a refund is available," and offer a way to provide those details or contact support.

**Leadership - risk and return:** Automated eligibility checks reduce costly refund disputes and prevent the AI from making promises the store's policy does not support. The inexpensive rule handles clear cases while targeted LLM review covers ambiguous ones.
