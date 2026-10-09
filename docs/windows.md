# Windows

On Windows, Rig is the Linux app. WSLg shows the window. The process, the checkout, the language server, the hooks, and the agent are Linux. There is no Windows build of the host, and the agent never speaks PowerShell.

`/init` runs inside the distro. `.prerequisites.json` installs Linux packages. Bash hooks run as bash. Paths are Linux paths. The harness does not translate `C:\` and does not strip CR to pretend a Windows shell is Unix.

The checkout lives in the distro, under the Linux home directory. A repo opened through the Windows drive is still a cross-OS mount. WSL 3 exposes that mount with virtiofs, which is the public replacement for the old 9p default and is fast enough to use, but it is still a Windows filesystem with Windows case rules. `/init` warns on that root. The supported root is the Linux filesystem, where the agent and the tools agree on every path.

Git identity, `gh`, Docker, and the secret store are the ones in the distro. The Windows Credential Manager and the Windows `gh` login are a different machine. Pairing still works. The backplane does not care which OS drew the window.

Windows 10 is out. WSLg is Windows 11.
