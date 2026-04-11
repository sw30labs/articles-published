![We didn’t run out of compute. We ran out of control](https://media.licdn.com/mediaD4E12AQGTPudbmiYdcQ "We didn’t run out of compute. We ran out of control")

# [The AI Supply Chain Is the Real Enterprise Bottleneck](https://www.linkedin.com/pulse/ai-supply-chain-real-enterprise-bottleneck-nicolas-cravino-bpm5e)

Created on 2026-01-11 13:41

Published on 2026-01-11 14:56

---

### Executive Summary

***Enterprise AI is no longer limited by Compute capacity. It's limited by trust at scale.***

* **Modern AI is assembled, not built.** Each model, prompt, connector, dataset, and policy is a dependency-and dependencies multiply risk faster than most governance processes can handle.
* **The winning capability is governance velocity:** the ability to *approve, monitor, and roll back* AI changes at the same cadence as your AI stack evolves.
* **The fix is governance-as-code.** Treat AI artifacts like software artifacts: version them, sign them, test them, monitor them, and enforce policy automatically in CI/CD.

*If you do one thing after reading:* ***map your AI dependency graph****. If you can't name your dependencies, you can't secure them.*

![](https://media.licdn.com/dms/image/v2/D4E12AQGvMg5r_M3-9Q/article-inline_image-shrink_1500_2232/B4EZutg.R1LsAU-/0/1768142667405?e=1776297600&v=beta&t=1OXW0ccHuFvZ0zU6-Jexo-pG0g6VmM4nF1p_d72Pchg)

---

### 1) The Bottleneck Has Moved From Compute Scarcity to Control Scarcity

A few years ago, "AI strategy" was mostly a capacity conversation: GPUs, training runs, latency budgets.

That conversation isn't dead-but it's no longer the limiting factor for most enterprises. The limiting factor is **control**:

* Can you prove what model version made a decision?
* Can you explain why an agent took an action?
* Can you stop a bad update *before* it reaches production?
* Can you roll back safely when something drifts?

If you're a regulated business, the question isn't *"Can we run it?"* It's *"Can we defend it?"*-to customers, auditors, and regulators.

> Here's the key shift: ***Compute scales linearly. Trust requirements scale non-linearly.***

Every new tool, connector, dataset, or prompt adds edges to your dependency graph-not just nodes.

The risk isn't "the model" in isolation. The risk is the **system of systems**-and the fact that it changes constantly.

---

### 2) Why Linear Governance Fails at Machine Speed ?

Most enterprise governance is built for linear change:

* annual risk assessments
* quarterly model reviews
* spreadsheets of "approved vendors"
* manual sign-offs

But modern AI change is not linear. It's modular and combinatorial.

1. **One prompt tweak** can change tool selection,
2. **One tool schema change** can create a new injection surface.
3. **One RAG corpus refresh** can introduce a policy violation.
4. Even if each individual component looks "safe," t**he *interaction* can be unsafe**.

If you want a practical way to explain this to a board:

1. **Your AI supply chain looks less like a single system and more like a dependency graph.**
2. And graphs don't fail politely.
3. This is also why *"we did a model validation once"* is quickly becoming the new *"we ran a pen test once."*

---

### 3) Three Real-World Signals You Can't Ignore

**Signal #1: You're Responsible for What Your AI Says and Does**

In *Moffatt v. Air Canada*, a tribunal held Air Canada responsible for misinformation provided by its chatbot on the company website. The detail that matters isn't the refund amount; it's the precedent: **"the bot" is not a separate entity.** The company owns the outcome. [1]

If your enterprise deploys AI agents that draft customer comms, approve refunds, or trigger operational actions, assume the same principle applies: **the system's output is your output.**

**Signal #2: Regulators Care About Records, Not Intentions**

The SEC has repeatedly charged firms for recordkeeping failures. In 2022, the SEC announced penalties totaling more than **$1.1B** for widespread recordkeeping failures across 16 firms. [2] In 2024, the SEC announced another **$392.75M** in combined civil penalties across 26 firms for similar issues. [3]

This is the compliance version of observability: if you can't reconstruct what happened, you can't credibly claim control.

Now apply that to AI:

1. prompts change,
2. tool schemas change,
3. model providers update,
4. retrieval indexes refresh,
5. policies get edited in a repo.

If you can't produce an auditable trail of *what changed, when, and why*, you're building ***governance debt*** you'll eventually have to pay-with interest.

**Signal #3: LLM Security Standards Now Explicitly Call Out Supply Chain Risk**

OWASP's Top 10 for LLM Applications explicitly includes **Supply Chain Vulnerabilities** as a core risk category. [4] That should tell you something: this problem isn't niche, and it's not going away.

---

**4) Who This Hits First and What Each Leader Should Do Next**

When the AI supply chain breaks, it rarely breaks "neatly." It breaks across functions.

![](https://media.licdn.com/dms/image/v2/D4E12AQGirZ7x4jR92Q/article-inline_image-shrink_1500_2232/B4EZutgKEKHsAU-/0/1768142448045?e=1776297600&v=beta&t=t1576GdtGS_zUVfc5HSAV7eouPhR8MMuyi0ksoUKOzM)

This is also why "AI governance" ***can't live as a quarterly committee meeting***. It has to be executable.

---

**5) The Four Controls That Make Governance Move at Machine Speed**

I'll keep this practical. If you want governance velocity, you need four capabilities-implemented as controls, not slogans.

**5.1 Assurance With Risk-Tiered Gates**

Not every AI action deserves the same scrutiny.

Define risk tiers based on impact, reversibility, and regulatory exposure. Example:

* **Tier 0 (Low):** internal summarization, drafting, search
* **Tier 1 (Medium):** customer-visible content, recommendations
* **Tier 2 (High):** decisions affecting eligibility, pricing, credit, medical, legal
* **Tier 3 (Critical):** money movement, identity changes, safety-critical operations

Then enforce tier-appropriate controls automatically. High-risk agents shouldn't ship because someone clicked approve in a spreadsheet.

**5.2 Provenance as Your AI's Digital Alibi**

You need to be able to answer, fast:

* Which **model** version ran?
* Which **prompt** template was used?
* Which **tool schema** did the agent see?
* Which **dataset/version** fed retrieval?
* Which **policy package** allowed the action?

This is the AI version of a production post-mortem. Without provenance, incident response becomes guesswork.

**5.3 Supply Chain Integrity for AI Artifacts**

For software, we've learned (the hard way) to care about supply chain integrity: signed builds, attestations, SBOMs, hardened pipelines.

AI needs the same mindset-expanded to include:

1. prompt templates,
2. retrieval indexes,
3. tool schemas,
4. evaluation bundles,
5. policy rules.

If an attacker can't poison your model weights but can modify your tool schema or prompt routing, you still lose.

**5.4 Observability and Rollback**

AI systems fail in slow motion (drift) and fast motion (prompt injection / tool misuse). You need both:

* **continuous monitoring** (behavior, cost, safety signals)
* **fast rollback** (last-known-good model/prompt/policy package)

This is where traditional "annual model validation" collapses. You can't govern at the speed of quarterly reviews when your stack changes weekly-or daily.

---

**6) Governance-as-Code in Practice**

