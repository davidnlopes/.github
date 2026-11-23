# .github

This repository holds the workflows that every public repository in the organization must pass before a pull request merges. Each workflow in `.github/workflows/` is a thin caller. The checks themselves live in [reusable-workflows](https://github.com/davidnlopes/reusable-workflows).

Organization rulesets mark these workflows as required, so repository owners do not copy them into their own repositories.

## Required checks

| Workflow | Check |
| --- | --- |
| [`required-semantic-pr.yaml`](.github/workflows/required-semantic-pr.yaml) | Labels the pull request, then requires a Conventional Commits title and exactly one `major`, `minor`, or `patch` label, and blocks hold labels such as `do-not-merge` |
| [`required-trivy.yaml`](.github/workflows/required-trivy.yaml) | Scans the change with Trivy for vulnerable dependencies, secrets, and misconfigurations |

## Change a check

To change what a check does, edit the matching workflow in `reusable-workflows`. To add a check or change when it runs, edit the caller here and open a pull request. Use a Conventional Commits title, because the semantic pull request check also runs on this repository.
