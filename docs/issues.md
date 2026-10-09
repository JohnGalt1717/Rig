# Issues

An issue is a resource, like a container. GitHub Issues is the first tracker. Linear and Jira are the same contract later.

The agent reaches the tracker only through the contract. `gh`, `git` against the issue remote, the tracker's CLI, `curl`, `wget`, and the request proxy are refused when the target is the tracker. The refusal names the contract. There is no second path.

Auth is per repo. GitHub uses the account the credential helper already holds for that remote. Another tracker gets a login prompt on first use, stored against this repo only, and injected into the call. The agent does not see the token, and a login for one repo is not offered to another.

A fix does not start on the code. It starts on a plan. The plan opens with the root cause, then the execution steps. Where the cause or the approach is not settled, the grill runs and the open questions have to be empty before execution. The plan is the file in `.agents/plans/` for that issue.

The plan is committed on the branch. The pull request description is that file, plus a running note of what changed from the plan and what the work actually found. The note updates as the session learns. The agent does not write a separate summary.

The ticket stores that record as fields, not as a paragraph in the body. On first connect the harness creates them if the tracker allows it: root cause, plan, unanticipated changes, and what was actually found. GitHub keeps those on the Project item for the issue, which is the only place GitHub has custom fields. Linear and Jira get them on the issue itself. A tracker that cannot hold a field gets a refused close, not a blob of markdown standing in for one.

Before squash or merge, the harness takes the plan off the branch and writes those fields. Close is refused until they are filled. The merge does not contain the plan file. The repo is clean. The ticket holds the history.

No plan, no branch. A ticket that is not a code change does not get one.
