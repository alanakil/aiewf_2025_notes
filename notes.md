### AI Engineer World's Fair 2025 - Notes

# Beyond benchmarks: strategies for evaluating LLMs in Production (Workshop)

By: Taylor Jordan Smith, Red Hat

The common path in AI has different levels:
- Level 0: Chatbot for simple QA
- Level 1: Retrieving information and recommending actions
- Level 2: Agents orchestrate low complexity tasks
- Level 3: Agents orchestrate multiple workflows across domains
- Level 4: Real-time cross-domain agent collaboration

Evaluate performance based on the framework/architecture:
- RAG: retrieval and generation metrics (RAGAS)
- MCP: Field extraction accuracy, pipeline completion rate
- Agents: Function calling validity rate, step consistency/reporducibility
- Decision support: User-aligned, judgement heavy outputs; field extraction accuracy; pipeline completion rate


# Piloting agents with copilot

By: Christopher Harrison, GitHub

Coding writing agents heavily rely on seeing the right context: 
- Readable code
- Comments
- Repo structure

Coding agents need and instructions file and a setup file. E.g., `copilot-instructions.md` and `copilot-setup-steps.yml`. These include detailed instructions on how to do certain things or what tools to use. E.g., use X library for Y.
Drafting a good instructions file is not easy and takes time, but it is very valuable. We could even set instrucitons at the org-level and leverage MCP to implement them.

In this lab, they create an issue in GitHub (write docs) and assign it to Copilot, which then completes the corresponding tasks and raises PR for you. How could we implement this in ADO?

The coding agent can run files like running tests to check if they succeed.

Copilot only has write access to the branch corresponding to the issue it was assigned. It does not necessarily have access to external resources. It may access a remote MCP server, but it needs to pass through the firewall.

|      | Completions | Chats/edits | Agent mode | Copilot coding agent |
| Scope | Next few lines | Multi file | Complete tasks | Entire issues |
| Frequency | 100s ms | Seconds | Minutes | 10s of minutes |
| Loop | Inner | Inner | Inner | Outer |
| Dev canvas | VS Code | VS Code | VS Code | GitHub |


# Graph Intelligence: Enhance reasoning and retrieval using graph analytics

By: Alison Cossette, Neo4j

Nodes - entities that have properties
Edges - relationships
Properties - data about the entity

We could leverage our topics in the graph as a property.

Tips:
- Don't add too much unnecessarily. Start small. Do not start with all the data.
- Evals drive the structure.
- Consider using multiple indices to boost efficiency. You can also filter based on properties within one index.
- Track chunk usage frequency.

Why are knowledge graphs important? Because you capture new information encoded in the relationships that is not available via naive RAG.

Think about this: When users prompt the assistant, they are hiddenly navigating the graph!

They keep the images separately in a S3 bucket, but their embedding is present in the graph.

Analysis: 
- Use clustering to create relationships between chunks.
- Community detection for curating and understading data at scale in prod. They use Louvain optimization.
- Look for within cluster cosine similarity; number of chunks in a cluster; text length; drop duplicates. Use these insights to clean up data.
- Gauge the importance of each chunk: use pageRank, betweenness centrality, cooccurrence (establish a relationship between chunks used for the different questions).

# Shipping AI that works: An evaluation framework for PMs

By: Aman Khan, Arize AI

This was a demo of Arize AI which is an observability platofrm to consider along with Weights and Biases, Galileo, among others.

It is worth checking their open source code: they have several LLM as a judge evaluations that we may want to look into like a summarization eval, is this function call the right one to choose? Is the user furstrated? Is the plan ideal, valid or invalid? Emotion detection, toxicity, etc.

Check out coderabbit

# Building the Open Agentic Web

By: Asha Sharma, Microsoft

Maintenance of codebases need not compete with features anymore.

Check out github.com/copilot/spaces where you can talk to an assistant about a project.

In Copilot there now is an ML Engineer Agent called @amelie that can help with ML tasks.

# State of startups and AI

By: Sarah Guo, Conviction

