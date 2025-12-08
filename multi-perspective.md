Multi-Perspective Prompting

Anthropic's Constitutional AI uses multiple viewpoints to reduce bias and improve reasoning.

Template:

Analyze [topic/problem] from these perspectives:

[PERSPECTIVE 1: Technical Feasibility]
[specific lens]

[PERSPECTIVE 2: Business Impact]
[specific lens]

[PERSPECTIVE 3: User Experience]
[specific lens]

[PERSPECTIVE 4: Risk/Security]
[specific lens]

SYNTHESIS:
Integrate all perspectives into a final recommendation with trade-offs clearly stated.

---

Example:

Analyze whether we should migrate from Postgres to DynamoDB from these perspectives:

[PERSPECTIVE 1: Technical Feasibility]
Engineering complexity, timeline, data migration risks

[PERSPECTIVE 2: Business Impact]
Cost implications, team velocity, vendor lock-in

[PERSPECTIVE 3: User Experience]
Latency changes, feature implications, downtime requirements

[PERSPECTIVE 4: Risk/Security]
Data consistency guarantees, backup procedures, compliance

SYNTHESIS:
Integrate all perspectives into a final recommendation with trade-offs clearly stated.

---

Gets you strategic thinking instead of surface-level advice.
