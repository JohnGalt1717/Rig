# Structure database

`.structure.db` at the repo root is the derived index of the tree: files, symbols, tests and their metadata, and the edges between them. It is gitignored. `/init` creates it on first run. The harness rewrites `.gitignore` so that entry, the credential files, and the local state files are present. The ignore list is deterministic. The agent does not edit it.

Updates are incremental because edits pass through the proxy. A save invalidates the files it touched and the index patches those. The agent does not rebuild the index, and two machines do not sync the file. It is host-local. Secrets never go in it.

The test list the agent queries lives here, including when a test should be run. Coverage from the last run is attached to those rows.
