# Extensions

An extension flattens one outside system to a contract. The agent sees the contract. The panel shows the call. `/init` loads the extensions the repo declares, and it detects the ones the tree implies. A pull that adds a declaration runs `/repair` and loads the new one.

Declared in the machine contract, or detected:

| Extension | Detected from | Contract |
| --- | --- | --- |
| Source control | a git remote | Commit, pull, push, merge, through the credential helper. |
| Pull requests | GitHub on that remote | Open, review, comment. GitLab is the same contract later. |
| Checks | `.github/workflows` | Run, status, log. A finished run is an event. |
| Containers | `compose.yaml`, a Dockerfile | The container panel. Engine is Docker, Podman, Apple containers, or WSL. |
| Language pack | `*.sln`, `pubspec.yaml`, `package.json` | Analyze, build, test, debug, format. |
| Packages | the lockfile next to those | Restore, advisory, bump. |
| Secrets | `credentials.schema.json` | Read names, inject files. |
| Certificates | certificate entries in the machine contract | Issue, trust, rotate. |
| Database | a connection in the session runtime | Query, migration status, apply, rollback. |
| Traces | an OpenTelemetry exporter in the runtime | The logs tab as a trace. |
| Browser | a UI project | The embedded browser and the drive contract. |
| Simulators | a mobile target in the language pack | Boot, install, drive. |
| API contract | `openapi.yaml` or the equivalent | Routes linked to the client calls in `.structure.db`. |

Cloud accounts are the same shape later: detect what the repo deploys to, map the resources, gate the dangerous calls. Not in the first version.

An extension that is not loaded is not callable. The agent does not get a raw CLI for it.
