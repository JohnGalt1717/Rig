# Structure database

`.structure.db` is the harness-owned version of what codebase-memory does today.

codebase-memory parses a repo into a local knowledge graph and lets an agent query that graph instead of grepping. tree-sitter builds the AST for a wide set of languages. A hybrid language-server pass resolves types for the languages where a name is not enough to know which method was called. Nodes are projects, packages, folders, files, types, functions, and routes. Edges are contains, defines, calls, imports, implements, and HTTP calls. The graph sits in SQLite. A watcher re-indexes changed files. The agent then asks for callers, a trace, or impact, and gets a structural answer.

That is the right shape. The part that does not fit is the same part that did not fit for the debugger: it is a separate MCP the agent starts, watches files on its own, and holds a process the harness did not spawn.

Rig keeps the graph and drops the server. `.structure.db` at the repo root is that graph. `/init` builds it the first time. After that the proxy already knows which files a session wrote, so the index patches those files. There is no second watcher. The agent queries the harness contract: search, callers, callees, trace, impact. The panel can show the same graph. A tool that works the same way — a local index, a structural query, a process of its own — is ingested the same way. Its store is not a second database the agent owns.

The file is gitignored. The harness writes that ignore entry. Two machines do not sync the file. Secrets never go in it.

The test list lives in the same graph, including when a test should be run. Coverage from the last run is attached to those rows.
