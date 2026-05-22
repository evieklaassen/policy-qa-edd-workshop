# Workshop Brief: Eval-Driven Development for Enterprise AI Applications
**Prepared by: Evie Klaassen, May 2026**

---

## Topic & Rationale

This workshop focuses on **eval-driven development (EDD)**, the practice of building and iterating on AI agents against a disciplined, version-controlled evaluation dataset. In particular, we will explore the principles of EDD through the lens of a **policy Q&A chatbot** that answers employee questions about HR and IT policies.

Many enterprise teams building LLM-based applications hit the same wall: the app demos well, gets deployed to a pilot, and then fails on nuanced real-world queries in ways nobody anticipated. It's possible that fixing one issue could result in another. It becomes difficult to know if prompt changes, retriever changes, or model changes are improvements or regressions, and it's challenging to know whether quality is improving over time.

The root cause is almost always the same: instead of a team iterating without a systematic evaluation framework, they're optimizing by reading outputs.

**Use case rationale:**

HR and IT policy documents represent a near-universal enterprise use case where poor answer quality can have serious implications. The same question ("How many PTO days do I get?") has different correct answers depending on the employee's region, role, and tenure. And a wrong answer about parental leave or termination payouts could potentially expose the company to legal or HR risk. 

---

## Target Audience & Prerequisites

**Target audience:** Engineering teams building or evaluating RAG-based applications for internal knowledge Q&A, support, or decision-support use cases.

**Prerequisites:**
- Comfortable with developing in Python
- Has built at least one LLM-powered application (a RAG pipeline, an agent with tools, or similar)
- Understands the basics of RAG: document loading, chunking, embedding, retrieval, generation
- Understands the fundamentals of LangChain: LCEL, prompting, simple chain structures
- Minimal LangSmith experience required (ideal to know what LangSmith is and its basic features, but knowing how to use LangSmith is not required)
- No prior LangGraph experience required

**Participants will need:**
- A LangSmith account and LangChain API key
- An API key for an LLM provider (OpenAI in this workshop)
- Dependencies: Python 3.10+ and packages from `requirements.txt`

---

## Learning Objectives

By the end of this session, participants will be able to:

1. **Articulate why eval-driven development matters** and describe the specific failure modes it catches that manual review misses
2. **Design a golden eval dataset** that covers representative queries, context-dependent cases, and edge cases
3. **Choose and implement appropriate evaluators** (correctness, groundedness, completeness) using LLM-as-a-judge, and explain the failure mode each evaluator targets
4. **Run structured evaluation experiments in LangSmith** and compare results across versions to make data-driven iteration decisions
5. **Route cases to human review** using LangSmith annotation queues and describe the criteria for human vs. automated evaluation
6. **Articulate clear criteria** for when a change warrants a new eval run vs. when it doesn't
7. **Maintain a healthy eval dataset** by adding cases from real failures

---

## Where This Fits in a Broader Curriculum

**What comes before this module:**
- *LangChain fundamentals*: LCEL, prompting patterns, basic RAG pipeline construction
- *LangSmith basics*: What LangSmith is, how tracing works, navigating the UI

This module assumes participants have built at least a basic RAG chain and can read LangSmith traces. Deeper LangSmith evaluation experience is not required.

**What comes after this module:**
- *LangGraph and control flow*: Adding conditional logic, multi-step agents, and state management to the pipeline we built here
- *Human-in-the-loop agent patterns*: Going beyond annotation queues to agents that pause mid-execution and request human input
- *Production observability*: Monitoring live traffic quality in LangSmith, setting up degradation alerts, managing eval pipelines in CI/CD

The core purpose of this module is to help enterprise customers move past building cool prototypes and onto building production-grade and trustworthy agents.

---

## Anticipated Friction Points

**1. Skepticism around LLMs as a judge**

It's normal for developers to be skeptical of using LLMs to evaluate their outputs, because how can one know that the LLM-as-a-judge is evaluating correctly and properly? To address this, this workshop covers:
- Using a stronger model as judge than the model being evaluated
- Writing explicit rubrics rather than relying on judgment
- Using human review to periodically calibrate the judge. 

LLM judges themselves are not ground truths, but scalable proxies that needs their own quality bar.

**2. Choosing the right evaluators**

Teams often ask whether to use LangSmith's built-in evaluators or write custom ones. The workshop uses custom evaluators to make the rubric transparent and debatable, as well as one built-in evaluator for comparison and learning purposes. This workshop also demonstrates how different evaluators catch different failure modes.

**3. Producing ground truth labels at scale**

In this workshop's use case of policy Q&A, it is important to work with subject matter experts once per policy version. This is positioned as a one-time investment with clear business justification.

**4. Viewing human review (via annotation queues) as part of the evaluation cycle itself, not as a fallback**

Human review is a powerful tool that can help spot subtle hallucinations and errors in LLM-generated responses. It can also provide additional cases for our golden dataset, overall making our evaluations more robust. This workshop addresses how human review is a critical part of the evaluation cycle, not just a "plan B" for cases where our LLM-as-a-judge fails.

---
