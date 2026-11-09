# Product

Rig drives the coding harnesses already installed and logged in: Grok Build, Codex, Claude Code. Those keep their loops. Rig owns the environment they run in.

The user clones a repository, runs `/init`, and the session is scoped, tooled, isolated, and able to edit, test, and review. Direct editing is secondary. The agent does the work. The user sees the diff, the diagnostics, and why the harness loaded what it loaded.

The first proof is C# and Flutter. Next.js and Vite are later packs.

## Sessions

A session starts in a directory and is scoped by that directory plus the work. The harness resolves the git root, loads the single `.agents/` there, and applies globs. Several sessions run at once. Each gets its own network bridge and its own containers. See [isolation.md](isolation.md).

## How the agents are driven

See [harness.md](harness.md). Each agent area gets one MCP. That MCP replaces the defaults, exposes Rig's contracts, and proxies any additional MCP the area declared. Skills name the contracts. Language packs configure the debugger, the UI driver, coverage, and the test harness for the area. `/init` installs them.

Least-cost routing picks the harness when the repo does not name one.

## Command line

No raw shell. Commands go through the proxy. On Windows the proxy runs them in WSL.

## Deploy

The setup is code in the repo. It generates the pipeline. See [deploy.md](deploy.md). Libraries that let a language call the deploy API directly are later.

## Later

A hosted vault. A native Flutter editor in place of Monaco. Language libraries for deploy.
