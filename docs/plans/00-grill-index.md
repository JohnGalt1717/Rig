# Grill index

These sessions gate implementation. Each plan is a grill-with-docs brief: sources are the docs in this folder, the frontier is the open questions, and execution starts only after the frontier is empty.

| Plan | Gate for |
| --- | --- |
| [01-shell-and-sessions.md](01-shell-and-sessions.md) | Flutter shell, tabs, pop-out, home page |
| [02-folder-contract.md](02-folder-contract.md) | Loader, globs, panel |
| [03-relay-and-data.md](03-relay-and-data.md) | .NET 11 relay, SQLite, personal and org |
| [04-credentials-and-init.md](04-credentials-and-init.md) | `/init`, schema, keychain |
| [05-language-packs.md](05-language-packs.md) | Flutter and C# packs, e2e runner |
| [06-git-and-review.md](06-git-and-review.md) | Identity, pull requests, review agents |

Do not start a later plan's code while an earlier plan's frontier is open, except 03, which can proceed against the accepted ADRs once 01 has named the attach intent list.
