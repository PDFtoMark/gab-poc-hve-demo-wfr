# PoC: hve-core demo-material-render workflow_run author-run trust bypass

Authorized security assessment reproduction. The base repo mirrors the trust
decision made by `microsoft/hve-core .github/workflows/demo-material-render.yml`:
the `workflow_run` consumer accepts a triggering run only when it is a successful
run of `.github/workflows/demo-material-author.lock.yml` on the default branch.

The attacker forks this repo, rewrites `demo-material-author.yml` in the fork so
the same workflow name/path runs on `pull_request`, hashes and uploads a
`demo-material-content-<run_id>` artifact, and opens a PR from a fork branch
named `main`. The privileged consumer then accepts that run and consumes the
attacker artifact.
