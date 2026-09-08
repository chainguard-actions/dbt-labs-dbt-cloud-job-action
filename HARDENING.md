<!-- markdownlint-disable -->

# Hardening Report: dbt-labs--dbt-cloud-job-action/v8.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **dbt-labs--dbt-cloud-job-action/v8.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/ci.yml references two actions using mutable version tags (@v4) instead of full 40-character commit SHAs. This means a compromised or modified tag could silently execute different code. Affected references: `actions/checkout@v4` (line 14) and `actions/setup-node@v4` (line 16). These should be pinned to their full SHA digests, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/ci.yml:14`
- `.github/workflows/ci.yml:16`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key and the only job (`test`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g. write access to contents). A minimal explicit `permissions:` block (e.g. `contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/ci.yml: (1) Pinned actions/checkout@v4 to full SHA 11d5960a326750d5838078e36cf38b85af677262 # v4. (2) Pinned actions/setup-node@v4 to full SHA 49933ea5288caeca8642d1e84afbd3f7d6820020 # v4. (3) Added top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required permissions.

