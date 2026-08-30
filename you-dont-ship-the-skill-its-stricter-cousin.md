# [You Don’t Ship the Skill. You Ship Its Stricter Cousin](https://www.linkedin.com/pulse/you-dont-ship-skill-its-stricter-cousin-nicolas-cravino-ki3sc)

Published on 2026-08-11 12:00

Here’s what we were trying to do.

I had built an agent skill – a personal side project - a SKILL.md playbook plus reference files that an AI agent reads and follows. It worked super well. So well that the obvious next step was to turn it into a product: a web app version. Faster, cheaper, no file-reading overhead, no agent loop — a clean scoring service instead of a coaching agent reading documents.

> The plan seemed straightforward: extract the skill’s rubric and logic into prompts, verify the app scores the same as the skill, ship it.

That plan contained a flawed assumption we didn’t know we were making: that a skill could be converted into a web app and keep its behavior. That if we matched the formulas, the weights, the bands, and the penalties closely enough, the scores would converge.

Two of us. Just under three months (working only on weekends on this project). Five rounds of recalibration. Every formula, weight, band, and penalty verified byte for byte.

And the score still sat a full point below the reference.

Last weekend I found out why. It took one afternoon. I’m sharing it because I didn’t know this gap existed — and I suspect most teams productizing a skill right now don’t either. My pain, your gain.

### The discovery

Same model. Same question. Same answer, word for word. The only thing I changed was what the judge was allowed to read.

- The skill, run within Claude -Cowork: scored 4.73
- A hand-built prompt carefully distilled from the skill: scored 3
- An agent with no access to the skill files: scored 3
- An agent reading the actual skill files: scored 4

> The residual gap wasn’t drift in anyone’s code. It’s structural. Nobody’s bug.

The one-liner: a skill’s calibration lives in the whole document — rubric, worked examples, pushback flow, tone. Any prompt extracted from it drifts strict, roughly a point on average. “Aligned to the skill” is a property of reading the skill, not of rewriting it.

### What I learned (so you don’t have to)

1. Don’t promise parity. Promise a documented mapping. Decide whether you’re shipping the skill’s behavior or a strict-mode variant of it — and say which, in writing, with numbers.
2. Run the same input through both judges before you launch. One fixed baseline, verbatim, through the skill and through your app. The diff shows you exactly where your extraction added teeth. It costs an afternoon. Almost nobody runs it. (We didn’t. For nearly three months.)
3. Diff to remove unintended strictness — not to reach the skill’s number. Some of your offset is bugs. Fix those. The rest is structural, and no amount of prompt tuning closes it, because the target behavior isn’t written down in any prompt.
4. Freeze the rubric, version it, publish the offset. A stricter, stable, documented gate is a legitimate product decision. A moving offset is the worst of all worlds.
5. An agent that loses access to its skill doesn’t error. It improvises. It grades from whatever the base model carries in its weights — confidently, and only sometimes does it tell on itself. Alert on it like a database outage.
6. If you truly need parity, serve the skill itself. It works today, at 3–4× the latency per verdict. That’s a business decision, not a technical one.
7. Extraction flattens more than scores. Our coaching skill lost its pushback loop, its fatigue budget, its “want to revise, or shall I flag this?” conversation. Decide deliberately what your product keeps.

### Why this matters beyond my project

Skills are becoming a distribution format — Anthropic’s Agent Skills, LangChain’s DeepAgents, the whole industry converging on SKILL.md plus reference files. The obvious commercial move is exactly the one we made: take a skill that works and distill it into a fast, cheap app.

That’s the trap, and it’s a pleasant one to walk into. Every step is a good engineering decision — and the destination is a product that doesn’t do what its label says. You don’t ship the skill. You ship its stricter cousin, and name it after the skill.

And it’s not just coaching apps. Anywhere a rubric or playbook gets distilled into a grader prompt — eval harnesses, content moderation, compliance screening, hiring rubrics — the operationalized version adds teeth the original never had. If your gate grades stricter than the policy it claims to implement, your thresholds, your vendor comparisons, and your audit trail are all quietly miscalibrated.

---

### TL;DR — the boring bits

- The setup: my skill — a coaching agent that runs a structured, multi-part interview, scores every answer on a specificity rubric, and pushes back on vague ones — vs. a web-app rebuild of the same flow by the product team. The skill scores our fixed 36-answer baseline at 4.73 (A). After five rounds between mid-June and early August, the app stalled at 3.75 (C) — a stubborn −0.98.
- Round 3 proved the app runs the skill’s scoring spec byte for byte. So the gap wasn’t the formula. It was rubric severity: the rebuilt judge demanded machine-checkable structure the skill never asked for — named individuals, numeric thresholds in fixed patterns, per-route trigger conditions.
- The experiment: three judges, one model (open-weight, run locally, production temperature), one question, one answer verbatim. Distilled prompt → 3. Agent with no skill access → 3. Agent reading the real skill files → 4 — graded in the skill’s own vocabulary, using its pushback protocol.
- Judge 2 is the load-bearing control: same agent architecture, files unreachable. It scored 3. So the agent loop buys nothing — what moved the score was what the agent was allowed to read.
- Reproduced through the real production pipeline: 3, 3, 3 vs. 4, 4, 3. A distribution shift with normal variance — roughly a point on average, not a deterministic +1. One controlled experiment, not a universal constant.
- Bonus gotcha: the skill-less agent downgraded its own confidence and flagged it “couldn’t verify the exact rubric text” — then graded from priors anyway. An empty skill catalogue is a legal state; nothing raises. Assert a non-empty catalogue at startup, and treat a zero-file-read verdict as a failed request, not a fast one.
- Your three options: keep diffing prompts (has a floor — removes unintended strictness only), freeze a strict mode and publish the mapping (the honest end state), or serve the skill itself (214s vs. 61s per verdict in my spike — if that doesn’t fit your request path, run it nightly as a calibration oracle and publish the offset).

### Bottom line

The skill is the spec. If you want the skill’s behavior, read the skill. If you want something faster and stricter, fine — freeze it, measure the offset, publish the mapping, and sell it for what it actually is.

What you can’t do is tune your way to a target that only exists as the-skill-read-by-a-model.

Five rounds taught us that. One experiment told us why.

("Views my own; this describes a personal project")
