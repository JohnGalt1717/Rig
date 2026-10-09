# Tool surface

The agent gets contracts. A shell command that duplicates one is refused. The refusal names the contract. The call shows on the panel the contract owns.

Editor: read file, list directory, file search, text search, symbol search, usages, problems, changeset, edit, create, delete, rename, touch. Semantic search reads `.structure.db`. Usages read the graph and the language server. Problems read the panel. `rg`, `find`, `cat`, `mkdir`, `rm`, `cp`, `mv`, and `touch` are these, and the shell form is refused.

Request: `curl` and `wget` are refused. The agent calls the request contract. The harness fills the base URL, the cert, and the session. The exchange shows in the UI.

Browser: no raw browser, no Playwright binary the agent starts. The embedded browser is the only one. The agent gets the DOM, the accessibility tree, a screenshot, and the drive actions. The window shows the page the agent is on.

Ports: `lsof`, `ss`, and `netstat` are refused. The port panel lists what this session owns, the way the editor shows ports. The agent reads that panel.

Structured read: `jq` is refused. The agent asks for a path in a JSON or YAML file and gets the node.

Environment: `printenv` and `env` are refused. The agent gets the injected names. Values stay redacted.

Database: a SQL client is refused. The agent queries the session database through the contract. A write confirms.

Scripts: a Python, JavaScript, or shell file the agent writes in order to call these is refused. A script already in the repo, named by the contract as a utility, is allowed, and it runs through the runner.

Contracts already named: build, format, analyze, test, coverage, debug, drive, restore, package bump, git, review, secrets, certificates, containers.
