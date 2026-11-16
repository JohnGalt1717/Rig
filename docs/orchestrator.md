# Orchestrator

The orchestrator is the ring leader for a project. It is also the merge queue. It does not write product code. It decides what runs, where, in what order, and what may land, across every machine that has the repo.

It is an agent. It gets a special set of skills and MCPs that the coding sessions do not get: overlap detection on paths and symbols, effect analysis, test impact, and the merge operations. Those tools are injected only into the orchestrator. A coding session cannot call them.

## Ordering and parallelism

A session declares the paths it will touch. The orchestrator holds the map and runs the overlap tools against it. Two sessions that overlap on code, on an effect, or on a test do not run at the same time. Work that does not overlap runs in parallel.

A change that rewrites a foundation holds the work that depends on it. The orchestrator can hold a ready session until a predecessor lands. Starting the second piece early is often slower, because the merge cost exceeds the wait. The decision is recorded. The panel shows the queue, the holds, and the reason.

## Merge queue

Long-running agent work dies when main moves and the branch is reset. The agent loses its place, the PR is force-pushed, and the turn starts over. GitHub's merge queue is the paid feature that tests a PR against the prospective tip before it lands. Anthropic's internal system, Scion, went further and does not ship.

Rig keeps git. The orchestrator is the queue.

A session works in its own worktree, on its own branch, inside its own environment. The orchestrator records the base. When main moves, it uses the overlap tools to decide whether the session is affected. If it is not, the session continues. If it is, the orchestrator rebases only the session's commits onto the new tip, as a harness operation. It does not reset the branch. Conflicts are both sides in the editor. A resolver agent, or the session itself, fixes them. The session continues from the new base. Its context is not thrown away.

A proposed change is tested against the current tip, or the tip plus the changes already queued that overlap it. It lands only if that test passes. The coding agent does not merge. The orchestrator does. No GitHub Enterprise merge queue is required.

## Across machines

A session can run on any machine that has the checkout and the environment. The orchestrator assigns it. The window that started the work does not have to be the machine that runs it. Results come back through the backplane.
