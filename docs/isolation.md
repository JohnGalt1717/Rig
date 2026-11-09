# Isolation

Every worktree and every branch is an environment. Two sessions do not share a port, a database, a cache, or a process.

## No nested VM

The environment is not a lightweight VM with containers inside it. Nested virtualization is not available on macOS, and 27.3 does not add it. GPU passthrough to a VM is not the same thing.

Isolation is a network, the way Compose and Kubernetes isolate a set of containers without wrapping them in a VM. Rig creates a bridge for the session, assigns ports that do not collide, and registers DNS. Containers join that bridge. They do not join the host network.

| Host | Runtime |
| --- | --- |
| macOS | Apple containers. |
| Windows | WSL containers. The app is the Linux build through WSLg. |
| Linux | The native runtime. |

Not Docker. Not Podman. The runtime is the one Rig ships for that host.

Localhost inside a container is the container. `.local` names resolve to the host mapping Rig registered. A USB device or an emulator on one machine is a name on that bridge, reachable from a container on another machine through the network Rig built. No dev tunnel.

## Resources

The repo config names the resources: a database, Valkey, a bus, a collector. Rig starts them on the session bridge, injects the connection strings, and tears them down with the session.

A test group asks for a database. Rig cuts a sub-database on the server already running and drops it when the group ends. No container per test.

The agent asks for a rebuild, a reload, or a selective update. Rig does it. The agent does not run a container command.

## Command line

There is no raw shell. Commands go through Rig's proxy. On Windows the proxy runs them in the WSL distro. The path, the tools, and the scripts are Linux. Nothing speaks PowerShell.

## Across machines

A session's containers can be on a different machine from the window. The backplane forwards the intent. The host with the bridge applies it. The first version works with one machine. Adding a second does not change the interface.
