# Harness on the harnesses, and isolation

Grill this before any code. It replaces the earlier provider-and-host plan.

## Decision

Rig drives the installed harnesses. Grok Build over ACP, Codex over its app-server, Claude Code over the Agent SDK. Those keep their loops. Rig owns the environment: the root MCP, the scope, the container per worktree, the resources, the network.

Least-cost routing picks the harness when the repo does not. A review uses a different harness than the author.

## Isolation

One container per worktree or branch. Apple containers on macOS, WSL containers on Windows, native on Linux. No Docker, no Podman. Network-isolated. Rig injects env, pathing, and connection strings. Resources (database, Valkey, bus) start inside the container. Test groups get sub-resources, not new containers.

Emulators and USB devices are resources, proxied across machines. Localhost and `.local` resolve inside the container to the host mapping. No dev tunnel.

## Open questions

1. Does the container start on session open, or on first resource request?
2. Is the root MCP one server with scoped tools, or one server per agent match?
3. Cross-machine in the first cut, or one machine with the interface ready?
