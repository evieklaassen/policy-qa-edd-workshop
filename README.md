# Policy Q&A Agent — Eval-Driven Development Workshop

A technical workshop demonstrating eval-driven development (EDD) for enterprise AI agents, using LangSmith and LangChain.

## Quick Start

```bash
# 1. Clone / download this repo
# 2. Create a virtual environment
python -m venv .venv && source .venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set environment variables (copy and fill in)
cp .env.example .env
# Edit .env with your API keys

# 5. Launch the notebook
jupyter notebook policy_qa_agent.ipynb
```

## Environment Variables

Create a `.env` file (or export these in your shell):

```bash
OPENAI_API_KEY=sk-...
LANGCHAIN_API_KEY=ls__...
LANGCHAIN_TRACING_V2=true
LANGCHAIN_PROJECT=policy-qa-workshop
```

Get a LangSmith API key at [smith.langchain.com](https://smith.langchain.com).

## Repo Structure

```
workshop/
├── policy_qa_agent.ipynb      # Main workshop notebook
├── WORKSHOP_BRIEF.md          # Pre-session brief for team leads
├── requirements.txt
├── policies/
│   ├── pto_policy.md          # PTO policy (US/CA/NL/UK/DE variation)
│   ├── it_security_policy.md  # IT security policy (role-based variation)
│   └── parental_leave_policy.md
└── data/
    └── eval_dataset.json      # 12 golden eval cases (easy/medium/hard)
```

## What the Workshop Covers

1. **RAG-based policy Q&A agent** — loading, chunking, embedding, retrieval, generation
2. **Deliberate failure modes** — stingy retriever (k=1) and hallucination-prone prompt, for teaching purposes
3. **Custom LLM-as-judge evaluators** — correctness, groundedness, completeness
4. **LangSmith eval pipeline** — uploading datasets, running experiments, comparing results
5. **Annotation queues** — routing borderline cases to human review
6. **Iteration discipline** — when to re-run evals, how to maintain a healthy dataset

## Cost Estimate

Running the full notebook (3 chain versions × 12 eval cases × 3 evaluators):
- ~108 LLM judge calls (GPT-4o) + ~36 agent calls (GPT-4o-mini) + embedding calls
- Estimated cost: **$2–5 USD** in OpenAI API credits
- LangSmith free tier is sufficient
