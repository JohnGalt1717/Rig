# Phase 2

The first version is the local app host. This is the rest of it. Aspire goes away.

The repo config is the environment. It names the database, Valkey, the message bus, and the rest. Starting Rig on the repo starts them, rebuilds what drifted, and injects the connection strings into the running code. On a dev machine that does not mean a compose file. The WSL engine and Apple containers run the same resources. Compose is a target, not a requirement.

The same config deploys. A plugin maps each resource to the service on Kubernetes or a cloud provider, and the deploy script is generated from the config rather than written beside it. The local shape and the deployed shape are one description.

Rig is the telemetry consumer. The session already has one trace. Phase 2 installs the collector into the deployed environment, with a private dashboard. Baseline telemetry stays on. Tracing above that turns up when an issue is open and turns down when it closes. An agent pulls the trace and writes the root cause onto the ticket. A monitor agent watches for errors that should not be there, opens the ticket, and attaches the cause against the branch for that environment. No Azure Monitor bill, no AWS equivalent.

Tests get the same resources without a container per test. A test group asks Rig for a database, a Valkey, a bus. Rig cuts a sub-database on the server already running, returns the connection string, and drops it when the group ends. The language pack exposes that call. Isolation without the Testcontainers tax.

The dashboard lists every resource per environment. An agent can read it when the repo allows. A repo that is not a monorepo gets a root repo whose config points at the others, and Rig treats that root as the repo.

`/init` reads the code, proposes the resources, and offers the edits that wire key vault, database, and cache injection. It then runs until the local session starts, and it does not leave the rest of the tree broken.

None of this is in the first version. Checks stay read-only until this lands.
