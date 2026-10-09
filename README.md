# Rig

Rig is a harness for coding agents. Chat is the primary surface. The agent does the work. You see the files, the diff, the diagnostics, and exactly what the harness loaded and why.

The agents that can edit, run, and test ship as terminals, or as guests inside an editor that was not built to scope them. Those editors hand the agent a global tool list, a global git account, and no rule for which tool is legal in which folder. Review, pull requests, and Actions happen in a browser or over a proxy API, so the screen you are on is never the place the work is happening. A new machine is a scavenger hunt: install the SDK, install the debugger, copy an env file, hope the bash hook runs on Windows.

Rig sits in front of the agents and refuses that. It is not another IDE, and it is not a plugin.

## Any machine, one backplane

The machine with the checkout is the host. The agent process, the language server, the simulator, and the injected credentials live there. Every other window is a client.

Clients and hosts dial a backplane. The backplane is a small .NET 11 service, SQLite and Entity Framework, speaking MinimalWebTransport. Both sides connect out. It is not hole punching. A personal install is an organization of one. Adding a person adds a membership. Same tables.

From any paired machine you see every session the host is running, and you control them: prompt, approve, deny, open a file, comment on a line. The host applies the intent and streams events back. If the host is asleep, that session is down. The backplane remembers which device is paired and which host owns which session. It forwards ciphertext. It does not store the repo, the transcript, or a secret.

Self-host the backplane wherever you want. A window on a laptop and a window on a desktop are the same app, talking to the same sessions.

On Windows the host is Linux. The app is the Linux build, shown on the Windows desktop through WSLg. The agent, the shell, the hooks, and the language server all run in the distro. Nothing speaks PowerShell. See [docs/windows.md](docs/windows.md).

## Plan, then execute

Work starts as a plan, not as a prompt that wanders. Rig runs a grill: it reads the docs and the code the task touches, asks only the questions that would change the design, and writes the settled plan to `.agents/plans/`. Execution starts when that plan's open questions are empty.

The plan stays linked to the session. The agent does not get to invent a second plan halfway through. A change of direction is an edit to the plan, then more work.

## Who does the work

There is one `.agents/` per repository, at the root. Nested copies are ignored.

| Directory | Role |
| --- | --- |
| `agents/` | Agent definitions. Each has globs, a priority, and the harnesses it may run under. |
| `behavior/` | Instructions mirrored to the repo path, with an optional globs array for cross-cutting rules. |
| `knowledge/` | Notes at the same relative path as the code they describe. |
| `hooks/` | Declarations. The harness runner executes them. The agent does not shell out. |
| `skills/` | Loaded only when the matched agent names them. |
| `plans/` | Settled plans. Grill writes them. Execution reads them. |

Longest matching glob wins, then priority. A tie is an error on the panel. The dispatcher hands off. It does not do the work itself.

A task can fan out. The harness starts sub-agents in two ways. An agent graph is an explicit handoff: the plan names the agents and the order, and each child reports back to the parent session. A glob fan-out is contextual: the files the task touches match other agents, and those agents run on their slice only, with their own tools and their own behavior. Neither child inherits the parent's tool list. The panel shows which agent ran, on which paths, and why.

## Languages, already chosen

A language pack owns setup, default quality hooks, the debugger, the clicker, the inspector, and the end-to-end driver for one language. The choices are already made. Flutter is driven with marionette and inspected with flutter-agent-lens. Appium is not offered unless a task asks for a non-Flutter surface. C# Aspire is restarted and rebuilt from the app, not through a raw CLI the agent can misuse. An unknown language is a pack someone wrote: tool entries, globs, and a setup script. `/init` will not guess.

End-to-end tests are JSON chains. The agent writes and repairs the chain. The harness executes it. One runner.

## The setup file

`.prerequisites.json` at the repo root is the machine contract. It is committed. It lists every tool the repo needs, with a glob for where it applies and an install for the Linux environment the host actually runs in. A language pack contributes its own entries. A repo can add more.

On Windows that environment is the WSL distro. `/init` does not install Windows packages and does not generate PowerShell. The window is Windows. The machine is Linux.

Nothing in that file is a secret, and nothing in it is specific to one person's laptop. Clone the repo onto a blank machine and the file is already there. `/init` reads it, installs what is missing, and records what it installed. The next run diffs the file against the machine and only touches what drifted. You confirm the drift. It does not rewrite a working box in silence.

That is how an agent brings a dev box up. The contract is in the repo. The user does not install SDKs, copy a dotfile, or share a machine image. If `.prerequisites.json` and the language packs are already in the tree, `/init` is the whole setup.

## Credentials

Credentials stay out of git. `credentials.schema.json` is committed: name, glob, description, when to use. The values are not. The first machine fills them once, into the Linux secret store of the distro the host runs in. After that the harness injects the matching names into the agent environment. A later machine gets the values from the store you already use, not from a Slack pin. The agent sees the description. The transcript is redacted before it is stored.

GitHub is the remote, not the vault. An `openbao` profile in `deploy/docker-compose.yml` can start OpenBao in dev mode. It is off unless you select it, and it is a stand-in, not the hosted store.

## GitHub, on this screen

GitHub is built in. GitLab comes later, behind the same UI.

The harness uses the credentials declared for the repo, on the git identity it wrote at `/init`, and talks to GitHub itself. Pull requests, review comments, checks, and Actions runs are rendered in the app, on the session that produced them. A review agent writes the review against the diff already on screen. The comment appears in the app and on the pull request, because that is where other people read it. You do not alt-tab to github.com, and the agent does not drive GitHub through a generic proxy the way an editor extension does. Source control, the checks, and the review thread are the same surface as the chat.

The agent does not get a raw GitHub tool. It asks the harness. The harness is what holds the account.

## Standards, extended where they break

Rig uses the standards that already exist. Agents speak ACP. Tools speak MCP. Skills are skills. The gap is everything those standards leave to the client.

The harness is that client, and it is opinionated. Scope is a glob, not whatever directory the process started in. Hooks are declared and run by the harness. Because the Windows host is Linux, a bash hook is bash, and the agent is not asked to know which shell the desktop uses. Credentials are injected, not dropped in a file the agent can cat. A tool not in the matched set is not callable. The panel shows the match. Where a standard is silent or wrong, Rig extends it in the repo contract instead of waiting for the next spec revision.

## Layout

| Path | What it is |
| --- | --- |
| `.prerequisites.json` | Machine contract. What `/init` installs, per glob, into the Linux host. |
| `credentials.schema.json` | Credential names and where they apply. Values are not committed. |
| `docs/` | Product contract, decisions, and the grill plans that gate implementation. |
| `.agents/` | The root contract above, including `plans/`. |
| `Api/` | Backplane, data model, tests. |
| `Apps/rig/` | The Flutter shell. One app. Linux build, shown on Windows through WSLg. |
| `Apps/shared/` | Flutter libraries. |
| `deploy/` | Compose file. Backplane profile, and an opt-in OpenBao profile. |

Direct editing is for review. The shell is Flutter. The editor is Monaco with the language pack's language server. The diff sits next to the chat that produced it.

## Status

Specification and scaffold. Implementation waits on the open questions in `docs/plans/`. Start at [docs/product.md](docs/product.md) and [docs/plans/00-grill-index.md](docs/plans/00-grill-index.md).
