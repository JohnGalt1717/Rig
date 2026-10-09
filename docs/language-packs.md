# Language packs

A pack owns setup, default hooks, the debugger MCP, the clicker, the inspector, and the e2e driver.

Dart / Flutter: marionette unless the schema names flutter-skill. Inspector is flutter-agent-lens. Appium is absent unless a task asks for a non-Flutter surface.

C#: test runner via the harness. Aspire control is in-app, not a raw CLI MCP.

E2E is JSON steps. The harness executes. The agent authors. YAML is not the format.
