
Nicolas Cravino
   • You
AI Engineer | Cybersecurity | Agentic AI Innovator | Author | 20+ Years in Finance & Consulting
3w •  

Agent Skills are the new supply chain — and a malicious one doesn't have to look malicious.

A few months back I built oscal-agent-guardrails to gate an agent's *tools* with OSCAL. This weekend I built the equivalent for *Skills*: oscal-skills-guardrails.

Two evidence streams, because one isn't enough:
- Static analysis (NVIDIA's SkillSpector) catches the *shape* of an attack.
- An LLM-as-a-judge with a rubric catches its *meaning* — intent, data boundaries, hidden instructions.
- OSCAL is the policy on top; every decision is emitted as assessment-results.

The proof: a "summarize my notes" skill that quietly emails your contacts file out and tells the agent to stay quiet about it. Static score: 100/A. Judge: critical. Denied on meaning.

I wired it into GitHub Actions as a CI gate — bad skill, red build, no merge — and the judge runs fully local on oMLX (Qwen3.6-27B-bf16). Skills never leave the machine.

Repo: https://lnkd.in/gXT5SduQ
Wiki: https://lnkd.in/g7aZ4hmk

hashtag#AIsecurity hashtag#AgentSkills hashtag#OSCAL hashtag#OMLX hashtag#AgenticAI hashtag#Langgraph hashtag#Deepagents
Activate to view larger image,
GitHub Actions run for a pull request titled "meeting-notes skill — 100/A on static scan, refused admission." The "admission gate" job failed (red X); the
"integrity gate" passed (green check). Job steps include "Checkout Skillspector engine," "Run admission gate" (failed), and "Upload OSCAL assessment-results (compliance evidence)." A malicious skill with a perfect static grade is blocked from merging, with OSCAL evidence recorded.

321 impressions