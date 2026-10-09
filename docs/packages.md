# Packages

Restore is a harness tool. The language pack names the restore command. The result parses into the dashboard. The agent does not invent a restore shell line.

The package panel is the tree of direct dependencies: current, latest in range, latest major, and the advisory if one exists. The data is the public advisory feed for that ecosystem (NuGet, pub, npm). A known vulnerability is a row, severity visible, not a comment buried in a restore log.

An update is a harness operation. The agent can ask for it. The harness runs the bump, the restore, and the lockfile write, then the problems panel and the tests the metadata says to run. The panel updates. The user sees the same bump the agent requested.

The agent does not edit a lockfile by hand.
