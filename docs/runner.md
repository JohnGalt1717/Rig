# Runner

No MCP the agent can call is the upstream server. Every server is registered with the harness and exposed as a proxy. The agent receives the proxied tool list for the matched glob. A server that is not in that list is not callable, even if it is installed on the machine.

The proxy does three things the upstream server does not.

It requires a timeout on every call. A missing timeout is a rejection. On timeout or session end the runner kills the process group, so a child cannot outlive the call.

It flattens the call to the Rig contract for that kind of tool. A debugger is the debug contract, whether the upstream is mcp-debugger, netcoredbg, or the Flutter debug adapter. A clicker is the clicker contract, whether the upstream is marionette or flutter-skill. Coverage, the test harness, the inspector, and git go through the same kind of contract. The upstream shape stays behind the proxy. The agent, the flow, and the dashboard see one shape per kind of tool. A server that cannot fill the contract is a failed language pack, not a special case the agent is allowed to call raw.

It records the call as structured events, not a log line. Tool name, contract, session, flow step, arguments after redaction, result, duration, process group, and the upstream error. The dashboard is that stream, live. You see which tool the agent called, which contract it was flattened to, what came back, and where the upstream disagreed with the contract. That disagreement is how a bad MCP shows itself. The agent can propose a skill or a flow change from a failed step. The change is a diff. It is not a quiet retry.

The panel shows what is running. A flow run is the same events grouped by step. One click lays the trace on the flow.
