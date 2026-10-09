# Machine config

`.prerequisites.json` is the machine contract. It lists installs, and it lists certificates: which names, which capabilities, which stores to trust. `/init` executes that file. The agent does not.

`/repair` is the same file run against a machine that already exists. It diffs the contract to what is installed, what is trusted, and what the session runtime expects, and it fixes the drift. A pull that changes the contract runs `/repair` on its own and rebuilds the projects the contract names. The panel shows what it changed. A failure is a row with a fix action, same as a restore failure.

Certificates are entries in that file, not a side script. Add and rotate are edits to the contract, then `/repair`.