What will happen by the end of 2026?
- <$0.01/token
- Agents ship code to prod
- Voice agents replace text
- Wall E

Key capabilities:
- Reasoning
- Agents
- Multimodality

Token marketshare today:
- 35% Google
- 23% OpenAI
- 17% Anthropic
- 15% DeepSeek

"Last year's model is a commodity"

Thick wrapper recipe: 
- Collect and package context
- Pass to model
- Orchestrate models
- Present outputs to user
- Enable workflows

AI leapfrog effect: Conservative industries like healthcare are now adopting AI fast (Sierra, Harvey, OpenEvidence).

Execution is the moat.

Prompts are bugs, not features.

# The last 6 months in LLMs

By Simon Willison

December: 
- AWS Nova
- Llama 3.3 70B which was comparable to 3.1 405B
- DeepSeek V3 685B

January: 
- DeepSeek r1
- Mistral Small 3 24B ~ Llama 3.3 70B

February:
- Claude 3.7 Sonnet (added reasoning)
- GPT-4.5

March: 
- o1-pro
- Gemini 2.5 pro
- GPT-4o native multimodal image generation

April:
- Llama 4 Scout and Maverick (flop)
- GPT-4.1 (1M context)
- o3 and o4-mini

May:
- Claude 4 Opus and Sonnet
- Gemini 2.5 pro preview

Simon uses the following prompt to gauge intelligence: "Create an SVG of a pelican riding a bicycle.".

Bugs:
- Sycophancy in chatgpt
- Grok white genocide in SA
- SnitchBench

Tools + reasoning = fire

MCP

Lethal trifecta:
- Access to private data
- Takes public inputs
- 


# MCP origin story

By Theodora Chu, Anthropic

It was created at Anthropic to add specific relevatn context to the window which was previously added manually.

Turning point: When coding IDEs adopted MCP.

MCP solves for:
- Agents as the future
- Model agency
- Server-side simplicity

Looking forward:
- Elicitation
- Registry API
- Improved open source examples
- Governance

Eventually, models will be so good that they will write their own MCP server on the go.

# Full spec MCP: hidden capabilities

By Harald Krschner, VS code

Full spec -> richer interactions.

More tools does not equate to better agents.

Tools: dynamic discovery.

Prompts: from static templates to dynamically generated workflows.

Sampling: Allows server to request LLM completions from the client.

Coming: Streamable HTTP, updated auth, community registry, elicitation.

# Make your agents remember what they do

By: Mark Bain, AUS

Attention (gravity) + Diffusion (entropy) + VAEs (Ricci flow) = Assymetries

Memory x Compute = i^2

Universe = network database

Graph is then its hidden causal structure and everythign else is a fuzzy diffusion. Relationships = causal links

LLMs = Correlations + W&B
Graphs = Preserve causality

Reasoning requeires causal links -> GraphRAG is the next big thing

Check out Cognee for AI memory -> mexican standoff between github users.

# Practical GraphRAG

By: Michael Hunger, Neo4j

Recall that LLMs are trained to explore graphs, so they are good at it. 

In GraphRAG, there are ways of doing retrieval:
- Rewrite into a Cypher query
- Get subgraph
- Explore the subgraph

We can also use vector search for chunks and then explore their entities. There are different methods.

Check out the diagrams in my notebook.

# Teaching Gemini to Speak YouTube

By Devansh Tandon, Google

Recommnedation problem: f(user, history/context) ~ Recommendations

Large Recommender Model:
Base Gemini checkpoint + YT info + retrieval ranking = LRM

YT info are tokenized videos. Given video tokens, predict the next video tokens.

Video tokens are based on title, descriptions, transcript, audio and video frames (embed it all).

Check out the SemanticID paper, this is the idea of the presentation.

Continued training to give recommendations but also speak english.
You could then: construct a prompt per user and ask for recommendations. This can handle the hardest rec, but it is very expensive.

Instead, they took the same approach but precalculated recommendations without using user information.

Challenges: vocabulary, freshness, scale. E.g., it needs to be able to recommend new important videos very quickly, so this requires the LRM to be trained in the scale of hours.

