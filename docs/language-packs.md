# Language packs

A pack owns setup, default hooks, the debugger, the clicker, the inspector, the e2e driver, and how the session environment is injected at launch.

The first proof is C# and Flutter. React Native, UWP, Uno, Angular, and Next.js are later packs on the same contracts. Each declares how it receives the session ports, the proxy URL, and the other variables: environment, generated config, or launch arguments. The session assigns the ports. The pack consumes them. Port collisions are not the pack's problem.

Dart / Flutter: marionette unless the schema names flutter-skill. Inspector is flutter-agent-lens. Appium is absent unless a task asks for a non-Flutter surface.

C#: test runner via the harness. Aspire control is in-app, not a raw CLI.

E2E is JSON steps. The harness executes. The agent authors. YAML is not the format.
