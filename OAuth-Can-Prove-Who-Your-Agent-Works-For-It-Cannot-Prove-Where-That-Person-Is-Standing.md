# From Article to Artefacts Vol 3 — OAuth Can Prove Who Your Agent Works For. It Can't Prove Where That Person Is Standing.

**AI agents inherited our identities. They didn't inherit our geography. For regulated data, that gap is now a compliance finding waiting to be written. And per this series' house rule, the argument ships with working artefacts, not just prose.**

Picture this. It's 9:40 pm in Shanghai. An analyst opens Slack from her hotel and types a question to her firm's AI assistant: *"Summarize the payment disputes for our top US retail clients this quarter."*

The assistant wakes up in a datacenter in Virginia. It carries a delegated token — minted days ago, on her behalf, when she was sitting in New York. It calls the customer-data API. The API checks everything it was built to check: valid signature, correct scopes, caller's network location. The caller is in Virginia. Allowed country. Allow.

Ninety seconds later, payment histories for thousands of US customers render in a Slack thread on hotel Wi-Fi in Shanghai.

The scene is hypothetical — I want to be upfront about that. Every component in it is real, deployed, and working exactly as designed. Which is the problem: every control passed, and the outcome is still the one the controls exist to prevent.

## Why banks are geofencing in the first place

If you work anywhere near financial services, you've seen the wave: location-aware access controls appearing on application after application. There's a specific reason, it has teeth, and — stay with me through two minutes of regulation — it's the setup that makes the agent problem land.

Since April 2025, the DOJ's [Data Security Program](https://www.justice.gov/nsd/data-security) (Executive Order 14117, implemented at [28 CFR Part 202](https://www.ecfr.gov/current/title-28/chapter-I/part-202)) restricts giving persons in six "countries of concern" — China including Hong Kong and Macau, Russia, Iran, North Korea, Cuba, and Venezuela — access to bulk US sensitive personal data. "Bulk," for personal financial data, starts at [10,000 US persons](https://www.ecfr.gov/current/title-28/chapter-I/part-202/subpart-B/section-202.205). Almost every consumer-facing system at a bank clears that bar without trying.

Here's the definition that does the work. Under [§ 202.201](https://www.ecfr.gov/current/title-28/chapter-I/part-202/subpart-B/section-202.201), "access" means logical or physical access, including the ability to "otherwise view or receive, in any form." Viewing counts. And the same section says access is determined *without regard* to security requirements — VDI, read-only rights, and watermarking don't take you out of scope. They're how you comply; they never make the question go away.

