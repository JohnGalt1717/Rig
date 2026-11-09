# The harness on the harnesses

Rig drives the harnesses installed on the machine. It does not replace their loops.

## Adapters

| Harness | How Rig drives it |
| --- | --- |
| Grok Build | ACP. The installed binary, already logged in. |
| Codex | `codex app-server`. Program to program. |
| Claude Code | Claude Agent SDK. The installed login. |

An adapter emits the same events. A new harness is a new adapter.

## The area MCP

Each agent area gets one MCP. That MCP is the only MCP the harness sees for that area. It replaces the defaults.

The MCP exposes Rig's contracts for the area: edit, debug, test, coverage, drive, container, secrets, structure. Skills in `.agents/skills/` are how the agent is told to call them. A skill names the contract. The agent does not get a raw tool list.

Additional MCPs the repo wants are proxied through this one. They are declared in the area, scoped by the same globs, and flattened to the area contract where a contract exists. An MCP that is not declared is not loaded. The hierarchy is the area, then the match, then the tool. The panel shows it.

## Language tooling

A language pack still configures the area. For C# and for Flutter, the first two, the pack sets up the debugger, the UI driver, code coverage, the test harness, and the problems push. `/init` installs them. The area MCP exposes them. The harness does not install them and does not call them directly.

Next.js and Vite are later packs. Same MCP, same contracts, new pack.

## Scoping and cost

One `.agents/` at the repo root. Agents declare globs. A child does not inherit the parent's tools. Least-cost routing picks the harness when the repo does not name one. A review uses a different harness than the author.

## Command line

No raw shell. The proxy runs the command, in WSL on Windows. See [isolation.md](isolation.md).
