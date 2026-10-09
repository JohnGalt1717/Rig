# Flows

`.agents/flows/` holds workflows. A flow is data: steps, branches, the skill that executes each step, and the condition that picks a branch. A skill runs a flow. The agent does not improvise the sequence once a flow matches.

A flow run is a trace the runner already recorded. One click opens that trace against the flow: which step ran, which branch was taken, what the tool returned, where it timed out. The agent can propose a change to the flow or to the skill from that trace. The change is a diff in `.agents/flows/` or `.agents/skills/`. It is not a silent edit to the session.

Flows are how repeated work stops making the same mistake. The grill writes the first flow. A failed trace is the reason to edit it.
