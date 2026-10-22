# .github

Defaults shared by every Didelo-lilian repository:

- [CONTRIBUTING.md](CONTRIBUTING.md): the git flow, branch and commit conventions, branch protection.
- [SECURITY.md](SECURITY.md): how to report a vulnerability.
- Issue and pull request templates, used by any repository that doesn't define its own.
- [`pr-conventions.yml`](.github/workflows/pr-conventions.yml): reusable workflow that checks branch names and PR titles.
- [`release.yml`](.github/workflows/release.yml): reusable workflow that versions and releases with [release-please](https://github.com/googleapis/release-please).

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

To enable releases, add `release-please-config.json` and `.release-please-manifest.json` (see [infra](https://github.com/Didelo-lilian/infra)) and:

```yaml
# .github/workflows/release.yml
name: Release
on:
  push:
    branches: [main]
permissions: {}
jobs:
  release:
    uses: Didelo-lilian/.github/.github/workflows/release.yml@main
    secrets: inherit
```

It authenticates as the organization's release GitHub App: `RELEASE_APP_ID` (organization variable) and `RELEASE_APP_PRIVATE_KEY` (organization secret).
