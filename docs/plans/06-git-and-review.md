# Grill: git and review

Sources: `docs/product.md`.

Settled: identity from harness key or `user.email`, no raw GitHub MCP, review posts to the pull request.

Open:

1. Which GitHub account map wins when a machine has several `gh` logins?
2. Does the review agent block merge, or only comment?

Recommendation on 1: the harness key in `.git/config` wins, and `/init` writes it after asking once.
Recommendation on 2: comment only.