Future:
- LLMs augment recommendations.
- Search and recs lines blur.
- Recommendations -> generated content.

# Buidling agents at cloud scale AWS

By: Antje Barth, AWS

- Amazon Q -> dev code CLI, built and shipped in 3 weeks.
- Strands agents -> open source SDK, check out the retrieval tool.
- AWS MCP servers in github.

# Windsurf everywhere doing everything at once

By: Kevin Hou, Head of Product, Windsurf

- Secret sauce: "Shared timeline between humans and AI". Think about the human actions outside the IDE.
- AI needs to do it all: Provision API keys, PRs, wriitng code, etc.
- Windsurf will do it all, and will be ON all the time.
- SWE != Coding
- New model: SWE-1. Some metrics they use: "accept all" rate and cascade contribution rate.
- Buidling an AI company in 2025 demands harmony in data and application.

# A year of progress in Gemini

By: Logan Kilpatrick, Google DeepMind

- They released live: Gemini 2.5 pro - 06-05
- Monthyl tokens: 9.7T -> 680T in a year
- Next for gemini:
    - Universal assistant
    - Native everywhere
    - Personalized
    - Proactive
    - Powerful
    - 10x shipping velocity
- Next for the model:
    - Omnimodal - next video
    - Experiments on diffusion
    - Agentic by default
    - Continue scaling reasoning
    - More smaller models
    - Infinity context
    - Big models
- Future for devs:
    - Gemini embeddings GA
    - Veo 3 and Iamge 4 in API
    - Agents
    - Computer Use API
    - Evals tooling
    - Deep Research API
    - Gemini code CLI
    - Move to a dev focused platform

# Thinking deeper in Gemini

By: Jack Rae, Google DeepMind

Intelligence bottlenecks:
- 2010s ngram models had short context due to exponential storage cost -> Sol'n: RNNs
- 2014 LSTM context is lossy -> Sol'n: Transformers
- 2024: Models are trained to respond immediately (limited test time compute). Want: Spend less compute on easy tasks, and more on hard ones.

Future of thinking: Better reasoning, better thinking efficiency, deeper thinking.

Deep think: Very high budget thinking mode on top of 2.5 pro

# Containing agent chaos

By: Salomon Hykes, Dagger

Want: 
- Background work (needs isolation)
- Rails (need customization, how to test, our practices, etc.)
- Efficient human intervention (multiplayer)
- Optionality (open)

We have the tech: Docker + git + agents

They developed "Container Use" for agents: portable environments that can be used with any coding agent. Resulting artifacts do not pollute the workspaces, but it is all tracked in git. Available on github.

# On engineering AI systems that endure the bitter lesson

By: Omar Khattab, Databricks

- The bitter lesson:
    - When leveraging domain knowledge, we build complicated methods that do not scale.
    - General scalable methods work best
    - Talks about maximizing intelligence
- Takeaway 1: Scaling search and learning works best. The key is what to search and learn?
- "Premature optimization is the root of all evil", Knuth
- Hypothesis: Premature optimization happens iff you hand engineer stuff at a lower level of abstraction than necessary.
- A prompt is a horrible abstraction for programming, b/c it overfits to an LLM, inference time strategy, and formatting.
- Invest in your actual spec: guidelines, evals, code.

# Turning fails into features

By: Vitor Balocco and Rakal Willinski, Zappier

- How not to build agents: prototype -> vibe code -> ship -> profit
    - After shipping, we need to collect feedback, understand data, evals, and iterate

- Collecting feedback: Trace everything and make sure it is reproducible
    - Explicit feedback is rare
    - Implicit feedback: copying a response, turning on/off feature, repeated messages, sentiment, etc.
    - NEED: do a weekly report on these!
- Look at your data: need observability
    - Vibe code your own tooling
    - Every failure should be an eval
    - Aggregations / clustering to identify failure modes
    - Tip: Use reasoning models to explain failures
