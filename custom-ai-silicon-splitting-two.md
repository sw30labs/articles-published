# [Custom AI Silicon Is Splitting in Two](https://www.linkedin.com/pulse/custom-ai-silicon-splitting-two-nicolas-cravino-5hrpc)

Published on 2026-08-28 12:00

OpenAI's Jalapeño freezes the physics of inference. Taalas HC1 freezes the model itself. The useful question is what you are willing to give up.

On August 25, 2026, two AI silicon announcements landed on the same day. OpenAI published the first measured results for Jalapeño, its first custom inference processor. Apple introduced M6, with neural acceleration in both its Neural Engine and GPU. Earlier that month, AMD announced an agreement to acquire Taalas, whose HC1 technology demonstrator makes one base model part of the physical implementation.

Three announcements. Three different bets. Not one ASIC to rule them.

> What are you willing to freeze in exchange for efficiency?

A custom chip is both an efficiency purchase and an option sale. The more flexibility a buyer gives up, the more certain it must be about workload, volume, model life, and exit. GPUs can lose an individual benchmark and still retain value because customers are paying for the option to change their minds.

In July 2024 I asked whether ASICs would dethrone GPUs for LLM inference. Specialization is gaining ground. “Dethrone” was too binary. Two later constraints still hold: every chip eventually meets the grid, and GPUs remain the broadest adaptability buffer against the next algorithmic surprise.

---

## Stop asking “GPU or ASIC?” Ask what gets frozen

What fabrication freezes. The fork is L4 vs L5. Cloud versus edge is a different axis.

Every computer freezes assumptions in hardware. The useful distinction is how far those assumptions reach into the AI stack. CPU, GPU, and NPU describe processor roles; “custom inference ASIC” describes how specific the implementation is. An NPU may itself be custom ASIC IP inside a SoC.

Most enterprises buy instances, endpoints, appliances, or contracts — not masks and wafers. Their decision is how much vendor-specific infrastructure, software, and lifecycle risk to accept.

This is a gradient before it becomes a bifurcation. The fork appears when the model's identity and base weights stop being ordinary replaceable software. Jalapeño remains on the programmable side of that line. Taalas's HC1 crosses it.

A production design needs a freeze contract for every layer it makes less flexible: the expected gain, expiration trigger, fallback path, replacement path, and owner.

---

## Two bets

Two bets on custom silicon. NPUs sit on the programmable side. GPUs remain the hedge.

### Branch one: specialize around the physics of inference

OpenAI and Broadcom announced a large custom-accelerator partnership in October 2025 and unveiled Jalapeño by name in June 2026. The August 25 disclosure was more useful than another roadmap: measurements from working silicon.

Jalapeño is an inference processor, not a training accelerator. OpenAI designed its architecture; Broadcom implemented the silicon and networking. OpenAI showed it running GPT-OSS 120B, DeepSeek R1 670B, and Kimi K2.5 1T. That diversity is the point. Weights remain in high-bandwidth memory. Each model family still needs kernels and serving optimization.

Frozen: recurring features of LLM inference — low-precision tensor execution, movement of weights and activations, KV-cache locality, synchronization, scale-out networking. Still changeable: model weights, supported kernels, serving policies.

OpenAI reported better throughput per kilowatt and lower end-to-end latency than selected Nvidia Blackwell configurations on three named InferenceX workloads. Treat that as a vendor result, not a universal Nvidia comparison: Jalapeño used HBM4 while the compared Blackwell systems used HBM3E, and SemiAnalysis participated in selected lab benchmarking with OpenAI rather than evaluating a production deployment. Deployment scale and production economics remain open.

Google's Ironwood, Microsoft's Maia 200, and AWS's Inferentia/ Trainium families are the same branch in other wrappers. The product is the accelerator plus memory, fabric, compiler, kernels, runtime, cooling, scheduler, and control plane.

### Branch two: specialize around the identity of a model

Taalas's ChatJimmy demonstration runs Llama 3.1 8B on HC1. According to Taalas executives interviewed by The Next Platform, a mask-ROM recall fabric embodies the fixed base model and weights, while SRAM holds mutable runtime state (KV cache, supported adapters). The design is fully digital. “Etched weights” is shorthand, not analog compute-in-memory.

Frozen: base-model structure, weights, deeply tailored dataflow. Still changeable: prompts, runtime state, surrounding software, supported adapters. Changing the base means producing different silicon.

Taalas reports roughly 17,000 tokens per second per user for the HC1 demonstration. Company-attributed; not an independently controlled TCO comparison. Customization confined to two metal layers, weights to PCIe cards in roughly two months— also company claims. Even if that cadence holds, it does not abolish fabrication, packaging, yield, inventory, integration, or retirement. An adapter is a tuning path, not a universal rollback.

AMD's August 6 agreement to acquire Taalas makes the category more strategically consequential. It does not prove production economics. Subject to closing, AMD might integrate the team, fold IP into Instinct, or keep model-bound compute as an option. A stronger platform can also mean one fewer exit.

The escape hatch changes by branch. A programmable inference ASIC can route an unsupported model to a provisioned GPU pool. Model-bound silicon needs a parallel programmable pool, a prequalified replacement module, or both.

---

## When hardware inherits the model's expiration date

