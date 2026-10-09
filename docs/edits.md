# Edits

An edit goes through the harness. The file explorer selects the file the agent is writing, and the editor can open it while the write is in progress.

Each session keeps its own changeset: the files that session touched, the diff against the base, and whether the file is still dirty. The panel is that list, the way the source-control view is in an editor, scoped to the session rather than to every dirty file in the tree. Another session's edits are not in it.

Generated files stay out of the changeset unless the user asks. The language pack names them. A lockfile shows as a summary — added, removed, bumped — not as the raw file.

Commit stages the session changeset. Before the commit the harness scans the diff for values it injected. A hit blocks the commit.
