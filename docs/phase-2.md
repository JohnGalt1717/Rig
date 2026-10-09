# Phase 2

The first version is the local app host for a session. Phase 2 is the app host for the repo, local and deployed. Aspire goes away. Nothing in this document ships in the first version. Checks stay read-only until it lands.

Aspire got the shape right and stopped at the dev machine: a config names the resources, the host starts them, the dashboard shows them, the code receives a connection string. It does not deploy from that config, it does not own the trace once the process leaves the laptop, and it does not hand any of it to an agent as a contract. Phase 2 is that host, continued.

## The config is the environment

One file in the repo names every resource the system runs.

A resource is a project, a database, Valkey, a message bus, an object store, a secret store, or a collector. Each entry names the kind, the engine-neutral settings, and the wires: which project receives which connection, which bus a worker consumes, which store a service reads. The file is the source. A compose file, a Helm chart, and a cloud template are renderings of it.

Starting Rig on the repo reads the file and brings the environment up. A resource that drifted is rebuilt. A resource that is current is left alone. A resource the file no longer names is stopped. This is the same loop on every open, not a command the agent remembers to run.

Connection strings are not copied by hand and they are not committed. The host injects them into the running code for the local session. The code asks the host, through the library the language pack adds, and receives the string for this session. A second session gets its own database and its own string. The code does not read a compose file, an `appsettings` overlay, or an env file the agent wrote.

## Engines

On a dev machine the engine is whichever one is there. Docker, Podman, Apple containers, and the WSL engine are the same resources. The pack names the engine at `/init`. The agent does not.

A compose file is a deploy target, not the way the dev session starts. A repo that already has one is read once, so `/init` can propose the config from it. After that the config is the source, and compose is what the host emits when the target is a compose host. Dev does not require it, which is why Apple containers and the WSL engine work without a compose binary.

## Deploy is the same file

The local shape and the deployed shape are one description. A plugin maps each resource to the service on a target.

Kubernetes is the first target after compose: a database resource becomes a StatefulSet or an external name, a project becomes a Deployment, Valkey becomes the cache workload, the collector becomes a DaemonSet or a sidecar. A cloud plugin maps the same resource to the managed service: the database to the managed database, Valkey to the cache product, the project to the workload service. The mapping is the plugin. The config does not grow a second copy per cloud.

The deploy script is generated from the config. It is not a file someone maintains beside it. A change to the config is a change to the environment. The host applies it locally on startup. The deploy applies it to the target the repo named. The agent does not write a Helm chart, a Terraform line, or a cloud CLI invocation. It edits the config, and the plugin renders the rest.

Checks run the same rendering. A workflow does not carry a hand-written deploy step. It calls the host, and the host emits the target from the config on that commit.

## Telemetry

Rig is the consumer. Aspire's dashboard goes away with Aspire.

Locally the session already has one trace across the resources the host started. The client span, the API span, and the downstream call share an id, because the host propagated it when it started them. Flutter and the backend are on that trace when the pack instruments them. The agent asks for the trace. It does not tail twelve consoles.

Phase 2 installs the collector into the deployed environment and turns it up with the deploy. The dashboard is private to the repo. It is not Azure Monitor and it is not the AWS equivalent. Baseline telemetry stays on: errors, request rate, a sample of traces. Tracing past that turns up when an issue is open and turns down when it closes, so the cluster is not paying for a full trace all day, and it is not paying a vendor to store it.

An agent can open a live session against an environment the repo allows, pull the trace, and write the root cause onto the ticket through the issue contract. The fields are the ones the first version already requires: root cause, plan, unanticipated changes, what was actually found. A monitor agent watches for errors that should not be there, opens the ticket, attaches the trace, and files the cause against the branch for that environment. The ticket is the record. The log line is the evidence.

## Tests

A test group does not start a container. It asks Rig for a database, a Valkey, a bus. Rig cuts a sub-database on the server already running, a key prefix or a database index on the Valkey already running, a vhost or a stream on the bus already running. It returns the connection strings. It drops them when the group ends.

The language pack exposes that call, so the test setup is a hook, not a Testcontainers recipe. The same call works on the dev machine and in checks, because both are a host reading the same config. Isolation is the sub-resource, not a new engine per test. A group that fails to release is reaped with the session, the way a process group is.

## The dashboard

Every environment the config names is a view: the resources, their state, the last deploy, the trace, the recent errors. Local is an environment. So is each target the repo deploys to.

An agent reads that view when the repo allows it. A ticket opened from a log line links to the trace that produced it, and the trace links to the resource. The panel from the first version, the one that shows the agent graph, is the same surface with the resources added.

## One repo holds the contract

`.agents/`, the plans, the knowledge, the docs, and the environment config live in one repo. Links in that repo bring the other checkouts down, and the agents read the root. The globs, the behavior, and the knowledge apply across the linked trees, because the root is the repo the harness loaded.

A codebase that is already split does not have to merge. Rig creates the root, points it at the existing repos, and that root is what `/init` and the agents read. The code stays where it is. The contract does not. A pull into a linked repo is a pull the root sees.

## Init

`/init` reads the code and the compose file if one exists. It proposes the resources, the wires, and the edits that inject the key vault, the database, and the cache. The proposal is a diff. The user accepts it. The host applies it, starts the session, and runs until the local environment comes up.

A failure is a row with a fix action, handed to the agent, same as a restore failure. It does not leave the rest of the tree broken to get one resource started. A later pull that changes the config runs `/repair`, which is the same file against a machine that already exists.

## What the agent still does not get

A cloud CLI, a Helm binary, a compose command, and a vendor monitoring console are refused, same as `docker` is refused in the first version. The agent edits the config, asks the host, and reads the dashboard. A destroy against a deployed environment is the terminal gate from the first version: classified, blocked, and confirmed, with the risk named. Silence is not approval.
