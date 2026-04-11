![](https://media.licdn.com/mediaD4E12AQEUhR0SVec16g)

# [Understanding AI Agent Security: Two Analogies That Make It Click](https://www.linkedin.com/pulse/understanding-ai-agent-security-two-analogies-make-click-cravino-nddde)

Created on 2026-02-21 15:26

Published on 2026-02-21 15:52

If you work in cybersecurity - or anywhere near it - you've probably been asked the same questions I get asked all the time: *How do we secure Ai Agents? And* ***how do I explain this to the board****?*

I've had these conversations more times than I can count. With CISOs trying to articulate risk to their executive teams. With board members who need to understand the exposure without drowning in jargon. With engineers who want a clear mental model. And with everyday professionals who just want to know: *should I be worried?*

The challenge is always the same. AI agent security spans identity management, secrets storage, policy enforcement, observability, and fail-safe mechanisms - and when you explain all of that in abstract technical terms, people's eyes glaze over.

So I started reaching for analogies. The two that resonate most consistently are **aviation** and **banking**. Everyone understands that planes need licensed pilots, regulations, air traffic control, and emergency protocols. Everyone understands that banks need identity verification, vaults, compliance rules, and the ability to freeze an account when something goes wrong.

That's why I wrote this short article. Not as a technical manual, but as a practical tool you can use - whether you're briefing the board, aligning your engineering team, or wrapping your own head around it. Please, feel free to borrow the analogies and share them. If it helps one person in your organization understand what we're facing with autonomous AI, it's done its job.

---

## Why This Matters Right Now

AI agents - autonomous systems powered by large language models that log into services, call APIs, and make decisions without human intervention - are already in production. Dynatrace's 2026 research shows 50% of organizations have agentic AI deployed, but most lack the governance to run it safely. (I have explored this in the past and written articles on this, that legacy 'linear governance' cannot match the AI Machine era.

In December 2025, OWASP released the Top 10 for Agentic Applications, identifying risks from agent goal hijacking to identity exploits and cascading multi-agent failures. NIST has issued its own RFI on AI agent security. The regulatory environment is tightening.

> A person might make one mistake. An agent can make thousands before anyone notices.

We need a governance framework. My proposal is to simplify it across seven layers.

---

## The Seven Layers - Through Two Lenses

### Layer 1: Build & Supply Chain

**Aviation:** Aircraft are manufactured by specialists to strict standards. Every component - engines, avionics, even bolts - must come from certified suppliers with documented provenance. When a part is defective, the FAA grounds the entire fleet until it's replaced.

**Banking:** Every vendor touching a bank's systems goes through rigorous due diligence: SOC 2 audits, penetration testing, ongoing monitoring.

**For AI Agents:** Use purpose-built frameworks, not custom-built cobbled-together systems. But building well is only half the battle - you also need to vet your entire supply chain. Know where your foundation model comes from and what it was trained on. Audit every plugin, tool, and MCP server your agents can invoke at runtime. Maintain a Software Bill of Materials (SBOM) so that when a vulnerability is disclosed, you know in minutes - not days - which agents are exposed. OWASP flags tool misuse (ASI02) and supply chain vulnerabilities (ASI04) as top agentic risks. A compromised base model is the equivalent of a defective engine: everything downstream is at risk.

---

### Layer 2: Identity & Credentials

**Aviation:** The FAA verifies identity, confirms training, issues ratings, and checks medical fitness. A student pilot can't fly a 747. Permissions are specific and layered.

**Banking:** KYC regulations require proof of identity and screening against watchlists. A teller has different access than a branch manager.

**For AI Agents:** Every agent needs a non-human identity (NHI) with credentials scoped to its specific role - least privilege, task-scoped, time-bound. OWASP identifies identity and access exploits as a top risk: attackers manipulate delegation chains to escalate privileges. Lifecycle management is critical: issuance, rotation, revocation.

---

### Layer 3: Secure Storage (The Vault)

**Aviation:** After 9/11, cockpit doors became reinforced and locked. Flight systems are accessible only to authorized crew.

**Banking:** Time-locked vaults, dual-key access, comprehensive audit trails. Every access logged, every withdrawal tracked.

**For AI Agents:** A secrets vault provides secure, audited, check-in/check-out access to API keys, tokens, and certificates. No hardcoded credentials. No plaintext storage. Every access logged, time-limited, and automatically rotated.

---

### Layer 4: Policies & Rules

**Aviation:** Airspace classifications, altitude restrictions, no-fly zones, mandatory procedures. The Federal Aviation Regulations fill entire bookshelves.

**Banking:** SEC rules, AML laws, transaction limits, risk thresholds.

**For AI Agents:** Comprehensive policies covering six domains: bias detection, drift monitoring, reliability and explainability, trust and safety, hate/abuse/profanity prevention, and intellectual property protection. Agents operate at machine speed - a single policy failure can scale to millions of interactions before someone catches it.

---

### Layer 5: Evaluations (aka 'Evals')

**Aviation:** No plane takes off without a pre-flight inspection. Pilots undergo recurrent training in simulators - practicing engine failures and system malfunctions on a strict schedule, not just when something feels off.

**Banking:** After 2008, the Fed introduced mandatory stress tests (CCAR). Banks must prove they can survive catastrophic scenarios before continuing normal operations. Not optional. Not self-graded.

**For AI Agents:** Evals are the pre-flight checklist and the stress test combined. Accuracy benchmarks against known test sets. Red-teaming with adversarial probes and prompt injections. Regression testing on every model update. Continuous scoring in production - sampling outputs and flagging degradation.

Without evals, you're flying blind. You might not know your agent is drifting, hallucinating, or producing biased results until the damage is already done. Evals are the mechanism that turns your policies from aspirational goals into measurable, enforceable standards. And just like stress tests and pre-flight checks, they need to happen on a schedule - not just when something feels off.

---

### Layer 6: Enforcement, Observability & Human Oversight

**Aviation:** Air traffic control provides real-time monitoring and clearances, backed by radar and flight data recorders. When conditions exceed thresholds, ATC hands control to the pilot - a human-in-the-loop override.

**Banking:** Real-time transaction monitoring, anomaly detection, daily reconciliation. Transfers above certain thresholds require a manager's sign-off.

**For AI Agents - three integrated capabilities:**

**Enforcement (the AI Gateway):** A checkpoint between the agent and its resources. Inbound check: is this authorized and within policy? Outbound check: are the results safe and compliant?

**Observability (the Control Plane):** 70% of organizations already use observability tooling with their agents. End-to-end traces reconstruct the complete decision path for any interaction - every LLM call, tool invocation, and intermediate decision captured with full context. Structured logging records every input and output. Real-time dashboards surface anomalies before they become incidents. Without this visibility, your gateway is making decisions in the dark.

**Human-in-the-Loop (Graduated Autonomy):** Not every action should be fully autonomous. Low-risk actions proceed automatically. Medium-risk gets logged for review. High-risk routes to a human approver before execution. This mirrors the aviation model where routine flight is handled by auto-pilot, but critical decisions require a human hand on the controls. The key: these escalation paths must be designed into the architecture from day one, not bolted on after an incident. Manual review alone cannot keep pace with machine-speed operations, which is why automated monitoring and selective human escalation must work together.

---

### Layer 7: Circuit Breakers

**Aviation:** Engine fire suppression activates automatically. Auto-pilot can be disconnected. Black boxes record everything for investigators.

**Banking:** Fraud detection freezes accounts instantly. Suspicious Activity Reports are filed. Forensic investigation follows.

**For AI Agents:** Circuit breakers are automated fail-safes for when things go seriously wrong:

* **Kill switches** that trigger on anomaly spikes - no human intervention required
* **Rate limiting & token budget caps** - hard ceilings on requests, tokens, and cost
* **Rollback to last known good** - automatic revert to the previous model version or policy set
* **Immutable audit trail** - every action logged in tamper-proof records for post-mortem

> Circuit breakers aren't a sign of failure. They're a sign of maturity. Every serious financial institution has them. Every serious AI deployment should too.

---

### Bringing It All Together

Seven layers. One integrated system:

1. **Build** with established tools - and vet every component in your supply chain;
2. **Manage identities** with least privilege, scoped credentials, and full lifecycle management;
3. **Store secrets** in a vault - never hardcoded, always audited, regularly rotated;
4. **Define policies** covering bias, drift, reliability, trust, harmful content, and IP;
5. **Evaluate relentlessly** - benchmark, red-team, regression-test, and score continuously;
6. **Enforce, observe, and escalate** - gateway + observability + human-in-the-loop, designed as one system; and
7. **Install circuit breakers** - auto-shutdown, rollback, and immutable logging.

These layers **are not independent**. A pilot's license means nothing without airspace rules. A bank vault is useless without KYC. Policies without evals are just words on paper. Enforcement without observability is flying blind. And all of it is incomplete without circuit breakers.

*The good news:* tools exist today for every layer of this framework - from agent-building platforms and dependency scanners to identity management systems, secrets vaults, policy engines, evaluation frameworks, AI gateways, observability platforms, and circuit breaker patterns. The infrastructure is available. What's needed is the organizational commitment to implement it as the integrated whole it needs to be.

The regulatory environment is tightening too. NIST has issued a request for information specifically focused on security considerations for AI agents, signaling that formal standards are on the horizon. Organizations that build this governance infrastructure now will be ahead of the curve - not scrambling to retrofit it later.

Just as we wouldn't let unlicensed pilots into uncontrolled airspace, or allow unverified individuals into bank vaults, we shouldn't deploy AI agents without the governance to keep them certified, evaluated, observed, and fail-safe.

The destination is worth reaching. Let's make sure we get there safely.

*If you found this useful, share it with someone who's trying to explain AI agent security to their board, their team, or their peers. The analogies are yours to borrow.*

---

**## References**

1. [[OWASP Top 10 for Agentic Applications (2026)](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)]
2. [[Dynatrace - Building Trust in Agentic AI: Observability-led Action Plan (2026)](https://www.dynatrace.com/news/blog/agentic-ai-report-new-observability-strategy/)]
3. [[OWASP Top 10 for LLM Applications (2025)](https://genai.owasp.org/resource/owasp-top-10-for-llm-applications-2025/)]
4. [[OWASP LLM Top 10 - Full Risk List](https://genai.owasp.org/llm-top-10/)]
5. [[SiliconANGLE - Human-in-the-Loop Has Hit the Wall (Jan 2026)](https://siliconangle.com/2026/01/18/human-loop-hit-wall-time-ai-oversee-ai/)]
6. [[NIST - RFI: Security Considerations for AI Agents (Jan 2026)](https://www.federalregister.gov/documents/2026/01/08/2026-00206/request-for-information-regarding-security-considerations-for-artificial-intelligence-agents)]
7. [[OWASP GenAI Security Project - Agentic AI Security Release](https://genai.owasp.org/2025/12/09/owasp-genai-security-project-releases-top-10-risks-and-mitigations-for-agentic-ai-security/)]
8. [[Confident AI - OWASP Top 10 2025: Risks & Mitigation](https://www.confident-ai.com/blog/owasp-top-10-2025-for-llm-applications-risks-and-mitigation-techniques)]
9. [[Braintrust - AI Observability Tools Buyer's Guide (2026)](https://www.braintrust.dev/articles/best-ai-observability-tools-2026)]
10. [[Superteams.ai](http://Superteams.ai) - [Building Guardrails for AI Agents (Jul 2025)](https://www.superteams.ai/blog/newletter-july-2025-how-to-build-strong-guardrails-for-ai-agents)]
11. [<https://www.practical-devsecops.com/owasp-top-10-agentic-applications/>)]
12. [[Aikido - OWASP Agentic Applications Full Guide](https://www.aikido.dev/blog/owasp-top-10-agentic-applications)]
13. [[Lares Labs - OWASP Agentic AI Top 10: Threats in the Wild](https://labs.lares.com/owasp-agentic-top-10/)]
14. [[Nibzard - The Agentic AI Handbook: Production-Ready Patterns](https://www.nibzard.com/agentic-handbook)]