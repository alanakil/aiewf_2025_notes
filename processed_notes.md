### AI Engineer World’s Fair 2025 – Key Takeaways

**1. LLM & Agent Evaluation**

* **Production evals go beyond benchmarks:** Use targeted frameworks for each architecture (RAG, MCP, Agents, Decision Support). Metrics include RAGAS, field extraction, pipeline completion, function call validity, and step consistency.
* **Automate and iterate evals:** LLM-as-a-judge is maturing for tasks like summarization, function call accuracy, emotion/toxicity detection, and plan validation. Regular A/B testing and failure analysis (implicit/explicit feedback) are critical. Top teams spend >2hrs on observability per day.

**2. RAG & Knowledge Graphs**

* **GraphRAG is the future:** Move from flat retrieval to graph-structured retrieval for better reasoning and causal understanding. Use properties and relationships, not just embeddings.
* **Start small, iterate:** Only add necessary data to knowledge graphs. Use evals to refine structure. Community detection and clustering help with data cleaning and chunking.
* **Chunk importance:** Measure chunk utility via PageRank, centrality, co-occurrence.

**3. Building and Scaling Agents**

* **Agent orchestration is on a maturity curve:**

  * Level 0: Basic chat QA
  * Level 1: RAG
  * Level 2: Single-task agents
  * Level 3: Multi-workflow, cross-domain agents
  * Level 4: Real-time cross-domain agent collaboration
* **Instructions/specs > prompts:** Successful coding agents (e.g., Copilot) rely on structured instructions and setup files, not ad hoc prompting. Specs and guidelines are the real bottleneck.
* **Functionality best practices:**
  * Memory/traceability: Track every agent step for reproducibility and improvement
  * Weekly failure/observability reports are a must

**4. Practical Deployment Insights**

* **Observability tools are maturing:** Consider platforms like Arize AI, W&B, galileo, freeplay, braintrust, traceloop, etc. for LLM observability and evals.
* **Updating and versioning:** Over 70% of orgs update models/prompts monthly, but many lack prompt versioning. Strong versioning practices needed.
* **Cost, scale & infra:** Costs are dropping fast; smaller models are more powerful, and inference efficiency is rapidly improving.

**5. State of the Art & Trends**

* **Open source is accelerating:** Open-weight models from China are advancing rapidly; execution and integration are more important than raw model selection.
* **Execution is the moat:** “Prompts are bugs, not features.” System-level integration, context packaging, and agent workflow orchestration are competitive differentiators.
* **AI is moving to multimodal & agentic:** Voice, code, and “omnimodal” agents are coming online.
* **MCP is becoming foundational:** Developed at Anthropic and rapidly adopted across platforms, MCP lets developers inject precise, relevant, dynamic context (code, docs, goals) into model or agent workflows. It's powering richer, more robust agentic systems, and is central to orchestrating advanced agents in production. Spec files and registry APIs are coming to standardize and govern MCP use across teams.

**6. R\&D & Training**

* **RL is scaling in post-training:** Ratio of pretrain to RL is moving from 99:1 to as high as 80:20. Training realistic reward functions and environments is both feasible and impactful.
* **Human in the loop is still the bottleneck:** Next-gen agents need to self-evaluate, self-correct, and create their own curriculum for open-ended improvement.
* **Training is accessible and affordable:** It's now possible to train a model using RL for very low cost (e.g., ~$80 for a Qwen 2.5 24B model). Outputs can be automatically verified using an LLM as a judge for quality, correctness, and specific requirements.

**7. Developer Enablement**

* **Agent platforms and SDKs are proliferating:** AWS (Strands), GitHub (Copilot, @amelie), Microsoft, and Google (Gemini) all releasing dev-focused tools and APIs for agent workflows.
* **Emphasis on harmony between data and application:** Data engineering and application design need to be tightly coupled to enable AI at scale.

**8. Miscellaneous**

* **Enduring the bitter lesson:** Premature optimization is the root of all evil, and it happens iff you hand engineer stuff at a lower level of abstraction than necessary. 
* **Observability and evals:** Most painful part for teams is keeping up with evals and AI progress—automation and systematic reporting are critical.

---

**Bottom Line:**
To stay competitive, focus on **robust eval pipelines, structured specs (not just prompts), improving knowledge retrieval and memory, agent traceability, and fast iteration cycles**. Adopt tools and workflows that prioritize *observability*, *versioning*, and *scalable agent orchestration*—not just raw model performance.
