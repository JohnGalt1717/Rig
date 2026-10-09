# Architecture

| Process | Runs where | Owns |
| --- | --- | --- |
| Shell | Any machine, Flutter | Windows, tabs, file tree, editor, panel |
| Host | Machine with the checkout | Agent process, language server, hooks runner, keychain injection |
| Relay | Wherever the operator starts it | Device directory, pairing records, ciphertext frames |
| Agent | Child of the host | The turn. Nothing else. |

Both ends dial the relay. WebTransport does not punch through NAT. The host approves a device key once. The relay does not store the repo, the unwrapped transcript, or a credential. No prompt queue.

A personal install is an organization of one. Adding a member adds a membership. Same tables.

SQLite via Entity Framework, one file per relay. Directory and session metadata only.

MinimalWebTransport is a NuGet from its own repository. Rig does not vendor it. The session envelope, device authentication, and redaction belong to Rig.
