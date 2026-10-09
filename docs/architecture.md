# Architecture

## Processes

| Process | Runs where | Owns |
| --- | --- | --- |
| Shell | Any machine, Flutter | Windows, tabs, file tree, editor, panel |
| Host | Machine with the checkout | Agent process, language server, hooks runner, keychain injection, simulator |
| Backplane | Wherever the operator starts it | Device directory, pairing records, ciphertext frames |
| Agent | Child of the host | The turn. Nothing else. |

The shell on the host machine may be in-process with the host. A remote shell is only a client.

## Attach

Both ends dial the backplane. WebTransport does not punch through NAT, and Rig does not pretend it does. Frames are mutually authenticated. The host approves a device key once and can revoke it. The backplane stores device public keys, which host is online, which session id it owns, and the pairing record. It does not store the repo, the unwrapped transcript, or a credential.

Intents flow window to host. Events flow host to window. No queue on the backplane. No second writer.

## Personal and organization

The same tables. A personal install is an organization of one, created at first run from the signed-in identity. Adding a member promotes nothing. It adds a membership. Session attach is allowed if the device is paired and the membership covers the repo.

## State

SQLite via Entity Framework, file beside the backplane process. One database per backplane. This is directory and session-metadata state, not source and not secrets. See [backend.md](backend.md).

## Trust boundaries

- Agent tool calls stop at the harness. A tool not in the matched mcp set is not callable.
- Credential plaintext exists in the host keychain and in the agent environment. Nowhere else.
- The backplane is a switchboard. Combining it with a vault is a later, separate key domain, even if it ships in the same binary.

## Transport package

MinimalWebTransport is not vendored. It is a separate library, consumed as a NuGet package. Rig takes a package reference. The session envelope, device authentication, and redaction rules belong to Rig, not to that package.
