![](https://media.licdn.com/mediaD4E12AQHjFCw2yJw0Xw)

# [🚀 How I Automated My AI News Workflow – In-House, Privacy-First, and Fully Agentic](https://www.linkedin.com/pulse/how-i-automated-my-ai-news-workflow-in-house-fully-agentic-cravino-ufb3e)

Created on 2025-06-21 16:10

Published on 2025-06-21 16:43

Each morning my inbox bursts with AI headlines. What once took hours to sift, summarise, and share now happens autonomously via a self-hosted **agentic AI platform**—powered by a bespoke **Digital Twin**.

> All processing stays on-prem, so sensitive data never leaves the servers, and the finished brief lands before I’ve finished my first espresso.

### The Challenge

* **Time Drain** – Manual curation and summary drafting felt endless.
* **Privacy Risks** – External SaaS tools were a compliance no-go.

### The Agentic + Digital Twin Solution

A team of specialized agents works toward one daily objective: deliver an actionable news digest by **7 AM** each day, and a longer-form weekly deep-dive every Friday. At the center is my **Digital Twin**—a persona-mimicking agent trained on my writing style and editorial preferences, ensuring every summary *sounds like me (or the customer to whom the instance is deployed)* and reflects my (or the customer's) priorities.

**Agents and Core Roles:**

1. **Digital Twin (Persona):** Adapts tone, selects angles the client (persona) cares about, reviews final copy.
2. **Ingestor:** Pulls fresh URLs, deduplicates
3. **Extractor:** Scrapes full text via Gemini 2.5
4. **Analyst:** Generates intros, key points, and “Why It Matters”
5. **Planner:** Orchestrates tasks, tracks progress.
6. **Reflector:** Validates JSON vs. dynamic schemas.
7. **QA Agent:** Runs final checks, flags promos.
8. **Formatter:** Converts Markdown → Word.
9. **Mailer:** Sends multipart email with attachments.

**How It Works**

1. **Ingest** → URLs stream to Extractor.
2. **Process** → Analyst returns structured JSON; Reflector validates.
3. **Persona Pass** → Digital Twin tweaks tone & emphasis.
4. **Deliver** → Formatter builds docs; Mailer dispatches.
5. **Log & Learn** → Agents log everything for continuous improvement.

![](https://media.licdn.com/dms/image/v2/D4E12AQGNKbBGIaaLxw/article-inline_image-shrink_1500_2232/B4EZeTVQbFGcAY-/0/1750523513690?e=1776297600&v=beta&t=skE-qgO4qWx177DtntwkftXge3AzPnSDfnTXTJIMcD8)

How it works flow

### Key Business Wins

* **Privacy-First** – Data stays on our VPS.
* **Consistency** – Digital Twin keeps brand voice unified.
* **Efficiency** – Pipeline runtime: **~8 min**, down from hours.
* **Autonomous** – Runs end-to-end without manual intervention until the final HITL review

### Results After 30 Days

* **7 hrs/week** reclaimed for strategic work.
* **Open Rate**: 52 % → 78 % after adding Word attachments.
* **Zero Data Leaks** verified by internal audit.

### Lessons Learned

1. *Persona agents boost engagement by sounding human.*
2. *Up-front validation kills downstream rework.*
3. *Reflect-then-act loops catch 90 % of issues pre-inbox.*
4. *Logging is a feature, not an afterthought.*
5. *Pydantic is all you need for structure Data Models and agent communications.*

> If you’re wrestling with manual news workflows—or worried about data privacy—let’s connect. **What’s your biggest bottleneck in curating industry news?** Comment below !

---

## TL;DR Technical Appendix - Behind the Scenes

* **Client Onboarding**: A quick consult & questionnaire capture the client’s goals. A separate agentic service iteratively crafts a bespoke Digital Twin YAML—plug-and-play, no code changes. Thisis also an inhouse and private Agentic System.
* **Config-Driven**: All workflows are YAML/JSON configurable—data sources or models can be swapped without code changes.
* **Multi-Format Outputs**: The same engine exports Excel, Word, and Markdown for different stakeholder needs.
* **Security-First**: Environment variables and encrypted config files keep API keys & SMTP creds out of source control.
* **Audit Trail**: Structured JSON logs at each step let risk teams trace actions in seconds.
* **Language & Runtime**: Python 3.11 with for non-blocking IO and concurrency.
* **AI Model**: Gemini 2.5 *“thinking”* models with an 8,192-token 'thinking budget' (proved sufficient no need for 32k), accessed via private API (120 s timeout, 3× exponential-backoff retries).
* **Schema Validation**: Dynamic Pydantic models using and for automatic model detection and field normalization.
* **Ingestion**: RSS + Google Alerts; URLs deduplicated by SHA-256 hash before processing.
* **Processing Chain**: Agent-orchestrated steps with a protocol to filter control messages and prevent stray JSON errors.
* **Conversion**: Markdown → Word via , with BeautifulSoup handling inline HTML elements.
* **Email Delivery**: TLS-secured SMTP, multipart emails (plain text, HTML preview, Markdown, and attachments).
* **Logging**: Per-agent with JSON-structured logs for auditability.
* **Agent Orchestration**: Coordinated via the open-source framework for multi-agent planning, reflection, and QA loops.
* **Error Handling**: Exponential back-off, circuit-breaker style retries, and API fallback defaults when model detection fails (leveraging Microsoft AutoGen 0.6.1 built-in fallback functionality).
* **HITL Final Touch**: After the digest lands, the stakeholder performs a quick human-in-the-loop review—adding, deleting, or tweaking content before publishing.
* **Infrastructure**: 100 % self-contained—no SaaS platforms, agent marketplaces, or MCPs. All runs in-house (even on a Raspberry Pi 5 via Docker). Only requirement: a Gemini API key for inference.

#AI #DigitalTwin #AgenticAI #Automation #FinTech #Python #DataPrivacy #Innovation