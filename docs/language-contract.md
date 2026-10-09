# Language contract

Every language pack fills the same surface. The agent, the flows, and the dashboard see that surface. The pack is the only place a language is special.

| Contract | What it is |
| --- | --- |
| Analyze | Resident analyzer. Pushes problems when a file changes. No build. Roslyn for C#, the Dart analyzer, `tsc` in watch, eslint. |
| Build | Full compile. Diagnostics parse into the same problems panel. |
| Format | One command, the dirty set, deterministic. |
| Debug | DAP, Rig is the only client. See [debugger.md](debugger.md). |
| Test | List, metadata, run, coverage. The metadata says when the agent should run the test. |
| Drive | e2e. The agent can drive by hand, or run the JSON rules it maintains. Failures come back as events. The agent corrects the rule and reruns. |
| Problems | The merged panel. Analyze, build, and test write rows here. The UI shows them as they arrive. |

A prompt does not grow a special case for a language. If a pack cannot fill a contract, that action is absent, and the panel says so.

The default workflow is deterministic. Edit one file: analyze that file, problems update. Edit many: the harness holds the dirty set, then analyze, problems, and format run on that set at the end of the burst. The agent does not decide which files changed. The proxy saw the edits.

Stop hooks do not re-run the analyzer. They read the panel. The agent asks for the latest. The harness already has it.
