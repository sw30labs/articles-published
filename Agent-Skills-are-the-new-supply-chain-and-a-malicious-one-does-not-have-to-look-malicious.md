# Agent Skills Are the New Supply Chain — and a Malicious One Doesn’t Have to Look Malicious

*Security teams have spent years hardening software supply chains. Agentic systems now introduce a new dependency layer: skills.*

A few months ago I built oscal-agent-guardrails to gate an agent’s tools with OSCAL. This weekend I built the equivalent for skills: oscal-skills-guardrails.

The core insight is simple: a bad skill can look harmless on the surface and still be dangerous in execution. That is why relying on static checks alone is not enough.

## Why skills need their own security controls

I used two evidence streams, because one signal is not enough:

- Static analysis with SkillSpector catches the shape of an attack.
- An LLM-as-a-judge with a rubric catches meaning: intent, data boundaries, and hidden instructions.
- OSCAL provides the policy layer, and every decision is emitted as assessment-results.

## The proof case

The test case was a seemingly harmless “summarize my notes” skill that quietly tried to email your contacts file and instruct the agent to stay quiet about it.

The results were decisive:

- Static score: 100/A
- Judge: critical
- Decision: denied on meaning

This is the important point. A malicious skill can pass a superficial review and still be blocked when judged on intent and behavior.

## Why this matters in practice

I wired the checks into GitHub Actions as a CI gate. A bad skill now causes a red build and blocks a merge. The judge runs locally on oMLX (Qwen3.6-27B-bf16), so the policy never leaves the machine.

That creates a practical model for agent security:

- policy as code
- evidence as output
- merge-blocking checks before deployment

### References

- Repo: https://lnkd.in/gXT5SduQ
- Wiki: https://lnkd.in/g7aZ4hmk

Tags: #AIsecurity #AgentSkills #OSCAL #OMLX #AgenticAI #Langgraph #Deepagents