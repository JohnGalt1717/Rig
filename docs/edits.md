# Edits

An edit goes through the harness. The file explorer selects the file the agent is writing, and the editor can open it while the write is in progress.

Each session keeps its own changeset: the files that session touched, the diff against the base, and whether the file is still dirty. The panel is that list, scoped to the session rather than to every dirty file in the tree.

Every file in the explorer, the changeset, and the active-file list carries the agent that is writing it. A sub-agent is named, so a test file shows the test agent rather than the parent. Clicking the tag opens that agent's context: the globs that matched, the skills it loaded, and the tools the proxy granted. The panel already computed the match. The tag is that match, on the file.

Generated files stay out of the changeset unless the user asks. The language pack names them.

Commit stages the session changeset. Before the commit the harness scans the diff for values it injected. A hit blocks the commit.
