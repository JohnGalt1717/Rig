# Issues

An issue is a resource, like a container. GitHub Issues is the first tracker. Linear and Jira are the same contract later. The agent does not get the tracker's API.

A fix does not start on the code. It starts on a plan. The plan opens with the root cause, then the execution steps. Where the cause or the approach is not settled, the grill runs and the open questions have to be empty before execution. The plan is the file in `.agents/plans/` for that issue.

The plan is committed on the branch. The pull request description is that file, plus a running note of what changed from the plan and what the work actually found. The note updates as the session learns. The agent does not write a separate summary.

Before squash or merge, the harness takes the plan off the branch. The file is stored on the closed ticket, with the root cause, the execution, and the drift note. The merge does not contain it. The repo is clean. The ticket holds the history.

No plan, no branch. A ticket that is not a code change does not get one.
