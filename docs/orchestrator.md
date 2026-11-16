# Orchestrator

The orchestrator is the ring leader for a project. It does not write code. It decides what runs, where, and in what order, across every machine that has the repo.

## Ordering

A session declares the paths it will touch. The orchestrator holds the map. Two sessions that overlap on a path do not run at the same time. A change that rewrites a foundation blocks the work that depends on it. Parallelism is the default only when the paths do not intersect.

The orchestrator can hold a ready session until a predecessor lands. Starting the second piece early is often slower, because the merge cost exceeds the wait. The decision is recorded. The panel shows the queue, the holds, and the reason.

## Across machines

A session can run on any machine that has the checkout and the environment. The orchestrator assigns it. The window that started the work does not have to be the machine that runs it. Results come back through the backplane.

## Merge manager

Long-running agent work dies when main moves and the branch is reset. The agent loses its place, the PR is force-pushed, and the turn starts over. GitHub's merge queue is the paid feature that tests a PR against the prospective tip before it lands. Anthropic's internal system, Scion, went further: the server owns history and merges, clients stay online, and a global lock on the queue was abandoned because it does not scale to agent volume. Conflicts are fixed after the fact, by an agent, faster than a person spots them. Scion does not ship.

Rig keeps git and builds the manager the queue was reaching for.

A session works in its own worktree, on its own branch, inside its own environment. The orchestrator records the base commit. When main moves, the manager does not reset the branch. It rebases or cherry-picks only the session's commits onto the new tip, as a harness operation. Conflicts are both sides in the editor. A resolver agent, or the session itself, fixes them. The session continues from the new base. Its context is not thrown away.

Merges go through the manager, not the green button. A proposed change is tested against the current tip, or the tip plus the changes already queued. It lands only if that test passes. The agent does not merge. The manager does. No GitHub Enterprise merge queue is required.

The same manager is what the user already runs as an agent inside T3 on other repos. In Rig it is not an agent someone has to start. It is part of the orchestrator.
