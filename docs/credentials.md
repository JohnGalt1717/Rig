# Credentials

Bring your own, for now.

Committed: `credentials.schema.json`, name, glob, description, when to use. Not committed: values. `.credentials` and `.env` are gitignored.

`/init` asks for a local file or fills the schema. The harness writes the OS keychain and injects the agent environment. The agent sees names and descriptions.

GitHub Actions secrets are not a source. The API does not return the value.

`deploy/docker-compose.yml` has a vault profile that starts Hashicorp Vault in dev mode. It is off unless selected. It is a local stand-in, not the product store.
