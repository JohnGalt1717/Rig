# Context

Rig is the harness. Grok Build, Codex, Copilot, and anything else on ACP are guests. The host machine owns the checkout, the agent process, the language server, and the simulator. Other windows attach through the backplane and send intents.

Decisions already made, and not open for a drive-by rewrite:

- One `.agents/` at the repo root. Globs select what loads. The panel shows what loaded and why.
- The backplane forwards ciphertext and directory state. It is not an application backend.
- Credentials: schema committed, values not. Injected from the keychain. GitHub Actions secrets are not the vault.
- MinimalWebTransport is a separate library, consumed as a NuGet package.
- Backend state is SQLite and Entity Framework on .NET 11. Personal and organization are the same model, chosen by membership.
- One Flutter app, `Apps/rig`. Shared Flutter code in `Apps/shared`.

Open decisions are listed in `docs/plans/00-grill-index.md`. Implementation waits on those sessions.
