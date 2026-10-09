# ADR 0002: Relay is a switchboard

Status: accepted

The .NET service stores directory state and forwards ciphertext. It does not store transcripts, source, or credentials. Host is the only writer. No prompt queue on the relay.
