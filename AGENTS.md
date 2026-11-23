# .github

This repository defines the organization's required workflows for public repositories. It contains no application code. Each file in `.github/workflows/` runs on pull requests in every repository that an organization ruleset targets.

## Callers here, logic elsewhere

A required workflow here only chooses when a check runs and which permissions it gets. The check itself lives in the `reusable-workflows` repository, and each job calls it with `uses:`. To change what a check does, change that repository, not this one.

## Every repository runs these workflows

A change here lands on every targeted repository at once, and a failing workflow blocks their pull requests. Write workflows that make no assumption about the repository they run in. Key anything repository-specific, such as concurrency groups, on `github.repository`.

## What must stay true

- Workflows contain no steps of their own. Each job calls a reusable workflow, so the check logic stays in one place and every repository gets the same behaviour.
- Reusable workflows are pinned to a major version tag, such as `@v1`, not to a branch or a commit SHA. Maintainers can ship fixes through the tag, and a major version change is the signal for a breaking change.
- Every workflow declares top-level `permissions`, and grants only what its jobs need. Required workflows run with the pull request token across many repositories, so the default token scope must not apply.
- Required workflow files start with `required-`. The prefix separates workflows that rulesets enforce from any workflow that only serves this repository.
