# Secrets

The agent never reads `.credentials`, `.env`, or `appsettings.json` for values. It asks the secret proxy. The proxy is the store `/init` filled: keychain in the distro, or the vault profile if that is selected. The schema in `credentials.schema.json` is the name, the glob, and when to use it.

Injection is the other half. The proxy writes the files a language already knows how to read, in hierarchy order: process environment, then the local file that language's library loads (`.env`, user-secrets, `appsettings.Development.json`). The agent does not hand-merge keys. A language pack names the file and the library. The harness writes the file for the matching glob and removes it on session end.

Values are redacted in the transcript and absent from `.structure.db`.
