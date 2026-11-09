# Isolation

Every worktree and every branch is an environment. Two sessions do not share a port, a database, a cache, or a process.

## The container

The environment is a lightweight container. Not Docker. Not Podman.

| Host | Runtime |
| --- | --- |
| macOS | Apple containers. GPU access when the OS provides it. |
| Windows | WSL containers. The app is the Linux build through WSLg. |
| Linux | The native runtime. |

The container is network-isolated. Rig builds the network: a bridge for the session, port maps that do not collide, DNS for the names the code expects. Localhost inside the container is the container. `.local` names resolve to the host mapping Rig registered.

## Resources

The repo config names the resources: a database, Valkey, a bus, a collector. Rig is the host. It starts them inside the container, injects the connection strings, and tears them down with the session.

A test group asks for a database. Rig cuts a sub-database on the server already running and drops it when the group ends. No container per test.

The agent asks the harness for a rebuild, a reload, or a selective update. The harness asks Rig. Rig does it. The agent does not run a container command.

## Devices and emulators

An emulator is a resource. An iOS simulator, an Android emulator, or a Linux desktop session runs where the hardware is and is reachable from any Rig session through the network Rig built.

A USB device attached to a machine gets a network endpoint on that machine. Rig proxies it. A session in a container on another machine reaches it by the name Rig registered. No dev tunnel. The mapping is the same on every machine running Rig.

## Across machines

A session's container can be on a different machine from the window. The backplane forwards the intent. The host with the container applies it. Machines see each other's sessions. The first version works with one machine. Adding a second does not change the interface.
