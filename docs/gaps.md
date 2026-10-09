# Gaps

The panels cover the editor. These are the failures that still get through.

## Done is a claim

Agents report a task finished without running the check. A turn cannot close done unless the harness agrees: problems clean for the dirty set, the tests the metadata named have run, and the drive contract passed if a UI file changed. The agent does not get to say verified.

## A session is not a checkout

A worktree stops two agents editing one file. It does not stop them sharing a port, a database, a migration, or a `node_modules`. A session gets a runtime: its own ports, its own database, its own compose project. The drive contract points at that runtime. Reusing another session's server is a harness error.

## Production is not a credential the agent can see

A token with a production scope is not injected into an agent session. Destructive calls (drop, delete volume, force push) require the environment class on the credential and a confirm. Silence is not confirm.

## A dropped turn resumes

The plan, the changeset, and the event log are the checkpoint. A disconnect does not restart the task. The next turn is handed the open findings and the dirty set.

## Compaction does not eat the plan

The model context can be summarized. The plan, the open review rows, and the dirty set stay outside it. The harness re-injects them. The agent does not reconstruct the task from memory.

## A risky call has a snapshot

Before a command that can overwrite the tree, the harness snapshots the session changeset. A bad write restores from that, not from a transcript.

## Flakes are data

`.structure.db` records a test that failed, passed on rerun, and the count. The harness does not hand a known flake to the agent as a defect to edit away.

## Two agents, one contract

If a session changes a public type, the impact query runs before done. Callers outside the changeset are findings. The agent does not discover the break from a later build on another machine.
