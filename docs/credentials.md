# Credentials

There is no `credentials.schema.json`. The helper holds the account.

Git and `gh` use the credential helper `/init` installed. The repo setup names the account for that remote. A tracker other than GitHub gets a login prompt on first use, stored against this repo only, and injected into the call. The agent does not see the token, and a login for one repo is not offered to another.

Secret values for the running code come from the secret proxy: the keychain in the distro, or OpenBao if that profile is selected. The agent asks the proxy by name. It never reads `.credentials` or `.env`.

GitHub Actions secrets are not a source. The API does not return the value.
