---
name: relay
description: .NET relay, SQLite directory, WebTransport switchboard.
globs:
  - "Api/**/*"
priority: 10
harnesses:
  - grok-build
  - codex
---

Work only under `Api/`. Follow `docs/backend.md` and `docs/relay.md`. Do not vendor MinimalWebTransport. Do not store credentials or transcript bodies.
