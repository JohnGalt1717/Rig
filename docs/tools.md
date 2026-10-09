# Tool surface

The agent gets the editor tools and the harness contracts. It does not get a shell for these.

Editor, the set VS Code exposes to an agent: read file, list directory, file search, text search, symbol search, usages, problems, changeset, edit, create, delete, rename. Semantic search reads `.structure.db`. Usages read the graph and the language server. Problems read the panel.

Contracts already named: build, format, analyze, test, coverage, debug, drive, restore, package bump, git, review, secrets, certificates.

The commands agents still shell out for, and the contract that replaces them:

| They run | Contract |
| --- | --- |
| `curl` the API | Request against the session runtime. The harness fills the base URL and the cert. |
| `lsof`, `ss`, `netstat` | Port map for this session. |
| `docker compose ps`, `logs` | Session runtime status and logs. |
| `jq` on a file | Structured read. |
| `printenv` | Names only, from the injected set. Values stay redacted. |
| A SQL client | Query the session database. Write is a confirm. |
| `rg`, `find`, `cat` | Search and read, above. |
| `mkdir`, `rm`, `cp`, `mv` | Create, delete, rename. |

A command that matches a row is rejected and the contract is named. A command that matches none is the miss in [terminal.md](terminal.md).
