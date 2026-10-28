# AI Evals: Final Project

> My final project for Product School's **AI Evals** certification. One evaluation system for a real LLM feature, from strategy, through failure discovery and an automated eval suite, to the gates and governance that let it ship safely.

This is a **template repo**. Click **Use this template → Create a new repository**, name it `ai-evals` (or `<your-feature>-evals`), and fill in one folder per module as you go. The repo URL is your submission.

> **Tools & cost.** No eval platform, no signup, no credit card, and no code. Every lab runs in any chat, such as ChatGPT, Claude or Gemini, and the Lab Guide for each module gives you the prompts. Prefer a dashboard? LangSmith, Braintrust or Phoenix are optional.

---

## Deliverables at a glance

| Module | Artifact | Status | File |
|---|---|---|---|
| M1 | **Evaluation Strategy Canvas** | ☐ | `01-evaluation-strategy/strategy-canvas.md` |
| M2 | **Failure audit log** | ☐ | `02-failure-discovery/audit-log.md` |
| M2 | **Failure Taxonomy** | ☐ | `02-failure-discovery/failure-taxonomy.md` |
| M3 | **Eval suite** (three checks and their results) | ☐ | `03-eval-suites/eval-suite.md` |
| M3 | **Eval spec** (five parts and three team messages) | ☐ | `03-eval-suites/eval-spec.md` |
| M4 | **Eval gate map** (gate level × placement) | ☐ | `04-eval-gates/gate-map.md` |
| M4 | **Launch strategy** (release criteria + mitigation) | ☐ | `04-eval-gates/launch-strategy.md` |
| M5 | **Coverage matrix** | ☐ | `05-scale/coverage-matrix.md` |
| M5 | **Eval budget** | ☐ | `05-scale/eval-budget.md` |
| M6 | **Ship-or-hold memo** | ☐ | `06-culture/ship-hold-memo.md` |

## The feature in one sentence

_What LLM feature are you evaluating, who relies on it, and what is the cost of getting it wrong?_

---

## Per-module loop

Each module's Lab Guide walks you through its labs step by step, with the prompts you paste into any chat. Open it from the Resources slide in the module's deck.

1. Work through the Lab Guide's steps.
2. At the end of each lab, click **Copy markdown**.
3. Paste it over the matching file below, and commit.

| Module | Save to |
|---|---|
| M1 | `01-evaluation-strategy/strategy-canvas.md` |
| M2 | `02-failure-discovery/audit-log.md` and `failure-taxonomy.md` |
| M3 | `03-eval-suites/eval-suite.md` and `eval-spec.md` |
| M4 | `04-eval-gates/gate-map.md` and `launch-strategy.md` |
| M5 | `05-scale/coverage-matrix.md` and `eval-budget.md` |
| M6 | `06-culture/ship-hold-memo.md` |

## How to submit

- Turn the deliverable files into your final presentation with the Final Project Deliverables Builder.
- Post your repo URL in `#ai-evals-cohort` and upload to the learning-platform portal within 7 days of your cohort ending.

## Repo structure

```
ai-evals/
├── README.md                         ← this dashboard
├── 01-evaluation-strategy/           ← Module 1
│   ├── strategy-canvas.md            from the Module 1 Lab Guide, Activity 2
│   └── eval-harness-proof.md         optional notes from Activity 1
├── 02-failure-discovery/             ← Module 2
│   ├── audit-log.md                  scored audit of real outputs
│   └── failure-taxonomy.md           prioritized failure modes
├── 03-eval-suites/                   ← Module 3
│   ├── eval-suite.md                 three checks and their results
│   └── eval-spec.md                  five-part spec and three team messages
├── 04-eval-gates/                    ← Module 4
│   ├── gate-map.md                   gate level × pipeline placement
│   └── launch-strategy.md            release criteria + mitigation
├── 05-scale/                         ← Module 5
│   ├── coverage-matrix.md            coverage across product lines
│   └── eval-budget.md                eval budget + trade-offs
└── 06-culture/                       ← Module 6
    └── ship-hold-memo.md             ship-or-hold recommendation
```