Here's the practical translation: controls, owners, cadence, and the evidence they produce.

![](https://media.licdn.com/dms/image/v2/D4E12AQFDQyxpZ6I6xg/article-inline_image-shrink_1500_2232/B4EZutcJa3MIAU-/0/1768141397603?e=1776297600&v=beta&t=r_QIeEbnVmDcYcEdMMzrFBYSH4jckG_06iN97na0W9Y)

Notice what's missing: "a committee approves AI." Committees don't scale. Pipelines do.

**Visual: A Dependency Graph You Can Actually Operate**

![](https://media.licdn.com/dms/image/v2/D4E12AQGnUuiSDQJbwg/article-inline_image-shrink_1500_2232/B4EZutijAtIkAU-/0/1768143074079?e=1776297600&v=beta&t=eXvPEgRuQwBv2mNVLYXwoTGAVdEPnJQXeHe87jwARpo)

This is what "defensible AI" looks like: you can point to each dependency, its owner, its version, and the controls around it.

---

**7) What This Looks Like in CI/CD**

![](https://media.licdn.com/dms/image/v2/D4E12AQGXTXMoBx74-g/article-inline_image-shrink_1500_2232/B4EZuti0gULUAY-/0/1768143148258?e=1776297600&v=beta&t=EoNJ1UZY0y4eBcTCtXudbwxnRsiV-YxmHAQpG9tL9x0)

If you want a concrete starting point, make "AI deploy" mean:

1. **Everything is in the inventory** (including prompts, tools, and datasets).
2. **Artifacts are signed** (builds, prompt packs, policies).
3. **Provenance exists** (who built it, from what, with what pipeline).
4. **Policy checks pass** (risk tier rules, allowed tools, data scopes).
5. **Eval suite passes** (quality + safety + bias thresholds by tier).
6. **Tool permissions are bounded** (least privilege; no silent escalation).
7. **Runtime guardrails are configured** (rate limits, sandboxing, safe completion).
8. **Rollback is ready** (a pinned last-known-good and a tested kill switch).

That's governance-as-code in one page.

---

**8) The KPIs That Prove You're Building Trust**

Most organizations track AI adoption metrics: number of pilots, tokens consumed, features shipped.

Those are not governance metrics.

If you want to know whether you can scale safely, track:

* **Assurance Velocity:** time from detecting a risky change -> blocking it in production
* **Rollback Time:** time to revert to last-known-good after a policy or eval failure
* **Coverage:** % of AI artifacts under inventory + signing + policy gates
* **Eval Pass Rate by Tier:** how often Tier-2/3 deployments pass without waivers
* **Tool Abuse Containment:** % of anomalous tool calls auto-blocked / quarantined
* **Audit Readiness:** time to produce an evidence packet for a given model/agent

These are the operational metrics of trust.

---

**9) Standards and Frameworks You Can Borrow**

