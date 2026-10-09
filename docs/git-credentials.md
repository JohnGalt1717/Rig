# Git credentials

The harness ships a credential helper and installs it at `/init`. Git and `gh` both use it. The agent does not run `gh auth login` and does not see the token.

The repo setup names the account for that remote. The helper switches context per command, so a second repo on the same machine uses its own account without a global `gh` switch. Push, pull, checks, and review publication go through that context.

The helper is the only writer of the git credential store and the `gh` hosts entry on the machine. A manual login outside it is drift, shown on the next `/init`.