- Build your evals:
    - Unit-test like evals:grades one iteration. Focus on negative feedback. Test new models on all evals.
    - Trajectory evals: grades the full run. Captures multi-turn criteria - better for agents.
    - Rubric based (LLM as a judge): human defines rubric for specific use cases. Tip: Do not use expected and output, use option_a, option_b.
- Ultimate eval: A/B testing

# Evals are not unit tests

By: Ido Pesok, Vercel

- To make good evals, understand the users and domain
- Avoid data points out of domain
- Collect: thumbs up/dpwn, random samples (100/week), Community forums, Twitter
- Use <xml> tags for evals

# How to train your agent

By: Kyle Corbitt, OpenPipe

- How hard is it to train with RL? They trained a Qwen 2.5 24B for $80 and 1 week of engineering! We need to keep this in mind.
- 2 hard problems:
    - Realistic environment: data needs to be large, diverse and realistic. they sued Enron emails
    - Reward function: Asked Gemini to provide questions based on emails, calibrated an LLM as a judge to determine if the answer is correct, and used this as a reward. In practice, you can add smaller subrewards to steer the answers one way or another. For example, add a reward to lower turn answers (uses less queries), penalize hallucinations (prefer to say IDK)
- Reward hacking: When it does the problem in a high reward manner, but not in the intended one. Again, modify the reward function to penalize these.

# A taxonomy for next generation reasoning models

By: Nathan Lambert, AI2

- The length of a task that AI can do is doubling every 7 months.
- Reasoning models for independent agents need:
    - Skills - ability to solve self-contained problems
    - Calibration - prevent overthinking
    - Strategy (planning, not great yet)
    - Abstraction - break down strategy into tasks (also planning and not good yet)
- Ways to compute rewards: math, code, LLM as a judge
- Skills are empowered by inference time scaling, tools, etc.
- Calibration is currently offloaded to the user. Some models spend 100s of tokens to get 2+3=?
- Strategy:
    - Gap between reasoning models and agents built with reasoning models
    - Reasoning models dive right into it
    - Agents that use reasoning models plan
- Abstraction
    - How to manage memory?
    - How to avoid repeating mistakes?
- o3 is amazing at search, but synthesizing the information requires better planning.
- "RL as the focal point of language model dev"
- Months ago the ratio of pretrianing to posttraining was 99:1. Now it is 80-90:10-20. RL is scaling!

# Towards verified superintelligence

By: Christian Szegedy, Morph Labs

- Bottleneck to AI self-improvement is the human: labels, data, tasks, envs, supervision.
- AI needs open-ended self improvement: compute and agency
- Next gen AI:
    - Will execute safely
    - Within that env, it needs full agency: checkpointing, branching, exploring outcomes, reverting them, etc.
    - Needs to create its own curriculum of problems
    - Learns indefinitely on a growing set of self-posed problems
    - Will be its own verifier and validator

# Trends across the AI frontier

By: George Cameron, Artificial Analysis

1. Reasoning vs non-reasoning models:
    - 10x token usage diff
    - 10x slower
2. Open weights vs proprietary: China dominates open landscape
3. Cost
    - Spread is >500x from gpt-4.1-nano to o3
    - Cost dropped 100x in 2 years
    - Small models are smarter, hardware is better, inference efficiency increased

# Braintrust

- Top AI teams spend >2 hours per day on braintrust (evals)
- Loop is: auto-optimizer, optimizes prompts, helps build datasets, etc.

# 2025 AI Engineering Survey

By: Barr Yaron, Amplify

- 70% use RAG
- 40% use finetuning: LoRA, QLoRA, RL, etc.
- >50% update their models monthly
- >70% update prompts monthly
- 31% have no way of versioning prompts
- >75% use text models
- 37% of those not using audio, plan to
- >90% plan to use agents
- >65% use vector dbs
- 90% say that agents should disclose that they are not human
- Most painful thing: Evals and keeping up with news

# The new code

By: Sean Grove, OpenAI

- Code vs communication -> specs win
- Code is 10-20% impact. Structured communication is 80-90% -> this is the bottleneck
- Vibe coding is versioning the binary and removing the source (prompt)
- A written spec aligns humans. Code is a lossy projection of the spec.


