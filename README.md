# Causari Audit Demo

A repository that exists to run the
[Causari Survival Audit](https://github.com/marketplace/actions/causari-survival-audit)
action in public, with the published release, where anyone can read the
run and the comment it posts.

What runs: on every pull request, on every push to `main`, and every
Monday whether or not anything changed. The Monday run is the point: it
shows that `uses: croviatrust/causari@v1` still installs and audits with
the current release, this week, not the week the demo was written.

What it shows: [pull request #1](https://github.com/croviatrust/causari-audit-demo/pull/1)
adds four lines in one commit that carries a `Co-Authored-By: Claude`
trailer. The sticky comment on that PR is the audit of that branch:
3 commits, 1 AI-tagged, 4 of 4 lines still at HEAD. The same comment
says the sample is below the floor of 5 commits and that no age-matched
gap can be computed. That is the honest result for a repository this
small: counts, not a rate, and not a grade.

`main` has no AI-tagged commit, so the audit of `main` reports the
untagged lines and `null` for everything AI-tagged. `null` is not zero.

Each run uploads `causari-audit.json`, the `re audit --json` output the
comment is rendered from.

Reproduce locally with the same release:

```sh
curl -fsSL https://causari.dev/install.sh | sh
re audit croviatrust/causari-audit-demo --summary
```

The workflow is [`.github/workflows/audit.yml`](.github/workflows/audit.yml):
a checkout with `fetch-depth: 0` and one `uses:` line.
