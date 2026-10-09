# Agents

Rig has one `.agents/` directory, at the repository root. The harness loads it. Agents do not walk the tree looking for another one.

Scope is globs plus an explicit priority, not file proximity. Longest matching glob wins. A tie is an error the panel shows. The dispatcher hands off. It does not do the work.

Knowledge lives at `.agents/knowledge/<same relative path>`. Behavior lives at `.agents/behavior/<same relative path>` and may add a globs array. Hooks are declared, and the harness runner executes them. Agents do not shell out.

Plans in `.agents/plans/` are execution plans. Grill sessions that must finish first are in `docs/plans/`.
