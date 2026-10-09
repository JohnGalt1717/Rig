# Folder contract

One `.agents/` at the git root. Nested `.agents/` directories are ignored.

```
.agents/
  agents/       one file per agent, globs and harness list
  behavior/     mirror of the repo, optional globs array
  knowledge/    OKF documents, same relative path as the code
  hooks/        declarations the runner executes
  skills/       SKILL.md folders, loaded when the matched agent names them
  plans/        execution plans, after the grill frontier is empty
```

Longest matching glob wins, then priority. A tie is an error the panel shows. No parent inheritance. Project Fulcrum's nested agent trees are not copied.
