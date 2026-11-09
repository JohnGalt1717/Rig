# Isolation

Every worktree and every branch is an environment. Two sessions do not share a port, a database, a cache, a process, or an environment variable.

## No nested VM

The environment is not a lightweight VM with containers inside it. Nested virtualization is not available on macOS. Isolation is a network bridge per session, the way Compose isolates a set of containers.

| Host | Runtime |
| --- | --- |
| macOS | Apple containers. |
| Windows | WSL containers. The app is the Linux build through WSLg. |
| Linux | The native runtime. |

Not Docker. Not Podman.

## Environment

The repo config names the variables the code expects: where to find certs, where the data root is, which endpoint to call. Rig sets them inside the session. A second worktree gets a different root and a different value. The host environment is not inherited. A variable that would have collided is not visible across sessions.

Connection strings, ports, and paths are injected the same way. The code reads the variable. It does not read a file the agent wrote.

## Network

Rig creates a bridge for the session, assigns ports that do not collide, and registers DNS. Containers join that bridge. Localhost inside a container is the container. `.local` names resolve to the host mapping Rig registered.

A USB device or an emulator on one machine is a name on that bridge, reachable from a container on another machine through the network Rig built. No dev tunnel.

## Resources

The repo config names the resources: a database, Valkey, a bus, a collector, a reverse proxy. Rig starts them on the session bridge, injects the connection strings, and tears them down with the session.

A test group asks for a database. Rig cuts a sub-database on the server already running and drops it when the group ends.

The agent asks for a rebuild, a reload, or a selective update. Rig does it. The agent does not run a container command.

## Command line

There is no raw shell. Commands go through Rig's proxy. On Windows the proxy runs them in the WSL distro.

## Across machines

A session's containers can be on a different machine from the window. The backplane forwards the intent. The first version works with one machine. Adding a second does not change the interface.
