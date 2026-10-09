# Rig

An opinionated command surface for coding agents. Chat is primary. The harness owns scope, tools, git identity, and review. The agent does the work inside that scope.

This repository is the product. It is not a plugin for VS Code.

## Layout

Mirrors Project Fulcrum: one backend tree, one app tree, shared libraries, a single root `.agents/` contract.

| Path | What it is |
| --- | --- |
| `docs/` | Product contract. Read this before writing code. |
| `.agents/` | Agents, skills, hooks, behavior, knowledge, plans. One root. No nested copies. |
| `Api/` | .NET 11 relay and directory. SQLite and Entity Framework. |
| `Apps/rig/` | The Flutter shell. One app. |
| `Apps/shared/` | Flutter libraries shared by the shell. |
| `deploy/` | Optional compose profile. Bring-your-own credentials is the default. |

## Status

Scaffold and specification only. Grill plans in `docs/plans/` are the gate before implementation. Do not treat the docs as settled where a plan still says open.

## Read next

1. [docs/product.md](docs/product.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/plans/00-grill-index.md](docs/plans/00-grill-index.md)
