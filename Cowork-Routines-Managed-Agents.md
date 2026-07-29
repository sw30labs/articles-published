View Nicolas Cravino’s  graphic link# Cowork, Routines, and Managed Agents: Choosing the Right Layer for Agentic Work

*The market is converging around agent infrastructure, but the three models are not interchangeable. They solve different problems at different layers of the stack.*

After a few hours of reading Anthropic’s documentation, I finally had a mental model for when to use each one.

Cowork, Routines, and Managed Agents were all launched in the same period and are all positioned as agent infrastructure. But they are not the same thing.

My context is practical. I have spent almost a year running domain-intelligence newsletters as code-first pipelines. A few months ago I began rebuilding them as SW 3.0 Cowork skills and running both versions in parallel so I could compare outputs and tune the new approach before retiring the old one.

That makes this analysis grounded in migration, not theory.

## The three layers

They are layers, not alternatives:

- Cowork is the operator layer: no-code skills, local state, Gmail and Drive integration, and built-in scheduling.
- Routines is the developer layer: cloud-hosted execution, GitHub triggers, repo-driven workflows, and laptop-off operation.
- Managed Agents is the platform layer: vaults, sandboxing, session logs, and agent-as-product infrastructure.

All three share the Claude core. They diverge on where they run and what they persist.

## A simple decision framework

Stop at the first yes:

1. Is the agent the product? → Managed Agents
2. Is the workflow repo- or code-centric? → Routines
3. Does it need docs, Gmail, or persistent local state? → Cowork
4. Must it run laptop-off? → Use a hybrid model, often with Routines for discovery and Cowork for editorial work

For my newsletters, Cowork wins. The workflow is not product-API-centric, it is not repo-centric, and it needs DOCX, Gmail, and deduped state across runs.

## The real constraint

The non-obvious part is that you cannot consolidate all three into one today. Managed Agents has no scheduler. Routines has no credential vault. Cowork has no cloud execution.

That is why the hybrid pattern exists. Each layer leaves gaps that the others fill.

My rule of thumb is simple: start in Cowork, prove value against a real baseline, and only graduate to Routines or Managed Agents when operational reality forces the shift.

This is still a first draft. If you are running agents in production and disagree with where I drew the lines, especially for non-coding workflows, I would love to hear from you.