# account-agent-eval

Evaluating a small LLM **account-management agent** the way a release-gating data scientist would — not just "does it work", but *how do we know, how sure are we, and should it ship?*

The agent helps a small B2B supplier manage ~40 restaurant accounts with three tools: **account Q&A**, **reorder flagging**, and **follow-up drafting**. All data is synthetic.

```mermaid
flowchart LR
    A[Synthetic accounts] --> B[Retriever]
    B --> C[Agent + 3 tools]
    C --> D[Eval harness]
    D --> E[Ship / no-ship report]
    classDef key fill:#2563eb,color:#fff,stroke:none
    class E key
```

## What gets measured

| Layer | Metrics |
|---|---|
| Retrieval | recall@k, MRR, NDCG |
| Agent | task success (with confidence intervals), groundedness |
| Judge | LLM-judge agreement with human labels |
| Failures | bucketed into retrieval / tool / reasoning |

## Roadmap

| Week | Focus | Output |
|---|---|---|
| 1 | Release-gate methods; eval-set design | `docs/release-gate.md`, test-task spec |
| 2 | Synthetic corpus + retrieval eval | `notebooks/` retrieval eval |
| 3 | Agent + task-level eval + failure analysis | `reports/eval-report-v1.md` |
| 4 | Production scoring pipelines (notes) | `docs/scoring-pipeline.md` |

## Layout

```
data/        synthetic accounts & test tasks
src/         agent, tools, eval harness
evals/       eval configs and labeled samples
notebooks/   exploration & metric analysis
reports/     eval reports
docs/        method notes
```

## Setup

```bash
uv sync
cp .env.example .env   # add your Anthropic API key
```
