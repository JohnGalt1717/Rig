# Dev certificates

`/init` issues the local development certificate and trusts it on the machine the host is running on. On Windows that machine is the distro, and the trust is also installed into the Windows store so the browser on the desktop accepts it. A new device that attaches does not inherit the cert. `/init` on that device issues and trusts one for the host it runs.

Add, rotate, and remove are harness commands. The agent does not run `dotnet dev-certs` or `mkcert` itself. A service the session starts uses the cert the harness already trusted. An untrusted cert at launch is an init failure, shown before the agent begins.
