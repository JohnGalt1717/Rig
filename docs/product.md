# Product

Rig drives the coding harnesses already installed and logged in: Grok Build, Codex, Claude Code. Those keep their loops. Rig owns the environment they run in.

The user clones a repository, runs `/init`, and the session is scoped, tooled, isolated, and able to edit, test, and review. Direct editing is secondary. The agent does the work. The user sees the diff, the diagnostics, and why the harness loaded what it loaded.

## Sessions

A session starts in a directory and is scoped by that directory plus the work. The harness resolves the git root, loads the single `.agents/` there, and applies globs. Several sessions run at once. Each can be a tab or a popped-out window. A home page lists everything running, on this machine and on attached hosts.

Each session gets its own container. See [isolation.md](isolation.md).

The host is the machine with the checkout and the container. A window on another machine attaches and sends intents. The host applies them. If the host is asleep, the session is down.

## How the agents are driven

See [harness.md](harness.md). Grok Build over ACP, Codex over its app-server, Claude Code over the Agent SDK. An adapter emits the same events. Rig adds a root MCP that is the only MCP the scoped agent sees. Least-cost routing picks the harness when the repo does not name one.

## Chat and files

Chat is the primary surface. A file tree sits beside it. Files open in the main area and in a right-hand pane. The editor is Monaco in Flutter for the first cut, with the language pack's language server. The problems list is those diagnostics.

## What Rig injects

For a matched path: the winning agent, matching behavior and knowledge, hooks the runner executes, the language pack, and the tools the proxy granted. Values are injected into the container. The transcript is redacted. The panel shows what loaded and why.

## Git and review

Commits and pull requests go through the account the credential helper holds. Agents do not get a raw GitHub tool. Review can run on a different harness than the author. The result posts to the pull request and shows in the app.

## Init

`/init` reads the tree, installs declared tools, proposes the resources, and builds the container image for the environment. Drift on a later run is shown and confirmed.

## End to end

Semantic tests are JSON chains the agent writes and the harness executes. Steps use stable selectors from the language pack's clicker. One runner.

## Later

A hosted vault. Deploy to a real cluster from the same config. A native Flutter editor in place of Monaco.
