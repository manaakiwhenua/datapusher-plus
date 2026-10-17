# datapusher-plus (Manaaki Whenua fork)

This is Manaaki Whenua - Landcare Research's fork of [dathere/datapusher-plus](https://github.com/dathere/datapusher-plus), the CKAN extension that loads resource files into the DataStore. Our DataStore image builds from it, so a fix we contribute upstream reaches DataStore before upstream releases it.

For the extension itself, see upstream's [README](../README.md).

## Branches

| Branch | What it is |
|---|---|
| `downstream` (default) | The branch we build from: an upstream commit plus the carried patches below. Protected; changes arrive by pull request. |
| `main` | A mirror of `dathere/datapusher-plus` `main`. Never commit to it. |
| `fix/*`, `feat/*`, `docs/*` | Cut from `main`, for pull requests to upstream. |
| `build/*` | Cut from `downstream`, for changes that only make sense for us. |

- **Mirror:** `main` from `dathere/datapusher-plus`
- **Adopted upstream commit:** `1825d62` (27 April 2025, two days after release 2.0.0). This is a deliberate exception to adopting a release: DataStore has run this commit since before the fork followed this layout, and no upstream release yet contains the carried patch below. Adopting a release here is a datapusher-plus upgrade with its own testing, not a pin bump.

Anything that builds from this fork pins a commit on `downstream`, never a branch name.

## Carried patches

Our own fixes, merged into `downstream`. Remove a row once the adopted release contains the fix.

| Branch | Upstream pull request | What it does |
|---|---|---|
| `fix/site-user-context-for-activity` | [dathere/datapusher-plus#341](https://github.com/dathere/datapusher-plus/pull/341) (merged to `main` 23 September 2026, not yet released) | names the site user when creating or deleting DataStore tables, which the CKAN 2.11+ activity plugin requires |

## Keeping up with upstream

When upstream publishes a release that contains everything in the carried-patches table:

```shell
git fetch upstream --tags
git switch main && git merge --ff-only upstream/main && git push origin main
git switch -c build/adopt-<release> downstream && git merge <release>
```

Resolve any conflicts, update the adopted release and the carried-patches table above, and open a pull request into `downstream`. Then bump the pinned commit wherever this fork is built.

## GitHub Actions

Actions are disabled on this fork. Upstream's workflows test and publish upstream's code and are not meant to run here.
