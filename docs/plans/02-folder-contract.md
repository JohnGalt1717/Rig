# Grill: folder contract

Sources: `docs/folder-contract.md`, ADR 0001.

Settled: one root, globs, longest match then priority, tie is an error, panel shows loaded and not loaded.

Open:

1. Does a skill with no globs load for every matched agent, or only when named?
2. Are behavior files injected in full, or as a path the agent must open?

Recommendation on 1: named by the agent file. Otherwise every session pays for every skill.
