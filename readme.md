# Rig

Rig is a harness for coding agents. Chat is the primary surface. The agent does the work. You see the files, the diff, the diagnostics, and exactly what the harness loaded and why.

It exists because the current tools split the job badly. The agents that can actually edit, run, and test (Grok Build, Codex, Copilot, and the rest) ship as terminals or as guests inside an editor that was not built to scope them. Cursor and VS Code give you a file tree and a debugger, then hand the agent a global tool list, a global GitHub account, and no rule for which MCP is legal in which folder. GitHub will not give a cloned repo its secrets back. Actions secrets are write-only. The practical result is a `.env` in Slack, a password manager someone forgot to share, or a workflow that hands the decryption key to whoever can run it.

Rig is the thing that sits in front of those agents and refuses that. It is not another IDE, and it is not a plugin.

## What you get

You clone a repository and run `/init`. The harness reads one `.agents/` at the git root, matches the path you started in against globs, and starts the winning agent with only the tools, hooks, behavior, and knowledge that matched. A panel shows each match and each file that did not load. Several sessions run at once, as tabs or as their own windows. A home page lists what is running.

The machine with the checkout is the host. The agent process, the language server, the simulator, and the credentials live there. A window on another machine attaches through a relay and sends intents: prompt, approve, deny, open a file, comment on a line. The host applies them. If the host is asleep, the session is down. The relay forwards ciphertext and remembers which device is paired. It does not store the repo, the transcript, or a secret.

Direct editing is there for review, not for living in. The shell is Flutter. The editor is Monaco with the language pack's language server, so highlighting, diagnostics, and go-to-definition work. The diff sits next to the chat that produced it. A comment on a line goes back to the agent. A review agent writes the review, and the git layer posts it to the pull request, because that is where other people read it.

## How a session is scoped

There is one `.agents/` per repository, at the root. Nested copies are ignored.

| Directory | Role |
| --- | --- |
| `agents/` | Agent definitions. Each has globs, a priority, and the harnesses it may run under. |
| `behavior/` | Instructions mirrored to the repo path, with an optional globs array for cross-cutting rules. |
| `knowledge/` | OKF notes at the same relative path as the code they describe. |
| `hooks/` | Declarations. The harness runner executes them. The agent does not shell out. |
| `skills/` | Loaded only when the matched agent names them. |

Longest matching glob wins, then priority. A tie is an error on the panel. The dispatcher hands off. It does not do the work itself.

Language packs decide the rest. A pack owns setup, default quality hooks, the debugger, the clicker, the inspector, and the end-to-end driver for one language. Flutter uses marionette to drive the app and flutter-agent-lens to inspect it. Appium is not offered unless a task asks for a non-Flutter surface, so the agent cannot grab the wrong tool. C# Aspire is controlled from the app, including restarts and resource rebuilds, not through a raw CLI the agent can misuse. End-to-end tests are JSON chains the agent writes and the harness executes. The agent does not improvise the clicks at runtime.

## Credentials

Bring your own, for now. The schema is committed (`credentials.schema.json`: name, glob, description, when to use). The values are not. `/init` asks you to fill them once. The harness stores them in the OS keychain and injects the matching names into the agent environment. The agent sees the description. The transcript is redacted before it is stored.

GitHub is the remote, not the vault. A `vault` profile in `deploy/docker-compose.yml` can start a local Hashicorp Vault in dev mode. It is off unless you select it, and it is a stand-in, not the product.

## Relay

The backend is a small .NET 11 service using SQLite and Entity Framework. A personal install is an organization of one. Adding a person adds a membership. Same tables.

Transport is MinimalWebTransport, extracted from Project Fulcrum into its own repository and consumed as a NuGet package. Both sides dial the relay. This is not peer-to-peer hole punching. Self-host it wherever you want. A hosted tier, if it ever exists, runs the same binary and still cannot read session contents.

## Repository layout

| Path | What it is |
| --- | --- |
| `docs/` | Product contract, ADRs, and the grill plans that gate implementation. |
| `.agents/` | The root contract above. |
| `Api/` | Relay, EF model, tests. Aspire app host when that cut starts. |
| `Apps/rig/` | The Flutter shell. One app. |
| `Apps/shared/` | Flutter libraries. |
| `deploy/` | Compose file. Relay profile, and an opt-in vault profile. |

The shape follows Project Fulcrum, with one app instead of many, and without nested `.agents/` directories.

## Status

Specification and scaffold. Implementation waits on the open questions in `docs/plans/`. Start at [docs/product.md](docs/product.md) and [docs/plans/00-grill-index.md](docs/plans/00-grill-index.md).
