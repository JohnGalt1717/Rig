# Extensions

The harness is the app host for the session, the way Aspire is the app host for a set of resources. It starts what the repo needs, names the ports, wires the traces, and shows the lot in one dashboard. An extension is a resource kind. The agent sees the contract. The panel shows the call.

`/init` loads the extensions the repo declares, and it detects the ones the tree implies. A pull that adds a declaration runs `/repair` and loads the new one. An extension that is not loaded is not callable. The agent does not get a raw CLI for it.

| Extension | Detected from | What the host does |
| --- | --- | --- |
| Source control | a git remote | Commit, pull, push, merge, through the credential helper. |
| Pull requests | GitHub on that remote | Open, review, comment. GitLab is the same contract later. |
| Checks | `.github/workflows` | Run status and log. A finished run is an event. Watching, not deploying. |
| Containers | `compose.yaml`, a Dockerfile | Start the session runtime. Engine is Docker, Podman, Apple containers, or WSL. |
| Language pack | `*.sln`, `pubspec.yaml`, `package.json` | Analyze, build, test, debug, format. |
| Packages | the lockfile next to those | Restore, advisory, bump. |
| Secrets | `credentials.schema.json` | Inject names and files into the session. |
| Certificates | entries in the machine contract | Issue and trust, then hand the cert to the session. |
| Database | a connection the runtime needs | Start it, migrate, query. |
| Traces | an OpenTelemetry exporter | One trace across the session's resources. |
| Browser | a UI project | Embedded browser and the drive contract. |
| Simulators | a mobile target in the pack | Boot, install, drive. |
| API contract | `openapi.yaml` or the equivalent | Routes linked to client calls in `.structure.db`. |

Deploy and the cloud account that would receive it are out. Checks are read. Nothing in the first version ships a build anywhere.
