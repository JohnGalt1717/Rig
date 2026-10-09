# Review and source control

Source control is a set of agents the repo ships, not a raw git tool. Pull, push, commit, merge, pull request, and checks each have a skill. The repo assigns the harness those agents run under: Grok Build, Codex, Copilot. The skill is the same either way. The agent asks the harness. The harness holds the account and renders the result in the app.

Review runs locally. The review agent reads the session changeset and the problems panel, and writes findings into a Review panel: file, range, severity, and the suggested edit. The suggestion shows in the file, the way an inline review comment does. It also publishes to the pull request, because that is where other people read it.

A finding is a work item. The coding agent that picks it up is tagged on the row and on the file. Clicking the tag opens that agent: what it loaded, which finding it is on, and the edit it is making. Resolving the finding clears the row. The review agent can re-check. It does not run inside GitHub.
