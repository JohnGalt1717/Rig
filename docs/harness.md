# The harness on the harnesses

Rig drives the harnesses installed on the machine. It does not replace their loops.

## Adapters

| Harness | How Rig drives it |
| --- | --- |
| Grok Build | ACP. The installed binary, already logged in. |
| Codex | `codex app-server`. Program to program. |
| Claude Code | Claude Agent SDK. The installed login. |

An adapter emits the same events: turn, tool call, result, done, error. A new harness is a new adapter. The rest of Rig does not change.

The harness keeps its plan, its subagents, and its skills. Rig does not strip them. Rig adds a root MCP that is the only MCP the harness sees for the scoped area. That MCP is Rig's contracts: the editor, the debugger, the test runner, the container, the secret proxy, the structure index. The harness's own tools that would escape the scope are not offered.

## Scoping

One `.agents/` at the repo root. Agents declare globs. A file matches an agent. That agent gets the tools and the skills named for it, and the behavior and knowledge for that path. A child agent does not inherit the parent's tool list.

An agent graph is explicit: the plan names the agents and the order. A glob fan-out is implicit: the files the task touches match other agents, and those run on their slice. The panel shows which agent, on which paths, and why.

## Least cost

When the repo does not name a harness, Rig picks. A mechanical edit goes to the cheap model. A design or a hard bug goes to the strong one. A review goes to a different harness than the one that wrote the code. The choice is recorded on the turn. The user can pin a harness per agent or per repo.

## What the harness does not get

A raw shell. A raw container CLI. A raw cloud CLI. Credentials. A tool outside its glob. Those are refused, and the refusal names the contract.
