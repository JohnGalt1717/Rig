# Runner

No MCP the agent can call is the upstream server. Every server is registered with the harness and exposed as a proxy. The agent receives the proxied tool list for the matched glob. A server that is not in that list is not callable, even if it is installed on the machine.

A call is a request that returns a handle. The agent does not block the turn on it. Completion, a GitHub check, a review comment, and a still-running process past its sliding timeout are events pushed into the session. See [events.md](events.md).

The proxy flattens a known tool to the Rig contract for that kind. A debugger is the debug contract. A clicker is the clicker contract. Coverage, the test harness, the inspector, and git are the same idea. An MCP the pack does not care about is still proxied: timing is logged, a sliding timeout is computed from those timings, and shutdown still requires an answer. The agent never holds the upstream process.

Every call carries a timeout, or inherits the sliding one the runner has measured. On timeout the runner asks the agent if the process is still valid. Continue requires a reason. No answer kills the process group. Session end asks the same question across every live group. Silence kills them.

The dashboard is that stream, live. Tool, contract, session, handle, redacted arguments, result, duration, and the shutdown answer. A contract violation is the upstream result that did not fit, shown next to the call.
