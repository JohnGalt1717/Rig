# Review and source control

Source control is a set of agents the repo ships, not a raw git tool. Pull, push, commit, merge, pull request, and checks each have a skill. The repo assigns the harness those agents run under: Grok Build, Codex, Copilot. The skill is the same either way. The agent asks the harness. The harness holds the account and renders the result in the app.

Review is a choice on the repo, set in the setup UX: the internal review agent, GitHub Copilot's online review, or another harness that can produce a review. More than one can be on. They do not get separate panels.

Whatever produces the review, the findings land in the same Review panel and in the file as a suggested edit. A Copilot review posted on the pull request is pulled in and shown as if the internal agent had written it: file, range, severity, suggestion. The row records the source, so you can see it came from Copilot. Resolving it clears the row here and on the pull request.

Instructions stack. The harness ships the baseline: the problems panel, the session changeset, and the pack's review rules. The repo can add instructions in the setup UX, and those are appended, not a replacement. A review run uses both.

A finding is a work item. The coding agent that picks it up is tagged on the row and on the file. Clicking the tag opens that agent: what it loaded, which finding it is on, and the edit it is making. The internal review agent can re-check. Copilot's follow-up, if it is enabled, comes back through the same panel.
