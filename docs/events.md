# Events

A tool call is a request. It is not a wait. The runner accepts it, starts the process group, and returns a handle. The agent may end the turn. The harness wakes it when the handle resolves, or when a hook says the outside world changed.

GitHub is the obvious case. A pull request, a review, and an Actions run are not things the agent polls. The harness opens them, subscribes, and pushes the result into the session: checks finished, a review comment landed, the run failed. The agent is woken with that event. It can end the turn and be woken later, or keep working on something else. The same shape covers a debug session that has not stopped, a test run, and a deploy.

The runner also pushes while a process is still alive. Past the sliding timeout it asks the agent, in the session, whether the process is still valid. The agent answers continue, with a reason, or kill. Silence is not continue. No answer before the grace ends and the process group dies.

Shutdown is the same question. Session end, rebuild, and `/init` drift do not kill under the agent. The harness lists the live groups and requires an answer: shut down, or keep, with a reason. No answer, and the groups die. A leaked process is a missed answer, which the dashboard shows.

Known tools are flattened to the Rig contract and treated as this request-and-event shape. An MCP the pack does not care about is still proxied. The runner logs its timing, builds a sliding timeout from those timings, and still requires the shutdown answer. It is never a raw server the agent holds open.
