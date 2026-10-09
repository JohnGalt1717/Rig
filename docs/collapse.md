# Collapsed noise

These are the chores that currently sit outside the editor and outside the agent. Each one is a harness surface, same shape as problems and packages.

| Chore | Surface |
| --- | --- |
| Session diff | [edits.md](edits.md). The explorer follows the write. The changeset is per session. |
| Package restore, advisories, bumps | [packages.md](packages.md). |
| Lockfile review | A summary on the changeset, not the raw file. |
| Generated files | Hidden from the agent diff unless asked. The pack names the globs. |
| Dev certificates and ports | `/init` issues the local cert and the harness allocates ports. The agent does not pick a port or trust a cert by hand. |
| Commit | Stages the session changeset. A secret in the diff blocks it. |
| Conflicts | The editor shows both sides. The agent resolves through that view. Marker files are not the interface. |
| Pending migrations | A language-pack panel: status, apply, rollback. Same row shape as packages. |
| Waived tests and suppressed diagnostics | A list with the reason and the age. Silence is not a pass. |

Cloud accounts, Kubernetes, and deployed config drift are out of the first version.
