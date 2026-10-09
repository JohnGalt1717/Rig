# Dashboard

The dashboard is the runner's event stream, and, per session, the agent graph.

The graph is live. A node is an agent. An edge is the instruction that started it: the parent prompt, the flow step, or the glob fan-out that matched. The node shows what that agent is doing now. A file it is writing is the same tag the explorer shows. Clicking a node, an edge, or a file opens the detail: the instruction it received, the skills and tools it was granted, the tool call in flight, and the reasoning it has emitted. The detail updates while the turn is running. It is not a log you scroll after the fact.

The tool stream sits under the graph. Each row is a proxied call: the agent, the session, the contract it was flattened to, the upstream server, the redacted arguments, the result, and the duration. A call in flight is visible before it returns. A timeout is a killed process group. A contract violation is the upstream result that did not fit, shown next to the call.

Debug sessions, clicker actions, test runs, and coverage are the same stream filtered by contract. Opening a row jumps to the node, the flow step, the file, or the stopped frame.
