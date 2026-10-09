# Grill: relay and data

Sources: `docs/backend.md`, `docs/relay.md`, ADR 0002.

Settled: .NET 11, SQLite, EF, personal as an organization of one, MinimalWebTransport as a NuGet, no transcript bodies in the database.

Open:

1. Package id and repository name for the extracted transport.
2. Does the AppHost ship in the first cut, or is `dotnet run` enough until Aspire embed?
3. Device key storage: public keys in SQLite are required for the directory. Private keys stay local.

Recommendation on 2: `dotnet run` first. Aspire embed is the C# pack, not the relay.
