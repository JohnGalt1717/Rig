# Runner

No tool the agent can call is direct. Bash, MCP servers, debuggers, clickers, and test runners are started by the harness runner. The agent asks. The runner executes.

Every call carries a timeout. A missing timeout is a rejection, not a default of infinite. On timeout the runner kills the process group, not the process. Children die with the parent. Session end kills every group that session started. A later `/init` or a rebuild does the same for the groups it owns.

The runner records the command, the cwd, the exit, the duration, and the tail of stdout and stderr. The panel shows what is running. A flow run is that log grouped by step.

Language-pack MCPs are registered with the runner, not with the agent. The agent receives the proxied tool list for the matched glob. A server that is not in that list is not callable, even if it is installed.
