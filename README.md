# .github

Defaults shared by every Didelo-lilian repository:

- [CONTRIBUTING.md](CONTRIBUTING.md): the git flow, branch and commit conventions, branch protection.
- [SECURITY.md](SECURITY.md): how to report a vulnerability.
- Issue and pull request templates, used by any repository that doesn't define its own.
- [`pr-conventions.yml`](.github/workflows/pr-conventions.yml): reusable workflow that checks branch names and PR titles.

To enable the check in a repository:

```yaml
# .github/workflows/pr.yml
name: PR
on:
  pull_request:
    types: [opened, edited, synchronize, reopened]
permissions: {}
jobs:
  conventions:
    uses: Didelo-lilian/.github/.github/workflows/pr-conventions.yml@main
```

Then require the `conventions / check` status check on `main`.
