![](https://media.licdn.com/mediaD4E12AQEeWBxZZCc5aQ)

# [ASICs vs. GPUs was never the final boss. The grid is.](https://www.linkedin.com/pulse/asics-vs-gpus-never-final-boss-grid-nicolas-cravino-7s2ye)

Created on 2025-12-15 00:51

Published on 2025-12-15 01:22

### ASICs vs. GPUs was never the final boss. The grid is.

(Follow-up to: “[Will ASICs Dethrone GPUs for LLM Inference?” - July 12, 2024](https://www.linkedin.com/pulse/asics-dethrone-gpus-llm-inference-nicolas-cravino-bfsue))

December 13, 2025

In July 2024, I asked a provocative question: Will ASICs dethrone GPUs for LLM inference?I’ll say it plainly: the direction was right, but the question was incomplete-and that’s the point.

Not because GPUs “lost.” NVIDIA is still the ecosystem king.

But because the world’s biggest AI players did what they always do when something becomes strategic:

They stopped renting the future and started manufacturing it.

Back then, the bottleneck looked like compute scarcity: “There aren’t enough GPUs.”

Today, the bottleneck is evolving into something more fundamental:

We’re not running out of chips. We’re running out of deliverable power-and the ability to get it to the right place, on the right timeline.

And if you’re a Cyber Security leader reading that, here’s the uncomfortable translation: availability risk is becoming energy-shaped. You can have impeccable controls, hardened clusters, signed artifacts, audited pipelines-and still lose the quarter because the utility can’t deliver the power you assumed would be there.

---

### The original formula: Model + Weights + Compute

For a while, the winning AI stack looked like a three-piece combo meal:

* **The model** (capability, architecture, training recipe)
* **The weights** (the “compiled experience” of that training)
* **The compute** (the hardware that turns weights into tokens)

*The catch:* compute was a third-party dependency. You bought GPUs. You rented GPUs. You waited in line for GPUs.

Then hyperscalers made the obvious move: they internalized the constraint.

A familiar pattern: when something is both scarce and strategic, it stops being a vendor line item and becomes a core competency. That’s not ideology-it’s survival.

> In AI, compute isn’t a purchase-it’s a supply chain.

---

### The 2025 update: “Fine. We’ll build the compute too.”

In early December 2025, AWS announced or previewed Trainium3-a next-gen proprietary chip aimed at both training and inference.

**AWS** has described *Trainium3* in terms of improvements relative to Trainium2, including higher compute, improved efficiency, and larger-scale configurations. AWS has also pointed to customer anecdotes suggesting meaningful cost improvements versus comparable GPU-based systems, and signaled a stronger push toward a unified training and inference platform.

And AWS isn’t alone.

**Google** has been on this path the longest with **TPUs**, tightly coupled with its software stack (XLA, JAX, TensorFlow, and increasingly PyTorch/XLA). **Microsoft** is building *Maia*. Everyone wants the same prize:

*Better performance per watt, better dollars per token, and less dependence on a single vendor’s roadmap.*

So yes: ASICs didn’t just “arrive.” They became inevitable.

**But here’s the twist:** even if you win the chip game, you can still lose the power game.

> Custom silicon is a competitive advantage-until power turns it into a paperweight.

---

### When you own the compute, the “third party” becomes energy

Once you have:

1. the model
2. the weights
3. the compute

...you realize you still don’t control the one resource that actually runs the whole machine:

*the juice.*

And “juice” isn’t just electricity. It’s:

* generation capacity
* transmission availability
* interconnect and congestion constraints
* substation buildouts
* transformer procurement timelines
* cooling infrastructure (and heat-rejection limits)
* water access (in many regions)
* permitting timelines
* land and proximity to fiber
* political tolerance for a new mega-load showing up

A modern AI data center isn’t just a building full of servers.

It’s a new kind of industrial plant.

A quick reality check (the kind you hear in a war room): you can procure racks in months, but you can wait much longer for interconnect approvals, substation upgrades, transformer delivery, and new generation to come online. The lead-time mismatch is now the story.

So the question becomes less “GPU vs. ASIC” and more:

### Are hyperscalers turning into energy companies with APIs?

If the grid can’t satisfy demand at the rate AI is scaling, the strategic play is obvious:

* You can’t deploy what you can’t power.
* You can’t monetize what you can’t keep online.
* You can’t win the inference market if latency matters and your capacity is rationed.

**Here’s the operational analogy:** we used to treat electricity like always-on background infrastructure, the same way teams used to treat bandwidth as infinite-until streaming, mobile, and cloud rewrote the rules. AI is doing that to power.

**Ethical and business implication:** when power becomes the bottleneck, who gets served first becomes a governance question, not just an engineering one. Priority access will tilt toward deep-pocketed incumbents, reshaping competition-and potentially public trust-unless leaders plan for transparency and fairness.

So what happens next?

I see three realistic paths (and one science fiction that might age into science).

> The next cloud war isn’t over chips. It’s over megawatts.

---

### Path 1: Buy power smarter (short-term)

This is already happening:

* long-term power purchase agreements
* co-location near cheaper power
* aggressive efficiency improvements (liquid cooling, better PUE, higher rack density)

This is the finance-and-ops route: don’t build power-out-contract it.

But contracts don’t create electrons on demand. *They mostly allocate them.*

And allocation becomes a security and resilience problem. When power is constrained, you don’t just negotiate price-you negotiate priority. That can show up as:

* curtailment clauses that force load shedding
* demand-response programs that trade uptime for rebates
* capacity-reservation models that behave like throttling

In other words: your inference SLO can become a function of grid conditions, not engineering intent. More often than not, the pain won’t be total blackout-it’ll be capacity ceilings, throttling, and regional allocation games.

Cyber-adapted example (what this looks like in a SOC ticket):

*On a Monday morning, your SOC sees a spike of API 504s on your internal LLM gateway, plus unusual retry storms from downstream services. The first hypothesis is a DDoS attack or a WAF regression. But your cloud provider status page is green. The clue is in a different telemetry stream: your facility power budget was temporarily capped (a demand-response event), so the platform scheduler started shedding non-critical inference capacity. The “attack signature” is self-inflicted backpressure*.

### What this means in production (orchestration, not theory)

If you run an internal LLM gateway (many enterprises do, even if they don’t call it that), treat energy and capacity the way you treat any other regional dependency: as first-class signals in routing and rate limiting.

**Pragmatic pattern:** capacity-aware routing + graceful degradation

* Maintain per-region capacity budgets (tokens/sec, concurrent requests, max cost/min, and-when available-cluster headroom).
* Route requests by SLO class:
* Interactive: low latency, smaller context, stricter timeouts
* Batch/agentic: higher latency tolerance, queueable, preemptible
* Define degradation ladders:

1. Switch to a smaller model or lower reasoning mode
2. Reduce max tokens or truncate context
3. Shed optional tools (web browsing, long retrieval)
4. Queue non-urgent workloads
5. Fail closed vs. fail open, depending on policy (security workflows usually fail closed)

> In the AI era, reliability isn’t a single-region SRE problem-it’s a real-time routing problem.

---

### Observability you’ll wish you had before the first incident

**The uncomfortable truth:** most organizations instrument AI like it’s a normal web app-then act surprised when the failure mode is completely different.

Classic uptime monitoring catches “latency is up.” It usually does not catch why latency is up: token throughput limits, retry amplification, queue backpressure, capacity curtailment, or silent regional quota ceilings. And when the constraint is power or capacity, your system’s default behavior-retries-often turns a brownout into a full outage.

What you want instead is observability that treats tokens, queues, and capacity as first-class signals-because that’s the real “physics” of AI systems in production.

* Gateway metrics: QPS, retries, queue depth, 429/503 rate, per-route latency
* Model metrics: tokens in/out, decode latency, tool-call counts, cache hit rate
* Capacity signals: scheduler headroom, region quotas, curtailment events (where available)
* Correlation IDs across retries (to prevent “ghost incidents” caused by client storms)

If you can’t measure token flow and retry storms, you don’t have observability-you have vibes.

---

### Path 2: Co-build power (mid-term)

This is where things get interesting-and where the conversation stops being “AI engineering” and starts being strategic operations.

If your data center is a sustained heavy load, you’re incentivized to treat power like a first-class component of the AI stack. Not as a line item-as a gating dependency that shapes product commitments, customer SLAs, and even which models you can reliably offer. The cost of a bad retry policy isn’t just downtime. It’s wasted compute spend, degraded customer trust, and an incident narrative you can’t explain.

Possible moves:

* On-site generation (gas turbines as bridging supply)
* Dedicated renewables plus storage (better optics, hard engineering)
* Small Modular Reactors (SMRs) (politically hard, strategically powerful)
* Microgrids that reduce dependency on fragile regional constraints

This isn’t “cloud provider builds a power plant” in the cartoon sense. It’s more subtle-and more consequential: the cloud provider becomes an anchor tenant for new generation, and power projects become part of the compute roadmap.

If you’re a company shipping proprietary chips (for example, Trainium, TPU, Maia), you don’t just roadmap silicon. You roadmap power availability.

*And that changes governance.*

Risk leaders who used to treat “data center risk” as a vendor questionnaire now have to reason about:

* Grid dependency and single points of failure outside your physical perimeter
* Microgrid controls as OT/ICS-adjacent security scope
* New third parties (utilities, EPC contractors, fuel logistics)
* Incident response where the root cause is an energy event, not a cyber event

If microgrids and load controllers become part of uptime, they become part of the threat model: segmentation, least privilege, logging, and change control. Treat them like Tier 0 infrastructure.

Power-aware AI isn’t just resilience. It’s also how you avoid quietly shifting scarcity costs onto everyone else-brownouts, higher prices, and higher emissions. Leaders will increasingly be asked to justify not only model behavior, but infrastructure choices.

> The next AI moat won’t be a model. It will be megawatts-secured, governed, and contracted.

---

### Enterprise integration reality: energy-aware reliability becomes an architectural requirement

If you’re building internal AI platforms, the practical enterprise move is to separate:

* Control plane (routing, policy, budgets, queueing, audit)
* Data plane (actual model endpoints: GPU/ASIC, self-hosted or vendor)

So when capacity shifts (for any reason-power caps, chip shortages, regional quota), you can move the workload without rewriting the application.

**In other words:** you’re not building an AI app. You’re building a market for compute inside your company-with routing, pricing (budgets), priority, and rules. That’s what control planes are: an internal economy for scarce resources.

A minimal shape that works:

* One gateway endpoint (/chat, /tools, /embeddings)
* Policy layer: authentication/authorization, PII rules, model allowlists, budget enforcement
* Router: chooses region/provider/model based on tier and live capacity
* Evals/guardrails: fast checks inline, deeper checks async
* Audit log: prompt/response hashes plus metadata (not necessarily full content)

This is also where orchestration tools can help: represent flows explicitly, add timeouts and retries, and capture structured traces for debugging and compliance.

A control plane doesn’t magically solve capacity, but it does reduce the incident tax, prevent uncontrolled spend, and let you offer differentiated tiers (premium interactive vs. delayed batch) instead of a single brittle experience.

> Control planes turn scarcity from chaos into policy.

---

### Path 3: Orchestrate scarcity like a first-class constraint

If Path 2 is about building more supply, Path 3 is about behaving like a grown-up consumer of supply.

The key shift is to treat compute and power constraints as normal operating conditions, not edge cases. Scarcity isn’t an incident. It’s a state. Your architecture either acknowledges that-or it lies until it fails.

**What this looks like on the ground:**

* Token budgets as an enforced resource (per app, per user, per workflow)
* Priority queues (interactive > batch > experimentation)
* Caching everywhere (semantic and exact-match) to reduce watts per answer
* Fallback models and “partial results” UX to avoid hard failures
* Async-first agents for non-urgent work (so curtailment becomes delay, not outage)

**This isn’t just reliability-it’s business design. It gives you levers to:**

* Preserve revenue and customer trust under constrained capacity
* Avoid runaway costs during demand spikes
* Create explicit service tiers instead of implicit favoritism (“the loudest team gets GPUs”)
* Make ethical commitments real (for example, lower-energy defaults where quality is sufficient)

This seems trivial, but the discipline is the point: scarcity has to be encoded in the platform, not “handled by hero engineers during incidents.”

> AI, the best reliability feature is a graceful “not now” instead of a catastrophic “never.”

---

### One “science fiction that might age into science”

The most plausible sci-fi isn’t sentient models. It’s a different map of where computation happens.

As power becomes the bottleneck, we should expect more organizations to experiment with:

* Locating batch inference/training near abundant generation (for example, renewables, hydro, industrial co-generation)
* Treating latency-sensitive inference as the premium product and moving everything else to the compute hinterlands
* Shifting from “follow the user” to “follow the power,” then using networks, caching, and product design to hide the seams

The point isn’t to predict a single outcome. It’s to internalize the direction: energy topology becomes architecture. That’s a new kind of systems thinking for most enterprises-and it raises new ethical questions about who bears the costs of AI growth.

If the industry “follows the power,” communities and regulators will demand clearer accounting of environmental impacts, local grid stress, and who benefits. This will land on executive desks, not engineering backlogs.

> We used to ship software to servers. Now we may ship workloads to watts.

---

### Closing thought

The recent debate has been “**GPUs vs. ASICs.**”

The emerging reality is that silicon is table stakes-and power delivery is the new gating dependency.

If you’re building enterprise AI, the winners won’t just have better models. They’ll have:

* A control plane that can route around scarcity
* Observability that correlates capacity events with application symptoms
* Evals and guardrails that degrade gracefully instead of failing catastrophically
* Governance that treats energy-shaped availability as a real risk category

Because in the next wave, the final boss isn’t the chip.

It’s the grid.