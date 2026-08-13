<!-- markdownlint-disable -->

# Hardening Report: Blockception--action-minecraft-bedrock-diagnose/v1.21.44-0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Blockception--action-minecraft-bedrock-diagnose/v1.21.44-0** was hardened automatically. 5 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow uses actions pinned to mutable version tags instead of immutable full-length SHA commit hashes. If a tag is moved (e.g. by a compromised upstream), the workflow will silently execute different code. Failing references: `actions/checkout@v4`, `actions/setup-node@v4`.

Locations:

- `.github/workflows/npm-test.yml:22`
- `.github/workflows/npm-test.yml:26`

### unpinned-uses (severity: high)

Workflow uses an action pinned to a mutable version tag instead of an immutable full-length SHA commit hash. Failing reference: `ncipollo/release-action@v1`.

Locations:

- `.github/workflows/tagged-release.yml:13`

### unpinned-uses (severity: high)

Workflow uses an action pinned to a mutable version tag instead of an immutable full-length SHA commit hash. Failing reference: `dependabot/fetch-metadata@v2`.

Locations:

- `.github/workflows/dependabot.yml:16`

### missing-permissions (severity: medium)

Workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository default (often `write-all`), granting broader access than necessary.

Locations:

- `.github/workflows/npm-test.yml:1`

### missing-permissions (severity: medium)

Workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository default (often `write-all`), granting broader access than necessary.

Locations:

- `.github/workflows/tagged-release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 5 findings across 3 workflow files:
1. npm-test.yml: Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020; added top-level `permissions: contents: read`.
2. tagged-release.yml: Pinned ncipollo/release-action@v1 → @339a81892b84b4eeb0f6e744e4574d79d0d9b8dd; added top-level `permissions: contents: write` (required to create GitHub releases).
3. dependabot.yml: Pinned dependabot/fetch-metadata@v2 → @21025c705c08248db411dc16f3619e6b5f9ea21a; permissions block already existed (contents: write, pull-requests: write) so no change needed there.

