View Nicolas Cravino’s  graphic link
Nicolas Cravino
   • You
AI Engineer | Cybersecurity | Agentic AI Innovator | Author | 20+ Years in Finance & Consulting
3mo •  

A few hours of Anthropic documentation later, I finally have a mental model for when to use what.

Cowork. Routines. Managed Agents. All shipped in the same quarter. All positioned as 'agent infrastructure.' Not the same thing.

Context: I've been running several domain intelligence newsletters as code-first pipelines for almost a year. A few months ago I started rebuilding them as SW 3.0 Cowork skills, running both versions in parallel — same sources, same delivery, different engines. Still comparing outputs and tuning the SW 3.0 versions before I retire the code.

That's the lens for this analysis. Active migration, not greenfield design.

— — —

They are layers, not alternatives:

▸ Cowork = operator layer (no-code skills, local state, Gmail/Drive, built-in cron)
▸ Routines = developer layer (cloud-hosted, GitHub triggers, repo push, laptop-off)
▸ Managed Agents = platform layer (vault, sandbox, session log, agent-as-product)

All three share the Claude core. They diverge on where they run and what they persist. (Image 1: Venn)

Mapped against a real pipeline — discover, analyze, deliver — each one has a distinct sweet spot and a distinct gap. (Image 2: capability table)

— — —

Four questions. Stop at the first yes. (Image 3: decision tree)

1. Is the agent the product? → Managed Agents
2. Code/repo-centric? → Routines
3. Needs docs/Gmail/state? → Cowork
4. Must run laptop-off? → Hybrid (Routine for discovery, Cowork for editorial)

For my newsletters, Cowork wins. Not a product API, not repo-centric, needs DOCX + Gmail + dedup state across runs.

— — —

The non-obvious bit: you cannot consolidate all three into one today. Managed Agents has no scheduler. Routines has no credential vault. Cowork has no cloud execution. The hybrid pattern exists because each layer leaves a gap the others fill.

My rule: start in Cowork, prove value against a real baseline, graduate phases to Routines or Managed Agents only when operational reality pushes you.

First draft. If you are running agents in production and disagree with where I drew the lines — especially for non-coding workflows — I want to hear it.


439 impressions