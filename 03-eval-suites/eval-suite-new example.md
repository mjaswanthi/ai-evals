# Eval Suite - Online Clothing Store Refund Bot

## Failure under test
**Incorrect Refund Promises (#HALLUCINATION):** The bot promises a refund without following the store policy: unused items may be returned within 30 days of delivery and must have original tags attached.

## Check 1 - Rule check
- **Looks at:** Customer question, bot answer, order delivery date, and current date.
- **Pass (1):** If more than 30 days have elapsed since delivery, the answer does not approve or guarantee a return/refund; otherwise the check passes.
- **Fail (0):** More than 30 days have elapsed and the answer explicitly approves or guarantees a return/refund.
- **Returns:** 1 or 0.

## Check 2 - Safety rule
- **Looks at:** Customer question, bot answer, and verified eligibility fields (delivery date, item condition, tags attached).
- **Pass (1):** The answer does not guarantee a refund unless all required eligibility fields are known and satisfy policy.
- **Fail (0):** The answer guarantees a refund when any eligibility field is missing or fails policy.
- **Returns:** 1 or 0.

## Check 3 - LLM judge
- **Looks at:** Customer question, bot answer, verified order details, and return policy.
- **Pass (1):** The answer accurately reflects the 30-day limit, unused condition, and original-tags requirement whenever relevant.
- **Fail (0):** The answer contradicts policy or omits a condition that changes eligibility.
- **Returns:** 1 or 0 plus one sentence explaining the decision.

## Illustrative evaluation results
*The following numbers are hypothetical teaching examples, not results from an executed audit.*

Assume a 20-answer human-reviewed dataset with 5 genuine incorrect-refund-promise failures and 15 passing answers. Run each check independently.

| Check | Caught | Missed | False alarms |
|---|---:|---:|---:|
| Rule check | 3 of 5 | 2 | 0 |
| Safety rule | 4 of 5 | 1 | 0 |
| LLM judge | 5 of 5 | 0 | 0 |

## Decide and save
**Classification: The Win.** A fast rule caught real failures (3 of 5), but neither rule caught all five; the judge found the remaining nuanced cases.

**Ship next:** Add structured eligibility checks before the bot can promise a refund, and use the LLM judge for cases involving unclear or conflicting policy conditions.

**Make it cheaper:** Store delivery age, unused status, and tags-attached status as explicit fields so a deterministic validator can check them without reading free-form policy text.
