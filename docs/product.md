# Product

Rig is a cross-platform harness for coding agents. The user clones a repository, runs `/init`, and the session is scoped, tooled, and able to edit, test, and review. Direct editing is secondary. The agent does the work. The user sees the diff, the diagnostics, and why the harness loaded what it loaded.

## Sessions

A session starts in a directory and is scoped by that directory plus the work. The harness resolves the git root, loads the single `.agents/` there, and applies globs. Several sessions run at once. Each can be a tab or a popped-out window. A home page lists everything running, on this machine and on attached hosts.

The host is the machine with the checkout. A window on another machine attaches and sends intents: prompt, approve, deny, open file, comment on a region. The host applies them and streams events back. If the host is asleep, the session is down.

## Chat and files

Chat is the primary surface. A file tree, equivalent in job to the VS Code explorer, sits beside it. Files open in the main area and in a right-hand pane. The editor is Monaco embedded in Flutter, with the language pack's language server for highlighting, diagnostics, and go-to-definition. The problems list is those diagnostics, not a second IDE.

## What the harness injects

For a matched path the harness injects the winning agent, matching behavior and knowledge, hooks the runner executes, the language pack, and credential schema names. Values are injected on the host. The transcript is redacted before it is stored. The ACP panel shows what loaded and why, including files that did not load.

## Git and review

Git identity comes from a harness key in `.git/config`, falling back to `user.email`. Commits and pull requests go through that account. Agents do not get a raw GitHub MCP. Review agents run inside the app against the diff, and the git layer posts the review to the pull request.

## Init

`/init` reads the language packs, proposes prerequisites, and installs declared tools per platform. Drift on a later run is shown and confirmed, not rewritten. Credentials are bring-your-own.

## End to end

Semantic tests are JSON chains the agent writes and the harness executes. Steps use stable selectors from the language pack's clicker. One runner. `e2e/` next to the app or library.

## Out of scope for the first build

Simulator and emulator capture with on-screen annotation. Cross-machine attach beyond a self-hosted relay. A hosted vault. Fulcrum identity as the key domain.
