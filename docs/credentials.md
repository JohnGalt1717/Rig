# Credentials

Bring your own, for now.

Committed: a schema file, `credentials.schema.json`, name, glob, description, and when to use it. Not committed: values. `.credentials` and `.env` are gitignored.

`/init` asks the user to point at a local file or to fill the schema. The harness writes values into the secret store and injects them into the agent environment for the matching glob. The agent sees the name and the description. The panel shows which schema entries matched. The agent never reads the file.

GitHub Actions secrets are not a source. The API does not return the value.

## Self-host

`deploy/docker-compose.yml` has an `openbao` profile that starts OpenBao in dev mode. It is off unless the operator selects it. Production key handling is a later hosted store, separate from this repo.
