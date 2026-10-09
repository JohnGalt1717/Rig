# Logs

A cheap agent watches the session logs. It does not edit. It pulls the lines that matter, keeps a running analysis, and pushes a finding to the session when a pattern breaks: an exception, a retry storm, a trace that started and did not finish. Other agents receive that finding as an event. They do not tail the log.

The logs tab is per debug session. A launch group shows each member. Where the runtime emits OpenTelemetry, the tab is the trace, not the text: the client span, the API span, and the downstream call on one trace id. Flutter and the backend share that id when the pack propagates it. The agent asks for the trace. It does not grep twelve consoles to build the causal chain.

The log agent is a node on the session graph. Clicking it shows what it has concluded and the lines it used.
