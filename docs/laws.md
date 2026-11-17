# Laws

Laws are precise, human-owned properties that the implementation must never break. They live as Markdown files (`.law`) and are the source of truth for what tests must enforce.

They are not proofs. They are unambiguous claims. A test expert agent (or a human) reads them and writes or reviews tests in the project's language that check the properties. Another agent reviews the tests to confirm they actually enforce the law rather than merely passing on a few examples.

This is the practical middle ground between natural-language requirements and a full proof assistant: the law is clear enough for an agent to translate into property-based or exhaustive tests, and the tests run in CI as the gate.

## Layout

Laws live under `.agents/tests/` (or a mirrored `laws/` tree) and follow the same relative path as the code they govern:

```
.agents/tests/
  Api/Ledger/
    balances_sum_to_zero.law
    no_negative_balances.law
  Apps/Web/Components/
    cart_round_trip.law
```

A move of code rewrites the mirrored paths in the same change, the same rule used for behavior and knowledge files.

## Shape of a law

A `.law` file is ordinary Markdown. The precision comes from the interview that produced it, not from a formal syntax. A recommended structure:

```markdown
# Law: balances_sum_to_zero

For every sequence of transfers applied to an initially empty ledger,
the sum of all account balances equals zero.

## Must hold
- After any number of transfers
- Including zero-amount and self-transfers
- After concurrent application (order must not matter for the sum)

## Explicit non-goals
- Individual account non-negativity (see no_negative_balances.law)
```

The title is the law's name. The first paragraph is the claim. The rest is human explanation and constraints the test expert must respect.

## Agents

Two roles, both ordinary agents under `.agents/agents/`:

1. **Law interviewer.** Uses the grill style. It reads the code surface and existing tests for a path, then interviews the human until every quantification, edge case, and invariant is explicit. It writes the `.law` file. The human owns the final wording. It does not write implementation or tests.

2. **Law reviewer.** Given a law and the tests that claim to enforce it, it checks whether the tests actually cover the property. It looks for missing generators, trivial assertions, hard-coded examples that ignore the law, and gaps. It does not decide the law is true; it decides the tests would fail if the law were broken.

Both agents are scoped by globs so they only see the relevant area.

## Enforcement

The verifier (see [verifier.md](verifier.md)) treats an open law with no matching tests as an unmet row. A change that touches a path with laws must keep the corresponding tests green. Language packs can supply default property-based testing libraries and generators for the common cases.

Laws stay language-agnostic. The tests are written in whatever language the implementation uses. The mapping from law to tests is the job of the test expert agent, guided by the project's language pack and any conventions recorded in `.agents/knowledge/`.

## Relation to plans

A grill session that settles a feature can emit laws as part of the plan. Execution does not start until the laws for the affected paths exist and the interviewer has no remaining open questions about them.
