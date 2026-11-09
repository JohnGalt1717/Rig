# Containers

The environment is a lightweight container per worktree or branch. Docker commands are refused. So are `podman`, `nerdctl`, and the Apple container CLI. The agent talks to Rig.

| Host | Runtime |
| --- | --- |
| macOS | Apple containers. |
| Windows | WSL containers. |
| Linux | The native runtime. |

Not Docker. Not Podman. The runtime is the one Rig ships for that host.

The container is network-isolated. Rig builds the network, the port maps, and the DNS. Resources named in the repo config start inside it. Connection strings are injected. A container the session started dies with the session.

The panel lists the session's containers, their resources, their ports, and their logs. Start, stop, rebuild, and logs go through the panel. The agent asks for a rebuild or a reload. It does not run a container command.

See [isolation.md](isolation.md).