I use model half-life as a decision heuristic, not a statistical constant: the expected period over which demand, accepted-result quality, licensing, trust, security, policy, compatibility, and operating cost keep model-bound silicon economically utilized. A model can still run while becoming economically obsolete.

- Model-bound silicon is the technical category.
- Seasonal silicon is a deliberate lifecycle strategy: bounded, replaceable generations on a planned cadence. My term, not a JEDEC category. It only works when refresh is slower than payback and every retired module has a reuse, resale, or secure-destruction plan.
- Stranded silicon is the failure mode: relevance ends before cost recovery.

Before comparing accelerators, define an accepted result: an output that clears quality, policy, format, and latency. Measure cost, energy, and throughput per accepted result at representative concurrency — not per token in isolation. Fast rejected output is not efficiency.

> Fabrication and deployment lead time + payback period < expected model economic life.

Treat economic life as the shortest of its quality, license, security, demand, policy, compatibility, and cost horizons. Recalculate when one changes. Product owns the acceptance threshold; security owns trust and recall; finance owns payback; operations owns replacement capacity.

My hypothesis: smaller fixed models find their best economics in constrained workloads (classification, routing, extraction, translation, control) with stable acceptance tests, adapter headroom, sustained volume, and a replacement plan. That is more plausible than hardwiring whichever frontier model leads this quarter.

No-go: unstable acceptance tests, uncertain volume, frequent architecture change, large fallback rates, or no funded replacement path. Under those conditions, programmability is insurance.

---

## NPUs are the same programmable branch, at the endpoint

Apple's M6, AMD Ryzen AI Max, and Arm Ethos-U85 do not share one instruction set. “NPU” is a market label. Peak TOPS without operator coverage, memory bandwidth, and fallback frequency is a sticker.

If a graph repeatedly falls back from NPU to CPU or GPU, theoretical efficiency vanishes at the boundaries. Local inference can cut latency and keep selected data on-device — but only if the application, update, telemetry, and supply chain actually preserve those properties.

That is not dethroning. It is a redistribution of work.

---

## Portability is an exit strategy

Hardware fragmentation creates a desire for one abstraction. Vulkan is a low-level cross-vendor GPU API, not an umbrella over CUDA and ROCm. IREE can import models and generate code for multiple targets; backend completeness varies.

Buyers want common graphs, observable fallbacks, and credible exits. Chip and cloud vendors benefit when compilers, kernels, and contracts make hardware sticky. Nvidia's strongest counterargument is not a faster GPU. It is pooled utilization, mature software, and the option to absorb the next unplanned workload.

Code portability is not performance portability. At the model-specific end, a common graph cannot retarget weights already embodied in fabricated silicon.

> Portability is not a compiler checkbox. It is an exit strategy — and an exit strategy is credible only if someone tests it.

---

## When a model patch requires a truck roll

I confronted model half-life while designing AEGIS — Agentic Execution for Governed Infrastructure Security — an unpublished proposal for an air-gapped agentic pentesting appliance with a hardwired inference module. A design exercise, not a deployed case study.

The temptation is to treat the fast fixed model as the product. That makes the appliance age at the speed of one base. The proposal separates four clocks: skills and prompts (days to weeks), sandboxed tools (weeks to months), adapters (months, without replacing the base), and a field-replaceable inference module (annually, or when the base itself must change).

In an air-gapped product those cadences need signed offline bundles, hardware-in-the-loop evaluation, staged activation, a rollback image, and fallback capacity during replacement. Provenance binds base weights, quantization, evaluation, mask revision, chip lot, adapter, firmware, and retirement status as one chain of custody. A security-triggered model withdrawal becomes a fleet-wide hardware event.

When intelligence becomes physical, serviceability and provenance must become product features. AI governance becomes asset management.

---

## The bifurcation could still disappoint

1. Vertical integration may stay a hyperscaler game. Most enterprises consume custom silicon through cloud pricing rather than own it.
2. Inference may remain too dynamic. Agentic workloads, multimodality, MoE, long context, and shifting quantization can reward programmable hardware faster than ASIC roadmaps adapt.
3. Taalas may prove a product, not a category. A striking demonstrator does not establish fleet-scale yield or independently validated TCO.
4. NPUs can stall in software. Weak operator coverage leaves advertised TOPS unused.

These are not arguments against specialization. They define its market boundary: uncertainty must be low enough to monetize.

---

## Five questions before you buy

The hardware decision is no longer “buy GPUs or wait for ASICs.”

1. Which workload — and what realistic volume — will remain stable enough to specialize?
2. What is frozen, and which change in model, quality, license, vulnerability, or demand triggers replacement?
3. What is the fully loaded cost per accepted result at realistic utilization, including software, power, validation, deployment, and retirement?
4. What falls back, what is the performance tax, and what tested path exists to another engine or supplier?
5. Who owns provenance, patching, recall, physical replacement, stranded inventory, and end-of-life handling?

The answers should produce four artifacts before commitment: a workload acceptance benchmark, a supported-operator and fallback map, a lifecycle and recall runbook, and a full-cost payback model. Without all four, the organization is buying a benchmark rather than an operating capability — and selling an option it has not priced.

The throne fragmented. GPUs remain the hedge. The durable winner will not be a single chip. It will be the architecture that freezes exactly enough, and can survive what changes next.

("Views my own.")
