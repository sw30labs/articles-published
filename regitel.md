View Nicolas Cravino’s  graphic link# RegIntel: An AI Agent for Penetration Testing Regulation Intelligence

*Keeping up with penetration testing regulations across jurisdictions is difficult, expensive, and constantly changing. RegIntel tries to make that process more systematic.*

Keeping up with penetration testing regulations across financial services jurisdictions is a challenge. DORA, CBEST, MAS TRM, CPS 234, and PCI DSS all have different requirements, frequencies, and scope. And they keep changing.

That is why I built RegIntel: an open-source AI agent system that researches, validates, and maintains a global inventory of pentest regulations across more than 20 jurisdictions.

## How it works

The system uses a LangGraph pipeline in which specialized agents:

- research through web search
- validate findings
- run a mandatory reflection quality gate before anything is written to the database

It also uses a dual-LLM strategy:

- cloud models for accuracy-critical tasks
- a local model, Qwen 3.5 122B on Apple Silicon, to keep costs down

## The practical workflow

A single command scans the landscape:

```bash
regitel scan --all
```

The project is Apache 2.0 licensed and open for feedback and contributions.

Repository: https://lnkd.in/egkTc9je

Tags: #OpenSource #Cybersecurity #PenetrationTesting #AI #LangGraph #FinancialServices #RegTech #AgenticAI
