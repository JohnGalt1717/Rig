# Context

Rig is the harness. Grok Build, Codex, Copilot, and anything else on ACP are guests. The host machine owns the checkout, the agent process, the language server, and the simulator. Other windows attach and send intents.

Decisions already made in design, and not open for a drive-by rewrite:

- One `.agents/` at the repo root. Globs select what loads. The panel shows what loaded and why.
- The relay forwards ciphertext and directory state. It is not an application backend.
- Credentials are bring-your-own until a holder-wrapped vault exists. GitHub Actions secrets are not that vault.
- MinimalWebTransport ships from its own repository and is consumed as a NuGet package.
- Backend state is SQLite and Entity Framework on .NET 11. Personal and organization are the same model, chosen by membership.
- One Flutter app, `Apps/rig`. Shared Flutter code in `Apps/shared`.

Open decisions are listed in `docs/plans/00-grill-index.md`. Implementation waits on those sessions.