You don't need to invent governance from scratch. You need to adapt proven ideas:

1. **NIST AI RMF 1.0** gives a practical risk framing across *Govern, Map, Measure, Manage*. [6]
2. **GDPR Article 30** is a reminder that regulators expect **records of processing**. [7]
3. **SEC recordkeeping rules** (e.g., Rule 17a-4) show the enforcement reality: inability to produce records becomes a violation in itself. [8]
4. **EU AI Act** formalizes risk-based obligations for certain AI systems-expect more "evidence requirements," not fewer. [9]
5. **SLSA** provides a supply chain maturity model you can borrow for AI artifact pipelines. [10]
6. **Sigstore** and **in-toto** show how signing and attestations can scale without turning key management into a nightmare. [11][12]
7. **SBOM guidance** from CISA/NIST is the closest software analogue to the "AI-SBOM" idea. [13][14]

Use these as scaffolding. Your governance should be opinionated-but not invented in isolation.

[New] Emerging and promissing governance Tools OSCAL. I've already published an article regarding the OSCAL innitiative, I strongly suggest you take a look at least at the OSCAL Webpage.

[![](https://media.licdn.com/dms/image/v2/D4E12AQE_0lxWrlwSjQ/article-inline_image-shrink_1500_2232/B4EZuthjlfMEAU-/0/1768142816414?e=1776297600&v=beta&t=Wuk8AnTmYRmKLH2rPjLH2bs81rQh30z17Q2v-adPfMU)](https://pages.nist.gov/OSCAL/)

---

**10) A Practical 30/60/90-Day Rollout Without Freezing Innovation**

If you're starting from "pilot chaos," here's a realistic sequence:

**Days 0-30: Make the supply chain visible**

* Create the AI inventory (models, prompts, tools, RAG, policies).
* Assign owners. "No owner" = "no production."
* Pick one critical use case and draw its dependency graph.

**Days 31-60: Make the supply chain defensible**

* Add signing + provenance for deployable artifacts.
* Implement policy-as-code gates in CI/CD.
* Define minimum eval suites by risk tier and enforce them as deploy gates.

**Days 61-90: Make the supply chain resilient**

* Add real-time monitoring for drift and tool misuse.
* Formalize rollback and practice it.
* Start reporting governance KPIs (assurance velocity, coverage, audit readiness).

At the end of 90 days, you don't have "perfect governance." You have **repeatable, automatable control**-and a foundation you can scale.

---

**11) The Strategic Implication Most Leaders Miss**

