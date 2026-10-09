# Folder contract

One `.agents/` at the git root. Nested `.agents/` directories are ignored. A package that leaves the repo does not take a private agent tree with it. That is accepted.

## Layout

```
.agents/
  agents/       one file per agent, globs and harness list
  behavior/     mirror of the repo, optional globs array
  knowledge/    notes, same relative path as the code
  hooks/        declarations the runner executes
  skills/       SKILL.md folders, loaded when the matched agent names them
  plans/        settled plans, written by grill, read by execution
```

## Agent file

An agent declares an id, a description, a globs array, a priority, and the harnesses it may run under (`grok-build`, `codex`, `copilot`, and so on). No globs means it does not match. Several matches: longest glob, then priority. A remaining tie is an error.

## Behavior and knowledge

A behavior file with no globs applies to its mirror path. A globs array extends it to cross-cutting sets, such as every test project. Knowledge uses the same mirror. A move of code rewrites the mirrored paths in the same change. The panel lists both.

## Hooks

A hook declares globs, harnesses, and a command. The runner maps Windows paths and strips CR. Language packs ship default quality hooks. A user hook overrides only where its glob is more specific.

## What is not in the contract

Parent inheritance. Merge with a nearer file winning. A second `.agents/` under `Api/` or `Apps/`.
