# Terminal

A terminal command is a miss. The agent should have used a contract: build, restore, test, format, debug, drive, git, secrets. Writing a Python or JavaScript script to do what a contract already does is the same miss. The dashboard counts both.

The proxy still allows a command, because a pack cannot cover every tool on day one. Every command goes through the runner. It carries a timeout. The process group dies on timeout, on session end, and on no answer.

A cheap model reads the command before it runs and classifies the damage: read, write-local, network, destroy. Destroy covers drop, delete-volume, force-push, recursive delete outside the session tree, and anything aimed at a production credential. A destroy classification does not run. The harness asks the user, with the risk the model named. Silence is not approval. Production credentials are not in the agent environment in the first place.

Cloud accounts get the same gate later, when that tooling exists. The classifier and the confirm are the same ones.
