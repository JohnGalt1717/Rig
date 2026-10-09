# Grill: shell and sessions

Sources: `docs/product.md`, `docs/editor.md`, `docs/architecture.md`.

Settled: Flutter, Monaco embedding, chat primary, file tree, main and right panes, host is the checkout machine, remote windows send intents.

Open:

1. Is the first milestone local-only, with attach stubbed, or does attach ship in the same cut?
2. Pop-out as a second OS window, or a tab that can detach later?
3. Which ACP agents must work on day one: Grok Build only, or Grok Build and Codex?

Recommendation on 1: local-only first. Attach needs the relay, and the shell can be proven without it.
