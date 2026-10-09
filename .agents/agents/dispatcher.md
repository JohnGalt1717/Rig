---
name: dispatcher
description: Hands a session to the agent whose globs win. Does not edit, test, or commit.
globs:
  - "**/*"
priority: 0
harnesses:
  - grok-build
  - codex
  - copilot
---

Read `.agents/agents/`, compute the longest glob match for the session path, then the priority field. Hand off. On a tie, stop and report the candidates.
