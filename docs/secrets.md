# Secrets

The agent never reads `.credentials`, `.env`, or `appsettings.json` for values. It asks the secret proxy. The proxy is the store `/init` filled: the keychain in the distro, or OpenBao if that profile is selected. There is no schema file in the repo. A name is registered when the user adds it, scoped to this repo.

Self-host is OpenBao. `deploy/docker-compose.yml` has an `openbao` profile that starts it in dev mode. It is off unless you select it. A hosted store, run for you, is a later product. This repo does not describe it.

Injection is the other half. The proxy writes the files a language already knows how to read, in hierarchy order: process environment, then the local file that language's library loads (`.env`, user-secrets, `appsettings.Development.json`). The agent does not hand-merge keys. A language pack names the file and the library. The harness writes the file for the matching glob and removes it on session end.

Values are redacted in the transcript and absent from `.structure.db`.
