<!-- markdownlint-disable -->

# Hardening Report: dbt-labs--dbt-cloud-job-action/v8.0.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **dbt-labs--dbt-cloud-job-action/v8.0.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses mutable tag-based action references instead of pinned full-length SHA commits. Both `actions/checkout@v4` and `actions/setup-node@v4` use version tags that can be moved by the upstream repository, enabling supply-chain attacks. Each should be pinned to a full 40-character commit SHA (e.g., `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`).

Locations:

- `.github/workflows/ci.yml:13`
- `.github/workflows/ci.yml:15`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents and pull requests). A minimal explicit permissions block such as `permissions: read-all` or specific scopes (e.g., `contents: read`) should be added.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed hardened/action/.github/workflows/ci.yml: (1) Pinned actions/checkout@v4 to full SHA 11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v4 to full SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, with original tags preserved as comments. (2) Added top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required access.

