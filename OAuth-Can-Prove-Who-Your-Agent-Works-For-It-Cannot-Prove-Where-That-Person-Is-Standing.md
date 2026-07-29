# OAuth Can Prove Who Your Agent Works For. It Cannot Prove Where That Person Is Standing.

*AI agents inherit our identities, but not our geography. For regulated data, that gap is now a compliance problem waiting to be written down.*

Picture this: it is 9:40 p.m. in Shanghai, and an analyst opens Slack from her hotel and asks her firm’s AI assistant to summarize payment disputes for top U.S. retail clients this quarter.

The assistant wakes up in a datacenter in Virginia and carries a delegated token minted on her behalf when she was in New York. It calls the customer-data API, which checks the signature, scopes, and network location. The caller is in Virginia. The request is allowed.

Ninety seconds later, payment histories for thousands of U.S. customers appear in a Slack thread on hotel Wi-Fi in Shanghai.

The scenario is hypothetical, but every component in it is real and deployed. That is the problem. Every control passed, and the outcome is still the one the controls were meant to prevent.

## Why this matters

If you work in financial services, you have seen the wave of location-aware access controls sweep through applications. The reason is straightforward: regulations increasingly restrict access to sensitive U.S. data from certain countries and regions.

The DOJ’s Data Security Program and related CISA security requirements place real obligations on banks and service providers. Location-aware controls are no longer optional for covered data flows.

## The control everyone is building

The design pattern is sensible:

- human access gets location-gated
- system identities are governed by entitlements
- location checks are layered on top of identity and conditional access policies

The problem is that agents break the old classification.

## Identity travels. Presence does not.

When an agent acts for a user, delegation moves the user’s identity downstream. The agent can act with the user’s authority, but that does not mean the human’s current physical location is known or being re-verified.

That creates a structural gap:

- identity propagates
- presence does not
- location controls often evaluate the wrong party, namely the agent’s datacenter rather than the human behind the request

## Three failures stacked together

The issue is not one single error. It is a stack of three failures:

1. Time: tokens outlive geography, and location is often checked only at issuance.
2. Place: controls geolocate the infrastructure rather than the human user.
3. Delivery: the regulated data becomes visible at the rendering surface, not only at the API call.

Any one of these is a finding. Together, they form a pattern that is especially dangerous for agentic systems.

## What good looks like

The fix is not unsolved, but it is under-specified. Five changes would make a meaningful difference:

1. Make presence a claim, not an assumption.
2. Gate the human touchpoints, not just the middle hop.
3. Shorten delegation for covered scopes.
4. Reclassify traffic by the human impact of the data, not only by token type.
5. Log the full delegation chain so it can be audited and defended.

## The bigger point

This is not only a banking story. The same gap exists in healthcare, regulated data handling, and enterprise agent deployments more broadly.

The real question is not whether agents can be delegated. It is whether organizations can prove where the human behind the delegation was when the data was accessed and rendered.

That is the compliance challenge now.
