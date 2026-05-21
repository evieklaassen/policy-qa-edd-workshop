# Eval-Driven Development Workshop for Enterprise AI Agents

A technical workshop demonstrating eval-driven development (EDD) for enterprise AI agents, using LangSmith and LangChain. The use case is an HR & IT policy Q&A agent.

## Quick Start

```bash
# 1. Clone / download this repo
# 2. Create a virtual environment
python -m venv .venv && source .venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set environment variables (copy and fill in)
cp .env.template .env
# Edit .env with your API keys

# 5. Launch the notebook using preferred method
```

## Environment Variables

It is critical to have an `.env` file with the following variables:

```bash
OPENAI_API_KEY=sk-...
LANGCHAIN_API_KEY=ls_...
LANGCHAIN_TRACING_V2=true
LANGCHAIN_PROJECT=policy-qa-eval-workshop
```

Get a LangSmith API key at [smith.langchain.com](https://smith.langchain.com).

## Repo Structure

```
workshop/
├── policy_qa_agent.ipynb      # Main workshop notebook
├── BRIEF.md                   # Pre-workshop brief for team leads
├── requirements.txt           # Dependencies
├── policies/                  # HR & IT policy documents
│   ├── pto_policy.md          
│   ├── it_security_policy.md  
│   └── parental_leave_policy.md
└── data/
    └── eval_dataset.json      # Golden dataset with 12 cases
```

## What this Workshop Covers

For a comprehensive overview of what this workshop covers, please review the [pre-workshop brief here](BRIEF.md).
