![](https://media.licdn.com/mediaD4E12AQE1RJ2Q1MHisA)

# [Why Your Agentic AI Pipeline Might Not Need Code](https://www.linkedin.com/pulse/why-your-agentic-ai-pipeline-might-need-code-nicolas-cravino-nhine)

*Created on 2026-02-11 04:39 · Published on 2026-02-11 22:00*

> The real shift is not from code to no code, but from infrastructure-heavy orchestration to inference-native execution.

I built *Article Buddy* to solve a personal problem: I write long-form technical articles, and I wanted an AI-powered editorial pipeline that could review my drafts the way a real publishing team would. Not a chatbot. A multi-stage system where specialized personas—a developmental editor, technical reviewers, a market analyst, a copy editor, a QA validator—each take a pass at the manuscript in sequence, improving it at every stage.

Three months. That's what Article Buddy took—nine stages of editorial processing, each a specialized LLM persona orchestrated through LangGraph, conda, YAML configs, temperature tuning, and the full infrastructure theatre. Beautiful machinery. I was proud of it.

Then I opened Claude in Co-work and decided to test something reckless: what if I handed Claude the entire YAML config—all nine personas, their prompts, their model settings, their orchestration sequence—and said, "Build this without code"?

No pip. No conda. No Python runtime. No state machines. No deployment.

Claude mapped each LangGraph node to a task subagent. Created the same flow. I ran the first article through it.

The output was indistinguishable.

I saved the entire thing as a reusable **skill** in two hours.

The infrastructure layer—all three months of Python work—had become optional. Not through gradual refactoring. Not because I was clever. But because the code was never the product. The YAML was. The nine personas, the prompt choreography, the knowledge retrieval logic—that was the actual thing. The code was just the carrier. And the inference provider's native orchestration had made the carrier redundant.

> This is not a product pitch. This is an anatomy lesson in where the AI industry is headed, and why the infrastructure-first model that dominated 2021-2024 is now economically broken.

---

## The Stack That Built Too Much

For roughly three years, building an agentic application followed a rigid, almost ceremonial formula: **Python** + **LangGraph** + **Docker** + **API key vault** + **monitoring** **infrastructure** + **logging** + **vector** **database** + **deployment** **orchestration** + **DevOps** **overhead**.

The assumption was unspoken but total: the intelligence of an agentic system requires orchestration code. You needed explicit state machines. You needed routing logic. You needed deterministic control over execution paths. You needed engineers who understood async serialization, token limit management, and sampling parameter tuning.

That assumption was defensible in 2022. It is now a luxury nobody can afford.

**Here's what actually happened:** in my experience observing dozens of agentic projects, roughly eighty percent became infrastructure projects rather than intelligence projects. Teams spent cycles wrestling with container runtimes, debugging serialization errors, managing vector embeddings, and tuning sampling parameters—not designing personas, iterating prompts, or thinking about workflow intelligence. The actual business value (better writing, faster analysis, smarter decisions) remained trapped behind walls of middleware.

The cost signals are impossible to ignore. McKinsey found that 88% of organizations now use AI in at least one business function — but only 39% report any measurable EBIT impact. The money is going somewhere. It’s going to infrastructures. Token usage runs unmonitored. Gartner reports that 68% of enterprises are now battling unauthorized AI usage because teams spin up shadow apps to avoid procurement delays, creating PII exposure and compliance nightmares. The infrastructure meant to contain risk has become its own risk vector.

Meanwhile, market demand is accelerating. Gartner forecasts that 40% of enterprise applications will incorporate AI agents by 2026—up from less than 5% today. If you're still building agentic systems the old way, you're about to get run over.

> The signal is loud: the infrastructure-first model is broken.

---

## The Two Layers Every Agentic System Has

Any agentic application, once you look at it honestly, decomposes into two independent layers that don't need to live together.

**The intelligence layer:** prompts, personas, decision rules, knowledge retrieval patterns, output validation. This is the value. This is where domain expertise lives. This is what changes with iteration.

**The infrastructure layer:** state machines, graph topology, deployment orchestration, monitoring, persistence. This is the scaffolding. This is operational overhead.

Article Buddy is the perfect anatomy lesson.

The intelligence lives in **YAML**. Nine editorial personas, each encoding decades of publishing expertise. The developmental editor spots narrative gaps. The technical reviewer validates accuracy. The market analyst asks whether anyone cares. Each has its own system prompt, temperature setting, knowledge preferences, and output validation rules. This is the program—the actual decision-making logic.

The infrastructure? All **Python**. The LangGraph state graph, the sequential node execution, the state passing logic, the YAML loader, the output parser. Competent code. Useful code. But code that carries something else.

> Andrej Karpathy captured this insight precisely: "Software 3.0" means the programming interface is no longer code. The programming interface is natural language. The YAML config—those prompts, those orchestration sequences—is the program. The Python is the runtime.

The inference providers have figured this out. Every major player now offers native task sequencing, tool use as a first-class citizen, structured output validation, agent execution, and integrated knowledge retrieval. When the infrastructure provider handles orchestration natively, the orchestration code becomes inert. You're no longer buying Python execution; you're buying orchestration as a service.

That's what happened with Article Buddy. The intelligence was always inference-native. The code was never necessary—it was just the first mechanism we had to make it work.

---

## How I Moved Nine Agents from Code to Skill

This works in theory. Let me show you it works in practice.

Article Buddy's architecture: nine sequential agents in a LangGraph StateGraph. Developmental editor, then technical reviewers, then market impact, then copy editor, then QA validator. The YAML specifies each agent's system prompt, model, temperature, output format, knowledge retrieval preferences, and validation rules.

The challenge Claude Cowork presented was real: no Python runtime. No pip. No subprocess calls.

But **Claude Cowork has task subagents**. It has native tool use. It understands structured output validation. It has built-in web search and file retrieval as native operations. It maintains context across sequential operations.

**So I did something simple:** I took the YAML config and described it in natural language. I said, "*Here are nine editorial personas defined by these prompts. Here's the sequence they operate in. Here's what each one validates. Here's what knowledge they need. Orchestrate this.*"

Claude didn't rewrite the Python. Claude read the personas, understood the pattern, and mapped each LangGraph node to a task subagent. Sequential state passing became a series of structured operations. Knowledge retrieval became access to live search and embedded file reading.

I tested it on a 2,500-word article. Timing was faster than the Python version. Cost per run was lower. Output quality was identical.

Then I iterated. Refined the knowledge preferences. Tweaked one persona's output validation. Added a feedback loop to the QA agent. Each iteration took minutes. The same iteration in the Python version would have taken hours—a code review, a deployment, waiting for the container to rebuild and push.

After two hours of iteration, the thing was production-ready. I saved it as a reusable skill. The entire infrastructure layer—all the Python, all the deployment wiring—had become dead code.

---

## When to Port, When to Keep Building Code

This is not an argument that every agentic system should be a skill. That would be absurd.

**Skill-native problems:** Sequential prompt orchestration. Text-based output. Workflows that benefit from web search or live knowledge. Human-in-the-loop operations. Speed-to-market matters more than fractional cost optimization. Iteration by domain experts is a competitive advantage.

**Code-native problems:** Tight deterministic loops. Batch processing at scale. Sub-second latency requirements. Persistent database connections. Exact reproducibility. Strict audit requirements in regulated industries.

**Hybrid patterns:** The intelligence (decision-making, orchestration) runs as skills. The hands (APIs, data transformations, database updates) run as code. This is the pragmatic middle ground for most enterprise workflows.

The trade-off table is unambiguous:

![](https://media.licdn.com/dms/image/v2/D4E12AQG0hkaY78Ytfw/article-inline_image-shrink_1500_2232/B4EZxLCZGxGoAU-/0/1770785445226?e=1775692800&v=beta&t=GoygXZP9Y2d17wC2e53fsImK8ThNCWkRYQzjDy_imsc)

**The honest answer:** if your problem is sequential prompt orchestration with text output and tolerance for multi-minute latency, use a skill. If your problem requires determinism, speed, or tight control, use code. Most enterprise workflows are actually 70% sequential orchestration and 30% deterministic logic—which means hybrid is your real answer.

---

## The Lock-In Question

Skills are provider-specific. A Claude skill is a Claude skill. You cannot trivially port a skill from Claude to OpenAI because the execution models differ fundamentally.

Lock-in is real. It matters.

Here's the honest picture of what's portable and what isn't:

**Portable**: Tool definitions (Model Context Protocol helps here). Prompt text. Knowledge files. Orchestration patterns documented in writing. System design patterns.

**Provider-specific:** How tasks are sequenced natively. How context flows. Latency and streaming characteristics. Cost structures. Native capability availability.

The market is signaling convergence. OpenAI signaled a strategic shift toward Responses as the native agentic interface. Anthropic is building skills with portability in mind. The industry is coalescing around inference-native execution.

**The pragmatic mitigation:** use Model Context Protocol for tool definitions; keep prompts in version control; document your orchestration patterns in natural language; accept that critical infrastructure stays in code; choose your inference provider the way you choose a cloud—understanding the lock-in but accepting it as a solved problem, like choosing AWS versus Azure.

**The hard truth:** perfect portability is impossible. But documented, pattern-based portability is achievable. And the productivity gains from inference-native execution dwarf the lock-in cost for most workflows.

---

## Security in a Provider-Hosted Model

When you ran agentic systems in Python, you controlled the execution runtime. You could inspect every decision. When you move to skills, the inference provider controls execution. You specify what you want; they decide how to achieve it.

This is a fundamental inversion of control, and it creates new risks worth taking seriously—but also new enforcement capabilities worth leveraging.

**New attack surface:** Execution opacity. Reduced audit trail granularity. Data residency concerns. Tool access control delegation.

**Mitigations that work:** Input/output validation at boundaries. Tool whitelisting and capability restriction. Provider audit logs ingested into your SIEM with real-time alerting. Data classification policies. Vendor security questionnaires and compliance attestation (SOC 2, ISO 27001). For regulated domains (HIPAA, SOX), explicit provider attestation of audit immutability.

**The honest trade:** You have less visibility into execution, but enforcement is stronger. A rogue engineer cannot modify your skill's logic at runtime. The provider's infrastructure enforces the skill's behavior. You're trading internal control for systemic enforcement.

This is the right trade for many workflows. It's not the right trade for HIPAA workflows or financial institutions where audit trails must be immutable and internal, and where you need attestation that every decision is auditable to the source system. In those cases, the orchestration code stays in your perimeter. Governance operationalization—SIEM integration, vendor questionnaires, data classification—should be a standing practice before moving any production workflow to provider-hosted execution.

---

## What You Actually Gain

> When you move intelligence from code to skills, something counterintuitive happens: you get capabilities you didn't have before.

Live knowledge integration at every stage without building and maintaining vector databases. The skill can access live search results and retrieve documents as native operations. No embedding management. No similarity scoring tuning. No stale vector indexes.

Faster iteration cycles that collapse from days to minutes. A prompt engineer can test five variations of a persona in an hour. The same engineer updating a Python app spends a day on code review, testing, and deployment. By the end of the quarter, the skill version has been refined forty times; the code version has been updated twice.

Cost transparency that actually works because you see the token budget per operation. You're not estimating infrastructure utilization; you're metering actual inference cost.

Democratization of capability design. Domain experts who don't code can now modify skills. A publishing expert can iterate the copy editor persona without asking engineering. A compliance officer can tighten validation rules without waiting for a code change. The people who understand the problem own the solution.

Article Buddy saw this directly. I iterated the copy editor persona five times in one afternoon. Tested against the same article. Measured output quality. Refined. The same work in Python would have consumed a week. The skill-based version is measurably better because iteration was cheap enough to be exploratory rather than surgical.

---

## What's Coming and Why You Should Move

2022-2024 was the era of LangGraph and orchestration code. It solved a real problem at the time because inference providers didn't expose orchestration primitives. You had to build them yourself.

2025-2026 is the transition. Skills and inference-native agents are now viable for the majority of agentic workflows. Teams that adopt skills now gain a competitive advantage in iteration speed and cost. They're shipping faster. They're experimenting more. They're building institutional knowledge about what works in their domain.

By 2027-2030, skills will be the default for orchestration. Microservices will shrink. Hiring will shift toward prompt engineers and domain experts. Organizations that didn't transition will find themselves maintaining expensive infrastructure for problems that no longer require it.

> The real question is not "*Is this real?*" It's already real. The question is: "*How do I transition without breaking everything I've built*?"

---

## Your Actual Next Steps

**First:** Audit one of your existing agentic systems. Map out which parts are intelligence (prompts, personas, decision logic) and which parts are infrastructure (orchestration, state management, deployment). You'll find that the majority of the code is scaffolding.

**Second:** Pick a low-stakes workflow. Convert the intelligence layer to a skill. Keep the critical code. Measure the difference in iteration speed and cost. Get real numbers.

**Third:** Update your capability roadmap. Hire for prompt engineering and orchestration design. Train domain experts to iterate skills directly. Accept that your infrastructure engineers will own less and your prompt engineers will own more. This is a hiring and organizational change conversation, not just a technology conversation.

**Fourth:** Design governance for provider-hosted execution. Input/output validation at boundaries. Tool whitelisting. SIEM integration. Compliance attestation. Make peace with the inversion of control. Document your data classification policies. For regulated workflows, clarify with your provider what attestations they can provide.

**Fifth:** Plan your vendor strategy. Use Model Context Protocol for tools. Version your prompts in your repository. Document your patterns. Choose your inference provider knowing you're committed, but knowing it's a solved problem.

---

## The Hard Truth About Transition

Article Buddy proves this isn't theory. The question is not whether the shift is real. The question is whether you lead the transition or get led through it.

By 2027, infrastructure-first agentic systems will look like Hadoop clusters—powerful, proven, but expensive and increasingly irrelevant for new work. The industry will have moved past them.

The organizations that transition early get a year of competitive advantage in speed and cost. They're staffed for the new model. They've iterated their governance patterns. They understand how to move fast without creating compliance disasters.

The organizations that transition late spend two years maintaining legacy infrastructure while competitors build ten times faster.

This is not a technological forcing function. It's an economic forcing function. Your competitors will build faster, cheaper, and better. The question is whether you want to compete with them or not.

The infrastructure mirage—the belief that agentic systems require elaborate orchestration code—is fading. The reality underneath is simpler and more powerful: prompts and personas, executed natively on inference providers, with governance and validation at the boundaries.

Article Buddy was the proof. The skill was the point. ***Everything else was optional scaffolding.***

The only real question now is: what are you waiting for?