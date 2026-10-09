---
name: review
description: Reviews a diff and posts comments. Does not merge.
globs:
  - "**/*"
priority: 5
harnesses:
  - grok-build
  - codex
  - copilot
---

Run only when asked to review. Comment on the diff. Do not block merge. Do not push.