Modular AI architectures don't just change your tech stack.

They change your operating model.

* **Vendor management becomes runtime management.** When model providers update, your system changes.
* **"Procurement" becomes an engineering concern.** Buying a model or tool is not a contract; it's a dependency.
* **Risk shifts left.** If your controls only exist at the end (audit), they will always be late.
* **Your dependency graph becomes a boardroom artifact.** It's the map of what the business *actually* relies on.

This is why governance is becoming **a competitive moat**. Organizations that can integrate **quickly** *and* prove control will move **faster** than those who treat governance as paperwork.

---

**## Closing: Start With the Dependency Graph**

If you've read this far, you already know the core truth:

> **You don't have an "AI model" problem. You have an AI supply chain problem.**

The good news is that this is solvable without freezing innovation.

A pragmatic first step:

1. **Map your AI dependency graph** for one high-value use case.
2. **Build** an **AI asset inventory** with owners and versions.
3. **Add** **signed artifacts + eval gates + policy gates** in CI/CD.
4. **Instrument** runtime behavior and **practice rollback**.

Do that once, then scale it.

If you want, I'm happy to share a lightweight "AI-SBOM" template and a starter set of policy/eval gates you can adapt to your environment.

---

**### About the Author**

Nicolas Cravino works at the intersection of enterprise architecture, security, and AI delivery. He helps teams move from AI prototypes to production systems that are measurable, auditable, and resilient.

---

**### References**

[1] [American Bar Association - "BC Tribunal Confirms Companies Remain Liable for Information Provided by AI Chatbot" (Feb 29, 2024)](https://www.americanbar.org/groups/business_law/resources/business-law-today/2024-february/bc-tribunal-confirms-companies-remain-liable-information-provided-ai-chatbot/)

[2] [U.S. SEC Press Release 2022-174 - "SEC Charges 16 Wall Street Firms with Widespread Recordkeeping Failures" (Sept 27, 2022)](https://www.sec.gov/newsroom/press-releases/2022-174)

[3] [U.S. SEC Press Release 2024-98 - "Twenty-Six Firms to Pay More Than $390 Million Combined to Settle SEC's Charges for Widespread Recordkeeping Failures" (Aug 14, 2024)](https://www.sec.gov/newsroom/press-releases/2024-98)

[4] [OWASP - Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

[5] [IBM - Cost of a Data Breach Report 2024 highlights](https://www.ibm.com/think/insights/cost-of-a-data-breach-2024-financial-industry)

[6] [NIST - AI Risk Management Framework 1.0](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)

[7] [EU GDPR - Regulation (EU) 2016/679, Article 30](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)

[8] [SEC - 17 CFR § 240.17a-4, Records to be preserved by certain exchange members, brokers and dealers](https://www.law.cornell.edu/cfr/text/17/240.17a-4)

[9] [EU AI Act - Regulation (EU) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng)

[10] [SLSA - Supply-chain Levels for Software Artifacts](https://slsa.dev/)

[11] [Sigstore - Overview and documentation](https://docs.sigstore.dev/about/overview/)

[12] [in-toto - CNCF project overview](https://www.cncf.io/projects/in-toto/)

[13] [CISA - Software Bill of Materials resources](https://www.cisa.gov/sbom)

[14] [NIST - SBOM and software supply chain guidance under EO 14028](https://www.nist.gov/itl/executive-order-14028-improving-nations-cybersecurity/software-security-supply-chains-software-1)

---

***## Glossary In 30 Seconds***

* **AI supply chain:** the full set of components that make an AI capability work in production: **\*\*models + prompts + tools/connectors + data/RAG + orchestration + runtime controls + monitoring\*\***.
* **RAG (retrieval-augmented generation):** letting a model answer using *your* documents via a search/index step (instead of "pure" model memory/training data).
* **Policy-as-code:** expressing governance rules in machine-readable form (so they can be enforced automatically in pipelines).
* **Provenance:** "where did this artifact come from, who changed it, and what built it?"
* **Drift:** when a model's behavior or performance changes over time as data, tools, or usage patterns shift.
* **SBOM:** a "bill of materials" for a system-an inventory of components and their relationships.
* **Agent:** an AI pattern where a model plans steps and calls tools/APIs to take actions.

---