# Workshop Brief: Eval-Driven Development for Enterprise AI Agents
**Prepared by: Evie Klaassen**

---

## Topic & Rationale

This workshop teaches **eval-driven development (EDD)** — the practice of building and iterating on AI agents against a disciplined, version-controlled evaluation dataset — through the lens of a **policy Q&A agent** that answers employee questions about HR and IT policies.

Most enterprise teams building RAG-based agents hit the same wall: the agent demos well, gets deployed to a pilot, and then fails on nuanced real-world queries in ways nobody anticipated. They fix one answer and break another. They don't know if their prompt changes are improvements or regressions. They can't tell their stakeholders whether quality is improving over time.

The root cause is almost always the same: the team is iterating without a systematic evaluation framework. They're optimizing by reading outputs.

**Why policy Q&A specifically?**

HR and IT policy documents represent a near-universal enterprise use case with uniquely instructive failure modes. The same question ("How many PTO days do I get?") has different correct answers depending on the employee's region, role, and tenure. Errors are consequential — a wrong answer about parental leave or termination payouts isn't just unhelpful, it can expose the company to legal or HR risk. 

---

## Target Audience & Prerequisites

**Target audience:** Engineering teams building or evaluating RAG-based agents for internal knowledge Q&A, support, or decision-support use cases.

**Prerequisites:**
- Comfortable with Python (can read and write async functions, use virtual environments)
- Has built at least one LLM-powered application (a RAG pipeline, an agent with tools, or similar)
- Understands the basic mechanics of RAG: document loading, chunking, embedding, retrieval, generation
- Minimal LangSmith experience required (ideal to know what LangSmith is and its basic features, but knowing how to use LangSmith is not required)
- No prior LangGraph experience required

**Participants will need:**
- A LangSmith account
- A LangChain API key
- An API key for an LLM provider (OpenAI in this workshop)
- Dependencies: Python 3.10+ and packages from `requirements.txt`

---

## Learning Objectives

By the end of this session, participants will be able to:

1. **Articulate why eval-driven development matters** and describe the specific failure modes it catches that manual review misses
2. **Design a golden eval dataset** that covers representative queries, context-dependent cases, and edge cases — not just happy-path examples
3. **Choose and implement appropriate evaluators** (correctness, groundedness, completeness) using LLM-as-judge, and explain the failure mode each evaluator targets
4. **Run structured evaluation experiments in LangSmith** and compare results across agent versions to make data-driven iteration decisions
5. **Route cases to human review** using LangSmith annotation queues and describe the criteria for human vs. automated evaluation
6. **Articulate clear criteria** for when a change warrants a new eval run vs. when it doesn't
7. **Maintain a healthy eval dataset** by adding cases from real failures and avoiding common anti-patterns (teaching to the test, stale ground truth)

---

## Where This Fits in a Broader Curriculum

**What comes before this module:**
- *LangChain fundamentals*: LCEL, prompting patterns, basic RAG pipeline construction
- *LangSmith basics*: What LangSmith is, how tracing works, navigating the UI

This module assumes participants have built at least a basic RAG chain and can read LangSmith traces. It does not require deep LangSmith eval experience — we build everything from first principles during the session.

**What comes after this module:**
- *LangGraph and control flow*: Adding conditional logic, multi-step agents, and state management to the pipeline we built here
- *Human-in-the-loop agent patterns*: Going beyond annotation queues to agents that pause mid-execution and request human input
- *Production observability*: Monitoring live traffic quality in LangSmith, setting up degradation alerts, managing eval pipelines in CI/CD

This module sits at the intersection of "I've built something" and "I need to trust it in production." It's the bridge from prototype to production-ready discipline.

---

## Anticipated Friction Points

**1. "My agent didn't fail the way I expected."**

Modern LLMs are very good at sounding correct. If you just run difficult questions and wait for the model to fail, it often produces a plausible-but-wrong answer that's hard to distinguish from a correct one by reading. The workshop addresses this by *engineering* the failure modes deliberately into two degraded chain versions — a stingy retriever (k=1) and a hallucination-prone prompt — so the failures are systematic and visible in eval scores rather than dependent on LLM luck.

**2. "What's the right evaluator for my use case?"**

Teams often ask whether to use LangSmith's built-in evaluators or write custom ones. The workshop uses custom evaluators precisely to make the rubric transparent and debatable. A key learning moment is showing that different evaluators catch different failure modes — correctness alone can miss hallucination if the hallucinated answer happens to match the reference.

**3. "LLM-as-judge feels circular — isn't the judge also an LLM?"**

Yes, and this is a real concern worth addressing directly. The session covers: (a) using a stronger model as judge than the model being evaluated, (b) writing explicit rubrics rather than relying on judgment, and (c) using human review to periodically calibrate the judge. LLM judges are not ground truth — they're a scalable proxy that needs its own quality bar.

**4. "How do we get ground truth labels at scale?"**

For policy agents, the answer is: work with your subject matter experts once per policy version. This is positioned as a one-time investment with clear business justification — the alternative is shipping an agent whose error rate you can't measure.

**5. Understanding the annotation queue workflow**

Participants who haven't used LangSmith's UI before may need a quick walkthrough of the interface before the queue demo. The session builds in a live UI walkthrough moment to orient everyone before the code adds runs to the queue.

---

## Session Notes for the Facilitator

- The notebook is designed to run top-to-bottom with cell-level explanations. Each major section includes a `💬 Discussion point` markdown cell with talking points and anticipated questions.
- The eval run cells (Part 4d) take ~2–3 minutes each due to LLM judge calls. In a live session, it works well to kick off the first eval run, use the wait time to discuss evaluator design, then come back to results.
- The LangSmith UI is central to the session — experiment comparison, trace inspection, and the annotation queue should all be shown live. Make sure you're logged into LangSmith on the projected screen before the session.
- If participants don't have API keys set up, the failure mode demonstration cells (Part 3) can be shown pre-run as they are the most pedagogically important cells and don't require LangSmith.
