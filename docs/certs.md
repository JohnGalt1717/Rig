# Certificates

Every session environment gets a certificate the apps and the backends trust. `/init` creates a local CA on the machine if one does not exist, and trusts it.

On macOS the CA goes into the system keychain. On Windows it goes into the distro trust store and the Windows store, so the browser on the desktop accepts it. On Linux it goes into the system store. A container in a session trusts the CA because Rig mounts the trust bundle into it. The app and the backend inside that container accept the cert without a warning and without a per-app exception.

A new machine runs `/init` and gets its own CA. A session on that machine issues certs from it. Certs are not copied between machines. Add, rotate, and remove are harness commands. The agent does not run `mkcert` or a language-specific cert tool.

An untrusted cert at launch is an init failure, shown before the agent begins.
