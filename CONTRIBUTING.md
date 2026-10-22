# Contributing

These rules apply to every Didelo-lilian repository. Repository rulesets and the `conventions / check` status check enforce them.

## Flow

GitHub Flow: `main` is protected and always releasable. Every change goes through an issue, a short-lived branch and a pull request merged with squash.

1. Open or pick an issue.
2. Branch from `main` as `<issue>-<slug>`, lower-case with hyphens: `12-traefik-https`. `gh issue develop 12 --name 12-traefik-https` creates it and links it to the issue.
3. Commit with a signed commit. To catch up with `main`, rebase on `origin/main` and push with `--force-with-lease`. Never force-push a branch someone else works on.
4. Open a pull request. Its title follows Conventional Commits and its body says `Closes #12`.
5. Once the checks are green and the conversations are resolved, squash merge. The branch is deleted on merge.

## Pull request title

Squash merge turns the PR title into the commit subject on `main`, so the title is what ends up in the history and the changelog.

```
<type>(<optional scope>)<optional !>: <summary>
```

| Type | For |
|------|-----|
| `feat` | a new feature |
| `fix` | a bug fix |
| `perf` | a performance improvement |
| `refactor` | a code change with no behaviour change |
| `docs` | documentation only |
| `test` | tests only |
| `build` | the build system or dependencies |
| `ci` | CI configuration |
| `chore` | maintenance that fits nowhere else |
| `style` | formatting only |
| `revert` | reverting an earlier change |

The summary is in English and in the imperative, starts lower-case and has no trailing period: `feat(dns): add the hello record`. A `!` marks a breaking change. Commits inside a branch should follow the same format. Only the title is checked, because squash merge drops the branch commits.

## Branch protection

| Target | Rules |
|--------|-------|
| `main` | no direct push, force push or deletion; pull request required with resolved conversations; squash merge only; linear history; signed commits; required status checks, up to date with `main` |
| other branches | signed commits |
| `v*` tags | cannot be moved or deleted |

Dependabot (`dependabot/…`) and release-please (`release-please--…`) branches are exempt from the naming rule.

## Releases

A release is tagged at the end of each iteration (one weekend). Versions follow SemVer as `vX.Y.Z`, and the changelog is generated from the PR titles.
