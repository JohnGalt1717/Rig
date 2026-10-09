# Containers

Docker commands are refused. So are `podman`, `nerdctl`, and the Apple container CLI. The agent talks to the container panel.

The panel lists what belongs to the repo: the compose project, the session runtime, images it built, ports it published. The engine underneath is whichever one the machine has. Docker, Podman, Apple containers, and the WSL engine are the same rows. The pack names the engine at `/init`. The agent does not.

Start, stop, rebuild, logs, and exec go through the panel. The GUI shows the call as it happens. Logs from a container feed the log agent. A container the session started dies with the session.
