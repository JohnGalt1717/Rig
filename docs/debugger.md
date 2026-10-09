# Debugger

The debug UI sits on the same session the agent drives. It does not attach a second client to the adapter.

The standard underneath is DAP. mcp-debugger already turns DAP into MCP tool calls and already keeps more than one session. Rig does not hand the agent that server. The harness hosts the session registry and exposes a proxy MCP. The proxy is the only thing the agent can call. The UI subscribes to the same registry.

One adapter process per session. One writer. Events fan out to the agent and to the window. Break, step, continue, evaluate, and inspect are harness commands. The window and the agent both issue them. They queue on the session. They do not race two DAP clients.

A launch group is the unit on screen. Aspire is a group: the app host plus each resource that came up under the debugger. A Flutter screen and the API it calls are a group. The view lists every session in the group, the one that is stopped, and the stack of each. Opening a frame shows the file, the locals, and the watch list. Switching sessions does not detach the others.

Rebuild is a harness operation. It kills the process group for that session, relaunches through the registry, and rebinds the breakpoints. The agent cannot spawn the debuggee itself. An orphaned debuggee is a bug in the proxy, because the proxy is the parent.

The proxy rejects a call with no timeout. A stopped session the user has opened is exempt from the agent timeout until the user continues or the user timeout fires. The agent does not get to hold a breakpoint forever.
