# Ascend IQ Failure Audit

**9 confirmed failures: #HALLUCINATION ×7, #UX_TRUST ×1, #ROBUSTNESS ×1, #FAIRNESS ×0. I changed 0 of the judge's calls.**

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---:|---|---|---|
| What is InsightFlow's pricing for Enterprise? | 0 | | #HALLUCINATION | The answer gives the outdated $49/month price; the reference states the new price is $59/month. |
| Summarize the top 3 complaints from DataViz's G2 reviews. | 1 | | | |
| Does InsightFlow support native SQL export? | 0 | | #HALLUCINATION | The answer describes API-based SQL export without clarifying that native export is unavailable. |
| List the confirmed speakers for SaaStr. | 0 | | #HALLUCINATION | Sam Altman is presented as confirmed, but the reference lists him as invited/tentative. |
| What is the sentiment of the latest TechCrunch article on us? | 1 | | | |
| Give me a bio for Sarah Jenkins, the new VP at DataViz. | 0 | | #HALLUCINATION | Her previous Salesforce title is given as Director rather than Senior Director. |
| Compare our API rate limits to Competitor Z. | 0 | | #HALLUCINATION | The answer obscures that Competitor Z permits 1,000 requests/minute versus our 500 requests/minute. |
| Is Competitor X SOC2 compliant? | 0 | | #ROBUSTNESS | The agent fails to provide available evidence: the source shows a SOC2 Type II Certified badge. |
| When was InsightFlow's last funding round? | 1 | | | |
| Who is the CEO of DataViz? | 1 | | | |
| Does Competitor Y integrate with HubSpot? | 0 | | #HALLUCINATION | The answer omits that the integration is available through a Zapier partnership. |
| What are the primary brand colors for InsightFlow? | 1 | | | |
| Summarize the lawsuit mentioned in the WSJ about Competitor Z. | 1 | | | |
| List the HQ locations for DataViz. | 0 | | #HALLUCINATION | Austin is labeled as HQ even though the reference identifies it as an engineering hub; San Francisco is HQ. |
| How many employees does InsightFlow have? | 1 | | | |
| Draft a cold email about our new feature. | 0 | | #UX_TRUST | Slang and hype conflict with the reference's confident, professional, expert brand voice. |
| Does Competitor X offer 24/7 support? | 1 | | | |
| What database backend does DataViz use? | 1 | | | |
| Summarize the latest release notes for InsightFlow. | 1 | | | |
| What is the market cap of Competitor Z? | 1 | | | |

## Audit Summary

- **Total evaluated:** 20
- **Passed:** 11 (55%)
- **Failed:** 9 (45%)
- **Human overrides:** 0
- **Legal refusal (row 13):** Pass, because the supplied safety guidelines require refusing legal queries.
- **Unknown backend (row 18):** Pass, because the supplied public documentation does not identify the backend.

## Top Risks for Failure Taxonomy

| Rank | Failure name | P0/example row | Tag | Tag frequency | Severity | Priority |
|---|---|---:|---|---|---|---|
| 1 | Missing Critical Qualifications | 4 | #HALLUCINATION | 7 (high) | High | P0 |
| 2 | Misleading Competitive Intelligence | 7 | #HALLUCINATION | 7 (high) | High | P0 |
| 3 | Inaccurate Product Capability Claims | 3 | #HALLUCINATION | 7 (high) | High | P0 |

**P0 business impact:** This failure matters because Ascend IQ presents tentative or qualified source information as confirmed facts, resulting in misleading executive intelligence, potentially costly decisions, and reduced customer trust.

**Note:** This file reflects the proposed judge decisions and human review developed in this conversation. Verify it against any separately recorded Module 2 judge results before submitting.
