# Ralph, Autoresearch, and Rubrics: What Is Actually Different?

*The overlap between these loops is bigger than the differences, but the evaluator is what really changes the behavior.*

I have been asked the same question repeatedly: “You keep talking about Ralph, autoresearch, and rubrics. What is actually the difference?”

The short answer is that all three are iterations of the same core pattern: an agent loop, external state, and a human who sets the goal once and then steps back. The intelligence is not only in the model. It is in the loop plus the check.

The real axis of difference is who holds the evaluator: a deterministic check or another LLM.

## Ralph loop

The Ralph loop gives the agent fresh context at each iteration and works one unit of work at a time until the backlog is empty.

Use it when you have a spec or PRD and the work decomposes cleanly. Fresh context is the key feature because it reduces drift and rot.

## Karpathy-style autoresearch

Autoresearch keeps and rolls back against a fixed metric. Use it when you can measure what matters — latency, accuracy, cost, or another concrete objective — and want the system to discover gains you did not specify in advance.

The metric acts as the safety rail.

## RubricMiddleware

Rubric-based loops use an LLM-as-a-judge with per-criterion feedback. Use them when quality is fuzzy and there is no clean metric: writing, analysis, taste, or nuanced evaluation.

These are powerful, but they are more prone to drift, so they should stay bounded and in-session.

## How they compose

They work well together.

- Ralph with a rubric can build toward a spec and a quality bar.
- Autoresearch can run inside a Ralph backlog for the highest-impact paths.
- My default hybrid is simple: the LLM proposes, and the deterministic check disposes.

## A practical rule of thumb

If the check can be coded, make it code. That is the version you can safely run overnight. If it cannot, put an LLM in the judge seat, but keep it on a short leash.

What loops are you running?