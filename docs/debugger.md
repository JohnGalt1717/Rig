# Debugger

Rig speaks DAP itself. It does not run mcpdebugger, and it does not wrap it.

DAP is the standard the language tools already speak. A language pack launches that language's adapter and Rig is the only client: Flutter's `flutter debug-adapter`, Dart's `dart debug_adapter`, netcoredbg, js-debug, debugpy. The pack does not write a debugger. It names the adapter binary, the launch shape, and the path mapping. An unknown language is a pack that supplies those, or it is not debuggable.

The session registry is the harness. One adapter process per session. One writer. The agent sees the debug contract, which is the proxy: break, step, continue, evaluate, stack, watches. A call returns a handle. A stop, a restart, and an exited process are events pushed into the session. The agent can end the turn and be woken when the debuggee stops. It does not poll.

The window subscribes to the same registry. It is not a second DAP client. Break, step, and evaluate from the window queue on the session beside the agent's calls.

A launch group is the unit on screen. Aspire is a group: the app host plus each resource that came up under the debugger. A Flutter screen and the API it calls are a group. The view lists every session, the one that is stopped, and the stack of each. Opening a frame shows the file, the locals, and the watches.

Rebuild kills the process group for that session, relaunches the adapter through the registry, and rebinds the breakpoints. The agent cannot spawn the debuggee. Shutdown asks the agent if the live groups are still valid. No answer kills them.

mcpdebugger already proved the adapter matrix and the agent-shaped breakpoint. That is the part worth reading. Its MCP server is the part that does not fit: it holds the turn, it is a second owner of the adapter, and it does not push. Rig's contract replaces it.