For a bank's own offshore staff and its vendors, these arrangements become "restricted transactions": lawful only if you implement [CISA's security requirements](https://www.cisa.gov/resources-tools/resources/EO-14117-security-requirements), whose headline obligation reads: *"Implement logical and physical access controls to prevent covered persons or countries of concern from gaining access to covered data."*

That sentence is the origin story of every location-aware access control program in banking right now.

And the clock is real. The rule's compliance obligations — written program, records, audits — have been live since October 5, 2025, which puts the first annual independent audits around October 2026. Penalties ride on IEEPA: the greater of [$377,700 or twice the transaction value](https://www.federalregister.gov/documents/2025/01/15/2025-00786/inflation-adjustment-of-civil-monetary-penalties), per violation. And in June 2026, a federal court in [*Baker v. Index Exchange*](https://www.hsfkramer.com/insights/2026-07/federal-court-finds-doj-bulk-sensitive-data-regulations-open-new-avenue-for-ecpa-suits) let an ECPA class action proceed past a motion to dismiss, with a violation of this rule as the predicate. The DOJ hasn't announced a public enforcement action yet. The plaintiffs' bar didn't wait for one.

## The control everyone is building

The blueprint that has emerged is sensible. Interactive human access gets location-gated. The strongest deployments don't trust network addresses alone: Microsoft Entra, for example, can require [country verification by GPS through the Authenticator app](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-assignment-network) — the phone shares its location hourly, with jailbreak and mock-location detection — precisely because IP addresses lie and VDI hides the endpoint. Citrix has an entire machinery of adaptive access and endpoint-location signals for the same reason.

System identities — service accounts, schedulers, batch pipelines — get handled differently. They have no GPS coordinates and no passport. So they're governed by data entitlements: which *system* may receive which data, with due diligence on where that system runs and who operates it.

Humans get location checks. Machines get entitlements. As a design, it's clean.

It was clean. Then we gave the humans agents.

## Identity travels. Presence doesn't.

When an agent acts for a user, the mechanics are delegation: the user's token is exchanged for a new token that carries the user's identity downstream — the pattern Microsoft calls On-Behalf-Of, generalized by [OAuth 2.0 Token Exchange (RFC 8693)](https://datatracker.ietf.org/doc/html/rfc8693). Think of it as a power of attorney: the agent can act with her authority, sign with her name, open her accounts. What a power of attorney has never included is a passport check.

The standard even defines a claim for it — `act` — so a downstream service can see "this agent is acting for this person." In practice, adoption is uneven: plenty of delegation flows in production ship the user's identity downstream with no actor chain at all.

The identity industry spent the last two years building this out properly. Microsoft shipped [Entra Agent ID](https://learn.microsoft.com/en-us/entra/agent-id/what-is-microsoft-entra-agent-id). Okta is building the [Cross App Access ecosystem](https://www.okta.com/newsroom/press-releases/okta-announces-cross-app-access-partners/). The major identity vendors now all have an answer to "how do agents get identities, credentials, governance."

All of it answers one question: *who does this agent work for?*

None of it answers: *where is that person standing right now?*

So the downstream API receives a human-looking token from a machine's network position. If it evaluates location — as every location-aware control does — it evaluates the agent's datacenter. The user's actual presence was observed exactly once, at sign-in, and never again. Identity propagates through the delegation chain hop after hop.

Presence dies at the first hop.

## Three failures, stacked

**Failure one: time.** Location is evaluated when tokens are issued. Tokens outlive geography. An Entra access token lives roughly [60–90 minutes — 24 to 28 hours with Continuous Access Evaluation](https://learn.microsoft.com/en-us/entra/identity-platform/configurable-token-lifetimes). CAE's near-real-time location enforcement sounds like the fix until you read the constraints: [it works with IP-range named locations, not countries, and only Microsoft's own resource providers participate](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation). Your custom APIs get none of it — if you want revocation on location change for your own services, you are building it yourself, per request, in the service. A user authenticates in New York, boards a fourteen-hour flight, and lands with live credentials. And here's the mechanism people miss: her agents refresh those credentials from *their own* network position — an allowed datacenter — so conditional access sees nothing wrong at refresh either. The same goes for anything long-lived: a streaming connection or an open agent session established before takeoff simply survives the flight unless something actively tears it down.

**Failure two: place.** The gate geolocates the wrong party. Agent infrastructure sits in whichever cloud region you deployed it — an allowed country, nearly by definition. The human behind the request could be anywhere on Earth. IP-based location control applied to delegated traffic measures your cloud provider's geography, not your user's.

**Failure three: the last screen.** Go back to § 202.201: access includes the ability to view or receive data "in any form... through information systems." On a plain reading, the operative event in my opening scene isn't the API call in Virginia. It's the rendering in Shanghai. And the rendering surfaces are exactly the ones nobody geofences — the Slack thread, the emailed digest, the push notification, the BI dashboard, the agent's own chat window. Control estates end precisely where data becomes visible.

Any one of these is a finding. Together, they're a pattern: we built location controls for a world where the requester's network position revealed the principal's physical position. Delegated agents quietly ended that world.

## Your classifier answers the wrong question

Here's the design decision doing the damage. Most programs decide "human or system?" by token plumbing: client-credentials tokens are machine traffic — exempt from location gating, governed by entitlements. User tokens are human traffic — gated.

Delegation breaks this classifier in both directions at once. On-behalf-of traffic carries user tokens, so it gets location-gated — against the agent's datacenter, the wrong location. Meanwhile, human-directed retrieval that happens to run under a pure service identity sails through with no location check at all, because the system said "machine."

The classifier answers "what kind of token is this?" The regulation asks "did a person in a country of concern obtain the data?" Those are different questions, and the gap between them is exactly agent-shaped.

There's a second-order effect worth naming, because I've watched versions of it play out in every hard compliance gate: agent traffic is noisy, novel, and nobody's fault. When a "no control, no production" deadline meets a wave of agent false positives, the resolution is predictable — a blanket exemption for the agent tier, filed as temporary. Controls rarely die in the codebase. They die in the exemption register. Auditors read exemption registers first. Engineers never do.

## What good looks like

I don't think this is unsolvable. I think it's unspecified. Five things I'd push for:

**1. Make presence a claim, not an assumption.** An attested, short-lived location assertion — GPS attestation from the authenticator, or verified network evidence — bound into the delegation chain next to `act`. Stale or missing presence claim? Location is unknown; for covered data, unknown means deny. Keep the evaluation local and cheap — this check runs on every request to covered endpoints, so it has to cost microseconds, not a network hop.

**2. Gate the human touchpoints, not just the middle.** Task initiation — where is the user *as she delegates*? — and result delivery — where is the recipient *as this renders*? Those are the two moments presence is real. Every hop in between sees machines talking to machines.

**3. Shorten delegation for covered scopes.** No multi-day refresh chains carrying access to regulated data. Long-running tasks re-attest presence to continue, and long-lived connections get maximum ages tied to the attestation window. Inconvenient, yes. So is the alternative.

**4. Reclassify honestly.** The question is not "what grant type is this token." It's "can covered data reach a human, and where is that human?" Fully autonomous pipelines whose output never renders to a person belong in the entitlement regime. Everything else — including your chatbot — is in location scope.

**5. Log like plaintiffs' counsel will read it.** After *Baker*, decision logs aren't just audit evidence; they're potential discovery material. Decision, signals used, policy version, retention. And one thing more: carry a correlation ID through the whole delegation chain — human, agent, API, rendering surface — because if you can't reconstruct that chain end to end, you can't investigate my opening scene, let alone defend it.

One more note, because rollout is where these programs live or die: turn the control on in report-only mode first, and measure the false-positive rate on agent traffic specifically — that number, not the architecture diagram, decides whether your exemption register stays empty. Enforce by cohort, not big bang.

And if you lead a team rather than build the controls, here is the one question worth asking this week: if a regulator asked where your agents' answers rendered last quarter, could anyone produce the report?

## Ship the control as code, not as prose

Regular readers know where this is heading. I've written before about phantom controls — compliance artifacts that exist only as prose, describing controls nobody actually deployed, undetected until an assessor or a penetration test finds the gap. The cure is the same one NIST built [OSCAL](https://pages.nist.gov/OSCAL/) for: make the control machine-readable, then make the machine prove it ran.

So I did the encoding. As far as I can tell, the [CISA Security Requirements](https://www.federalregister.gov/documents/2025/01/08/2024-31479/notice-of-availability-of-security-requirements-for-restricted-transactions-under-executive-order) behind all of this — the document driving the largest access-control retrofit banking has seen in years — have never been published as OSCAL. I've drafted an unofficial catalog of them, plus a small "presence propagation" overlay that turns the five recommendations above into actual OSCAL controls with parameters: the blocked-country list, the attestation maximum age, the delegation lifetime, the log retention. Alongside them, component definitions for the three building blocks — a presence-attestation service, a location-gate middleware, and a delivery-surface gate. All of it validates against the official OSCAL v1.1.3 schemas.

The part I find most interesting is the runtime loop. In my earlier [OSCAL guardrails experiments](https://github.com/ai-agents-cybersecurity), an OSCAL profile acts as the policy brain an agent consults before any tool call — and in [oscal-skills-guardrails](https://github.com/sw30labs/oscal-skills-guardrails) that same loop already vets every *skill* an agent loads: policy in, evidence out. Add presence, and the profile that *documents* the location control becomes the policy that *enforces* it — the agent checks the principal's attested location against the catalog before touching covered data, and every decision flows back as machine-readable assessment evidence. The document is the control. The control assesses itself. The new PoC, **oscal-presence-gate** — landing in [sw30labs](https://github.com/sw30labs) with everything I build from here on — completes the set: skills-guardrails gates *what* an agent may load, agent-guardrails gates *which tools* it may call, and this one gates *where the human it serves is standing*. It runs — planner, presence verifier, policy enforcer, evidence emitter, eighteen passing tests including the Shanghai scene above as an executable fixture — and everything it emits validates against the official OSCAL schemas.

## Where this goes

This isn't only a banking story. The same rule covers health records above 10,000 US persons and precise geolocation above 1,000 devices — and the same delegation mechanics ship in every enterprise agent platform. Any organization putting agents on top of regulated data inherits this gap on day one.

A falsifiable prediction to close. The delegation stack will grow a presence claim — some attested `loc` living beside `act` — and it will be forced by a regulator, not finished by a standards body. Compliance deadlines move faster than working groups. When the first audit or the first discovery request asks "prove the human behind this agent wasn't in a country of concern," the industry will retrofit in months what it declined to standardize in years.

I could be wrong about the mechanism. I don't think I'm wrong about the gap.

Somewhere right now, an analyst in a hotel is typing a question to an assistant that will answer from the wrong side of a border neither of them can see.

How is your organization classifying agent traffic today — by token type, or by where the data lands?

---

*Views are my own. Nothing here is legal advice; the regulatory reads are my practitioner's summary of public sources, linked throughout.*
