# Isolation

Every worktree and every branch is an environment. Two sessions do not share a port, a database, a cache, a process, an environment variable, or a checkout.

## What runs inside

The environment holds the source, the build, the resources, the reverse proxy, and the agent process. Cloning the repo and running `/init` brings the whole thing up. There is no separate machine setup.

The agent runs in the container. The language server runs in the container. The build runs in the container. The Aspire-style host Rig provides runs against those containers, with one debugger attached across them.

## Environment pushed everywhere

The repo config names the variables, the ports, and the URLs the code and the tests expect. Rig assigns unique ports for the session, starts the proxy with the forwarding rules for those ports, and injects the resulting values.

The injection is not only for processes inside the container. A simulator or an app launch on the host gets the same environment. Flutter, a browser, or another pack's runner is started with the session's base URL, the proxy address, and the ports. The app talks to the worktree's services, not to whatever is on the default ports. An e2e run is pointed at those ports automatically. A second worktree gets different ports and a different proxy. The two do not collide.

Simulators stay on the host where the platform requires it: iOS, Android, and the desktop shells. They are reached by name on the session bridge, and they receive the session environment at launch. Everything else is in the environment.

## No nested VM

The environment is not a VM wrapping containers. Isolation is a network bridge per session.

| Host | Runtime |
| --- | --- |
| macOS | Apple containers. Rig builds the network isolation. GPU passthrough from 27.3 is used when the runtime exposes it. |
| Windows | WSL containers. The app is the Linux build through WSLg. |
| Linux | The native runtime. |

Not Docker. Not Podman.

## Network and resources

Rig creates a bridge, assigns non-colliding ports, and registers DNS. Containers join the bridge. Localhost inside a container is the container. `.local` names resolve to the host mapping.

Resources start on the bridge. The reverse proxy is one of them. Test groups get sub-resources. A USB device or an emulator is a name on the bridge. No dev tunnel.

The agent asks for a rebuild or a reload. Rig does it. The agent does not run a container command.

## Command line

No raw shell. Commands go through the proxy. On Windows the proxy runs them in WSL.
