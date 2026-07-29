
Nicolas Cravino
   • You
AI Engineer | Cybersecurity | Agentic AI Innovator | Author | 20+ Years in Finance & Consulting
2w •  

I've been asked the same question a few times now - "you keep talking about these loops. Ralph, autoresearch, rubrics… what's actually the difference?"

Fair question. So I drew it.

The overlap is bigger than the differences. All three are the same animal at the core: an iterative agent loop, durable state kept outside the context window, human sets the goal once and steps back. The intelligence isn't the model - it's the loop plus the check.

The axis that actually matters: who holds the evaluator - a deterministic check, or another LLM.

Ralph (Wiggum) loop - fresh context every iteration, one unit of work at a time, runs until the backlog is empty. Use it when you have a spec or PRD and the work decomposes. Fresh context is the feature: no rot, no drift.

Karpathy-style autoresearch - keep/rollback against one FIXED metric. Use it when you can measure the thing you want (latency, accuracy, cost) and want the loop to discover gains you never specified. The metric is the safety rail.

RubricMiddleware - LLM-as-judge, per-criterion feedback. Use it when quality is fuzzy and no metric exists - writing, analysis, taste. Powerful, but judges drift, so keep it bounded and in-session.

And they compose. Ralph with a rubric gating each iteration - build to a spec AND a quality bar. Autoresearch inside a Ralph backlog for the hot paths. My default hybrid: LLM proposes, deterministic check disposes.

Rule of thumb - if the check can be code, make it code. That's the version you can safely run overnight. If it can't, put an LLM in the judge seat, on a short leash.

What loops are you running?

hashtag#AgenticAI hashtag#AIAgents hashtag#AgenticLoops hashtag#AIEngineering hashtag#ContextEngineering
Venn Diagram here depicted.


Discovery

549
Impressions
In-network (followers and connections)
46%
Out-of-network
54%
329
Members reached