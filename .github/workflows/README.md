# YourOwnLab reusable workflows

Reusable workflows centralize proven CI implementation while each repository keeps its triggers, permissions, and required check visible locally.

## Node CI

`node-ci.yml` is the baseline for dependency-light Node.js web applications. It:

- grants read-only repository content permission;
- checks out code without persisting credentials;
- uses Node.js 22 by default;
- installs the committed lockfile with `npm ci`;
- runs the repository-owned `npm run check` contract;
- pins third-party action references to full commit SHAs;
- limits the job to 15 minutes.

Example caller:

```yaml
name: CI

on:
  pull_request:
  push:
    branches: [main]

permissions:
  contents: read

concurrency:
  group: ci-${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  check:
    uses: YourOwnLab/.github/.github/workflows/node-ci.yml@main
```

The resulting required-check name changes from a local job name to the reusable workflow's composed job name. Update branch protection only after observing the exact successful check on an adoption pull request.

## Change policy

- Treat changes as platform changes and use a pull request.
- Keep permissions minimal and declare them explicitly.
- Pin external actions to a full commit SHA and retain the release tag in a comment.
- Do not accept secrets unless a concrete workflow requires them and its threat model is documented.
- Prefer backward-compatible inputs; coordinate breaking changes with every caller.
- Adopt centrally in `template-webapp` first, then roll out to product repositories deliberately.
