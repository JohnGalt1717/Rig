# Backplane package

MinimalWebTransport is its own library, published on NuGet. Rig references the package. Rig does not vendor the transport.

The package owns the connection, the stream, and the frame carriage. Rig owns:

- The session envelope.
- Device authentication and pairing.
- Redaction of known secret names before a transcript event is stored.
- The rule that the backplane does not unwrap payloads.

Until the package is published, the AppHost documents the package id and does not vendor source. No submodule.
