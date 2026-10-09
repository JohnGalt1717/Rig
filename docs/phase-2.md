# Phase 2

The first version is the local app host. This replaces Aspire. Nothing here ships in the first version. Checks stay read-only until it lands.

## The config is the environment

One file in the repo names every resource the system runs: the database, Valkey, the message bus, the projects, and the wire between them. Starting Rig on the repo reads that file and brings the environment up. A resource that drifted is rebuilt. A resource that is current is left alone.

Connection strings are not copied by hand. The host injects them into the running code for the local session, the same way Aspire hands a connection to a project. The code asks the host. It does not read a compose file.

On a dev machine the engine is whichever one is there. Docker, Podman, Apple containers, and the WSL engine are the same resources. A compose file is a deploy target, not the way the dev session starts. A repo that already has compose is read once, so `/init` can propose the config from it, and after that the config is the source.

## Deploy is the same file

The local shape and the deployed shape are one description. A plugin maps each resource to the service on Kubernetes or a cloud provider: the database resource to the managed database, Valkey to the cache service, the project to the workload. The deploy script is generated from the config. It is not a second file someone maintains beside it.

A change to the config is a change to the environment. The host applies it locally on startup, and the deploy applies it to the target the repo named. The agent does not write a Helm chart or a cloud CLI line. It edits the config, and the plugin renders the rest.

## Telemetry

Rig is the consumer. Aspire's dashboard goes away with Aspire.

Locally the session already has one trace across the resources the host started. Phase 2 installs the collector into the deployed environment and turns it up with the deploy. The dashboard is private to the repo. Baseline telemetry stays on. Tracing past that turns up when an issue is open and turns down when it closes, so the cluster is not paying for a full trace all day, and it is not paying Azure Monitor or the AWS equivalent at all.

An agent can open a live session against an environment the repo allows, pull the trace, and write the root cause onto the ticket. A monitor agent watches for errors that should not be there, opens the ticket, and attaches the cause against the branch for that environment. The issue contract from the first version holds the record.

## Tests

A test group does not start a container. It asks Rig for a database, a Valkey, a bus. Rig cuts a sub-database on the server already running, returns the connection string, and drops it when the group ends. The language pack exposes that call, so the test setup is a hook, not a Testcontainers recipe. The same call works on the dev machine and in checks.

Isolation is the sub-resource, not a new engine per test.

## The dashboard

Every environment the config names is a view: the resources, their state, the trace, the recent errors. An agent reads that view when the repo allows it. A ticket opened from a log line links back to the trace that produced it.

## One repo holds the contract

`.agents/`, the plans, the knowledge, the docs, and the environment config live in one repo. Links in that repo bring the other checkouts down, and the agents read the root.

A codebase that is already split does not have to merge. Rig creates the root, points it at the existing repos, and that root is what `/init` and the agents read. The code stays where it is. The contract does not.

## Init

`/init` reads the code and the compose file if one exists. It proposes the resources, the wires, and the edits that inject the key vault, the database, and the cache. It applies what the user accepts, starts the session, and runs until the local environment comes up. A failure is a row with a fix action. It does not leave the rest of the tree broken to get one resource started.
