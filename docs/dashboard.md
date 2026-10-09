# Dashboard

The dashboard is the runner's event stream, not a log viewer.

Each row is a proxied call: the agent, the session, the contract it was flattened to, the upstream server, the redacted arguments, the result, and the duration. A call in flight is visible before it returns. A timeout is a killed process group, shown as such. A contract violation is the upstream result that did not fit the Rig shape, shown next to the call so you can see what the tool did wrong.

Debug sessions, clicker actions, test runs, and coverage are the same stream filtered by contract. Opening a row jumps to the flow step, the file, or the stopped frame. The agent does not get a private channel around this view.
