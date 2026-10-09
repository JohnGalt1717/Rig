# Grill: credentials and init

Sources: `docs/credentials.md`, ADR 0003.

Settled: schema committed, values gitignored, keychain injection, no GitHub secret readback, vault compose profile off by default.

Open:

1. Schema filename and whether globs live on the schema or only on agents.
2. Does `/init` block the session until required schema entries are filled?

Recommendation on 2: block only entries the matched agent marks required. The rest warn on the panel.
