# ADR 0003: Bring-your-own credentials

Status: accepted

GitHub Actions secrets cannot be read back. Schema is committed. Values stay in a gitignored file and the OS keychain. A compose vault profile is optional and off by default.
