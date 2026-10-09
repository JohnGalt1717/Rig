# Packages

Restore is a harness tool. The language pack names the restore command. The result parses into the dashboard. The agent does not invent a restore shell line.

A pull that changes a package file or a lockfile triggers restore on its own. The harness diffs the incoming files, restores, and reports what failed to the user and to the session. A row with a fix action hands that failure to the agent. The agent does not notice the drift by reading the lockfile.

The package panel is the tree of direct dependencies: current, latest in range, latest major, and the advisory if one exists. The data is the public advisory feed for that ecosystem (NuGet, pub, npm). A known vulnerability is a row, severity visible, not a comment buried in a restore log.

An update is a harness operation. The agent can ask for it. The harness runs the bump, the restore, and the lockfile write, then the problems panel and the tests the metadata says to run. The panel updates. The user sees the same bump the agent requested.

The agent does not edit a lockfile by hand. The changeset shows the lockfile as a summary: added, removed, bumped.
