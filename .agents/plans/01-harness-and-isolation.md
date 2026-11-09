# Harness on the harnesses, and isolation

Grill this before any code.

## Decision

Rig drives the installed harnesses. Grok Build over ACP, Codex over its app-server, Claude Code over the Agent SDK. Those keep their loops. Rig owns the environment.

Each agent area gets one MCP. It replaces the defaults, exposes Rig's contracts through skills, and proxies additional MCPs the area declared. Language packs configure debugger, UI driver, coverage, and test harness. `/init` installs them. First proof is C# and Flutter.

## Isolation

No nested VM. macOS does not have it. Isolation is a network bridge per session, the way Compose isolates containers. Apple containers on macOS, WSL containers on Windows, native on Linux. No Docker, no Podman. Commands through the proxy, in WSL on Windows.

Resources start on the bridge. Test groups get sub-resources. Emulators and USB devices are names on the bridge, proxied across machines.

## Deploy

The setup is code. It generates the pipeline for the three large clouds. Language libraries that call the deploy API are later.

## Open questions

1. One MCP server per area, or one server with the area as a scope parameter?
2. Does the bridge and its containers start on session open, or on first resource request?
3. Cross-machine in the first cut, or one machine with the interface ready?
