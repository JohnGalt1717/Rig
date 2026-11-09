# Rig

Read [LICENSE.md](LICENSE.md) before you use this repository. It is a modified PolyForm Strict grant: you may run it, including commercially. You may not fork it, wrap it, or ship a modified copy, paid or free. It is not an open source license. Read it carefully.

Rig is a harness for coding agents. It drives the harnesses you already have installed and logged in: Grok Build, Codex, Claude Code. Those keep their loops and their plans. Rig owns the environment they run in.

Chat is the primary surface. The agent does the work. You see the files, the diff, the diagnostics, and exactly what the harness loaded and why.

## How it drives the agents

Rig does not reimplement Grok Build, Codex, or Claude Code. It drives the copies on the machine, the same way T3 Code does.

Grok Build speaks ACP. Codex runs as its app-server. Claude Code is driven through its Agent SDK. An adapter turns each into the same events: turn started, tool called, result, done. The rest of Rig never asks which one it is.

A session can hand work to another harness. A parent on Claude can start a child on Codex, or a review on Grok Build. The child keeps its own history. The parent wakes with the result. Least-cost routing picks the harness for the job when the repo does not name one: a cheap model for a mechanical edit, a stronger one for a design, a third for an independent review.

## What Rig adds

The installed harness is good at a turn. It is not good at a monorepo.

Rig is the root MCP for every scoped area. It hands the harness the tools that area is allowed, and nothing else. Agents and agent graphs are mapped to folders by glob. A test agent on a test file does not see the deploy tools. The panel shows the match: globs, skills, and the tools the proxy granted.

Command line is locked. The harness does not get a raw shell. It gets Rig's contracts: edit, search, restore, debug, drive, container. A request that would have been `curl` or `docker` is refused and named as the contract. Processes are owned. A turn that ends without closing them is forced to answer.

Language packs configure the rest. `/init` reads the tree, installs the tools, sets up the debugger, the test harness, the clicker, code search, and the structure index. The harness receives that as the environment. It does not set it up.

## Isolation

Every worktree and every branch gets its own environment. Nothing shares a port, a database, or a cache with another.

The environment is a lightweight container, not Docker and not Podman. On macOS it is an Apple container. On Windows it is a WSL container. On Linux it is the native runtime. The container is network-isolated. Rig injects the environment variables, the pathing, and the connection strings. The harness sees a machine that was built for this checkout.

Resources are declared in the repo config, the way Aspire declares them, and Rig is the host. A database, Valkey, a bus: Rig starts them inside the container, cuts a sub-resource for a test group, and tears them down with the session. The agent asks for a rebuild or a reload. It does not run the container CLI.

Emulators and devices are resources too. An iOS simulator, an Android emulator, or a USB device attached to one machine is reachable from a session on another, through the network Rig already built. Localhost and `.local` names resolve inside the container to the host mapping. No dev tunnel.

## Any machine

Machines running Rig see each other's sessions. A window on a laptop controls a session whose container is on a desktop. The backplane is MinimalWebTransport and a Hub. Both sides connect out. The first version can run with one machine. The interface is the same when a second appears.

On Windows the host is Linux. The app is the Linux build, shown on the Windows desktop through WSLg. See [docs/windows.md](docs/windows.md).

## Plan, then execute

Work starts as a plan. Rig runs a grill: it reads the docs and the code the task touches, asks only the questions that would change the design, and writes the settled plan to `.agents/plans/`. Execution starts when that plan's open questions are empty.

## Layout

| Path | What it is |
| --- | --- |
| `LICENSE.md` | Modified PolyForm Strict. Run it, including commercially. Do not ship a modified copy. |
| `.prerequisites.json` | Machine contract. What `/init` installs. |
| `docs/` | Product contract. Start at [docs/product.md](docs/product.md). |
| `.agents/` | Agents, behavior, knowledge, plans. One per repo, at the root. |
| `Apps/rig/` | The Flutter shell. |

## Status

Specification. Implementation waits on the open questions in `.agents/plans/`. Start at [docs/product.md](docs/product.md).
