# Isolation

Every worktree and every branch is an environment. Two sessions do not share a port, a database, a cache, a process, an environment variable, or a checkout.

## What runs inside

The environment holds the source, the build, the resources, and the agent process. Cloning the repo and running `/init` brings the whole thing up. There is no separate machine setup.

The agent runs in the container. The language server runs in the container. The build runs in the container, the way a dev container builds inside the environment instead of on the host. The Aspire-style host Rig provides runs against those containers, with one debugger attached across them.

Simulators stay on the host where the platform requires it: iOS, Android, and the desktop shells. They are reached by name on the session bridge. Everything else is in the environment.

## No nested VM

The environment is not a VM wrapping containers. Nested virtualization is not the plan. Isolation is a network bridge per session.

| Host | Runtime |
| --- | --- |
| macOS | Apple containers. Rig builds the network isolation. GPU passthrough from 27.3 is used when the runtime exposes it. |
| Windows | WSL containers. The app is the Linux build through WSLg. |
| Linux | The native runtime. |

Not Docker. Not Podman.

## Environment variables

The repo config names the variables the code expects: data roots, cert locations, endpoints. Rig sets them inside the session. A second worktree gets different values. The host environment is not inherited.

## Network and resources

Rig creates a bridge, assigns non-colliding ports, and registers DNS. Containers join the bridge. Localhost inside a container is the container. `.local` names resolve to the host mapping.

Resources (database, Valkey, bus, collector, reverse proxy) start on the bridge. Test groups get sub-resources. A USB device or an emulator is a name on the bridge, reachable from any machine running Rig. No dev tunnel.

The agent asks for a rebuild or a reload. Rig does it. The agent does not run a container command.

## Command line

No raw shell. Commands go through the proxy. On Windows the proxy runs them in WSL.
