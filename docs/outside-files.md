# Files outside the repo

A path outside the repo is not readable until the user allows it. The request shows the path and the permission, and it blocks. The default grant is read. Write is a second prompt.

An allowed file appears in the session as a loose file, visible in the explorer and the changeset, marked as outside. Every write keeps a copy. The history stays until the user accepts the file. Accept writes the current copy out and drops the history. Decline restores the first copy and drops the grant.

The agent does not get a blanket home-directory read. A grant is that path, that session.
