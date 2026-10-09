# Terminal

A terminal command is a miss, and for the commands in [tools.md](tools.md) it is a refusal. `curl`, `wget`, `lsof`, `ss`, `jq`, `printenv`, `rg`, `cat`, `mkdir`, `rm`, `mv`, `touch`, `docker`, `podman`, and a script the agent just wrote are not run. The runner returns the contract that owns the job.

A command that matches no contract still goes through the runner. It carries a timeout. The process group dies on timeout, on session end, and on no answer. A cheap model classifies it before it runs: read, write-local, network, destroy. Destroy does not run. The harness asks the user, with the risk named. Silence is not approval.

The dashboard counts every refusal and every command that still ran. A high count is a missing contract, not an agent to scold. Production credentials are not in the agent environment. Cloud accounts get the same gate later.
