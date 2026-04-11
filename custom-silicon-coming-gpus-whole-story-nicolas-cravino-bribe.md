![](https://media.licdn.com/mediaD4E12AQHjx21MxTq-Pw)

# [Custom Silicon Is Coming for GPUs - But Is That the Whole Story?](https://www.linkedin.com/pulse/custom-silicon-coming-gpus-whole-story-nicolas-cravino-bribe)

Created on 2026-01-28 21:43

Published on 2026-01-28 22:57

Back in July 2024, I asked: "[*Will ASICs Dethrone GPUs for LLM Inference*](https://www.linkedin.com/pulse/asics-dethrone-gpus-llm-inference-nicolas-cravino-bfsue)?"                           At the time, it was a speculative question. The challenges seemed daunting - memory requirements, model diversity, the rapid evolution of transformer architectures. I then followed up back in December 2025 with '[ASICs vs. CPUs was never the final boss. The Grid is.](https://www.linkedin.com/pulse/asics-vs-gpus-never-final-boss-grid-nicolas-cravino-7s2ye)

Now in the last week of January 2026, the ASICs vs GPU answer is becoming clear. And it's more nuanced than "yes" or "no."

###

---

### 1- The hyperscalers moved first:

 I've been mapping the "AI ingredient matrix" across major players. The Custom Silicon column tells a story:

* **Google** → TPU (deployed 2015, now 7th gen - Ironwood)
* **AWS** → Trainium + Inferentia
* **Microsoft** → Maia 100
* **Meta** → MTIA
* **Apple** → Neural Engine

They built. They deployed. They're reaping the cost advantages.

### 2- But here's what changed in the last 90 days:

**OpenAI** just made three moves that signal the shift is accelerating:

 1. **Cerebras** deal ($10B) — 750 megawatts of wafer-scale AI chips through 2028. Target: inference speeds 15-20x faster than current GPU systems. This isn't incremental. This is a bet that custom silicon is the future.

2. **AMD** partnership — Warrants for ~10% of AMD stock in exchange for large-scale MI450 GPU deployments starting late 2026. Diversifying away from NVIDIA while keeping GPU optionality.

3. **Samsung** & **SK Hynix** 'Stargate' deal — 900,000 wafers/month of HBM and DRAM (combined). Securing the memory supply chain that feeds everything.

4. **OpenAI** isn't building silicon in-house like Google. They're ***assembling a custom silicon stack through partnerships***. Different strategy, same destination (like a colleague always tells me, it's the *GPS theory*, different paths, same destination).

Meanwhile: **xAI** is running *100,000 H100s with zero custom silicon path announced*. **Anthropic** remains compute-dependent on AWS and Google.

I’ve been mapping the ‘AI ingredient matrix’ across major players. The Custom Silicon column tells a story:

![](https://media.licdn.com/dms/image/v2/D4E12AQED0J-ez9e6mQ/article-inline_image-shrink_1500_2232/B4EZwGysL5H8AY-/0/1769640478272?e=1776297600&v=beta&t=0HH2mU0Ee9S0225KjSZpreTvBYAyg8grWUup4wXP1j0)

### 3- The case for custom silicon is now empirical:

 ✅ Cost at scale — Google and AWS price inference aggressively because they own the silicon margin.

 ✅ Vertical control — Optimization from model to metal, no middleman

 ✅ Supply chain diversification — The NVIDIA → TSMC → Taiwan concentration is a real risk

 ✅ Inference economics — For predictable production workloads, purpose-built wins on perf/watt

 ✅ The memory wall — Cerebras' wafer-scale approach directly attacks the bottleneck that limits traditional architectures

### 4- But here's what keeps this from being a closed case:

### ⚠️ Algorithmic disruption is the wild card.

 We saw this in the past with Crypto-mining HW: Every **ASIC** is a frozen bet on a specific architecture. TPUs are optimized for matrix multiplications and attention mechanisms. Cerebras' wafer-scale chips assume certain memory access patterns.

**What happens when someone discovers a fundamentally different and disruptive approach?** (note the 'when' and not an 'if')

* Mixture-of-experts changed inference economics
* State-space models (Mamba) challenged attention orthodoxy

What's next? We don't know—and that's the point !

> GPUs remain the hedge. When the next architectural breakthrough lands, GPUs can adapt within a driver update. ASICs require a new tape-out.

This is exactly why OpenAI's deals matter. They're betting on custom silicon and keeping GPU optionality. Belt and suspenders. *Smart*.

---

### My read:

The hyperscalers who started building custom silicon a decade ago are now in harvest mode.

The pure-play AI labs have two paths:

1. **Build** (expensive, slow, requires hardware DNA); or
2. **Partner** (OpenAI's approach—assemble the stack through deals)

**The ones with no silicon strategy at all? Are they're hoping the GPU era lasts forever ?. That's not a strategy—that's a prayer.**

Custom silicon is winning the current game. But AI is still in its Cambrian explosion. The smart money is on custom silicon for production scale, GPUs for research and optionality, and enough diversification to survive the next disruptive architectural surprise.

**What's your take—is the custom silicon transition inevitable, or will the next algorithm shift reset the board?**

**Note**: I have not analyzed US adversaries. Some adversaries are coming up with awesome models, they have solid Power Grids, but we believe they are still behind on Silicon tech. It's possible that they are ahead of us maybe on algorithmic improvement, we did see interesting cases with DeepSeek and now even this week with Kimi K2.5.

---

### APPENDIX: Reference Links

### OpenAI Cerebras Deal

* OpenAI Official: <https://openai.com/index/cerebras-partnership/>
* TechCrunch: <https://techcrunch.com/2026/01/14/openai-signs-deal-reportedly-worth-10-billion-for-compute-from-cerebras/>
* CNBC: <https://www.cnbc.com/2026/01/14/cerebras-scores-openai-deal-worth-over-10-billion.html>
* Reuters/Yahoo Finance: <https://finance.yahoo.com/news/openai-buy-compute-capacity-startup-200619645.html>
* Bloomberg: <https://www.bloomberg.com/news/articles/2026-01-14/openai-forges-10-billion-deal-with-cerebras-for-ai-computing>

### OpenAI AMD Partnership

* OpenAI Official: <https://openai.com/index/openai-amd-strategic-partnership/>
* Tom's Hardware: <https://www.tomshardware.com/tech-industry/openai-and-amd-announce-multibillion-dollar-partnership-amd-to-supply-6-gigawatts-in-chips-openai-could-get-up-to-10-percent-of-amd-shares-in-return>
* Dr. Ian Cutress Analysis: <https://morethanmoore.substack.com/p/amd-and-openai-the-6-gigawatt-bet>
* Futurum Analysis: <https://futurumgroup.com/insights/amd-openai-partnership-scale-win-or-execution-risk-at-6-gw/>

### OpenAI Samsung/SK Hynix Deal (Stargate)

* OpenAI Official: <https://openai.com/index/samsung-and-sk-join-stargate/>
* TechCrunch: <https://techcrunch.com/2025/10/01/openai-ropes-in-samsung-sk-hynix-to-source-memory-chips-for-stargate/>
* Tom's Hardware: <https://www.tomshardware.com/pc-components/dram/openais-stargate-project-to-consume-up-to-40-percent-of-global-dram-output-inks-deal-with-samsung-and-sk-hynix-to-the-tune-of-up-to-900-000-wafers-per-month>
* TrendForce: <https://www.trendforce.com/news/2025/10/02/news-openais-stargate-900k-dram-wafers-could-hit-40-of-global-output-led-by-samsung-sk-hynix/>

### Google TPU

* Google Cloud Blog (Trillium/v6): <https://cloud.google.com/blog/products/compute/introducing-trillium-6th-gen-tpus>
* Google Blog (Ironwood/v7): <https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/ironwood-google-tpu-things-to-know/>
* Google Cloud TPU Page: <https://cloud.google.com/tpu>
* Wikipedia: <https://en.wikipedia.org/wiki/Tensor_Processing_Unit>

### Microsoft Maia

* Microsoft Tech Community: <https://techcommunity.microsoft.com/blog/azureinfrastructureblog/inside-maia-100-revolutionizing-ai-workloads-with-microsofts-custom-ai-accelerat/4229118>
* Azure Blog: <https://azure.microsoft.com/en-us/blog/azure-maia-for-the-era-of-ai-from-silicon-to-software-to-systems/>
* CNBC (Maia 200): <https://www.cnbc.com/2026/01/26/microsoft-reveals-maia-200-ai-chip-will-use-it-in-house.html>

### Meta MTIA

* Meta Engineering: <https://engineering.fb.com/2025/09/29/data-infrastructure/metas-infrastructure-evolution-and-the-advent-of-ai/>
* Meta Official (2024): <https://about.fb.com/news/2024/04/introducing-our-next-generation-infrastructure-for-ai/>
* TechCrunch: <https://techcrunch.com/2024/04/10/meta-unveils-its-newest-custom-ai-chip/>
* ACM Paper (ISCA 2025): <https://dl.acm.org/doi/10.1145/3695053.3731409>

### Apple Neural Engine

* Apple ML Research: <https://machinelearning.apple.com/research/neural-engine-transformers>
* Wikipedia: <https://en.wikipedia.org/wiki/Neural_Engine>

### xAI Colossus

* Wikipedia: [https://en.wikipedia.org/wiki/Colossus\_(supercomputer)](https://en.wikipedia.org/wiki/Colossus_%28supercomputer%29)
* ServeTheHome: <https://www.servethehome.com/inside-100000-nvidia-gpu-xai-colossus-cluster-supermicro-helped-build-for-elon-musk/>
* Data Center Dynamics: <https://www.datacenterdynamics.com/en/news/xais-memphis-supercluster-has-gone-live-with-up-to-100000-nvidia-h100-gpus/>

### Cerebras Performance Claims

* Cerebras Blog: <https://www.cerebras.ai/blog/cerebras-cs-3-vs-nvidia-dgx-b200-blackwell>
* Cerebras Inference Launch: <https://www.cerebras.ai/blog/introducing-cerebras-inference-ai-at-instant-speed>
* VentureBeat: <https://venturebeat.com/ai/how-cerebras-is-breaking-the-gpu-bottleneck-on-ai-inference>

### Chinese AI Models (DeepSeek, Kimi)

* Kimi K2.5 (Moonshot AI): <https://huggingface.co/moonshotai/Kimi-K2.5>
* SiliconANGLE: <https://siliconangle.com/2026/01/27/moonshot-ai-releases-open-source-kimi-k2-5-model-1t-parameters/>

### Original Transformer Paper

* "Attention Is All You Need" by Vaswani et al. (2017): <https://arxiv.org/abs/1706.03762>