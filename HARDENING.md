<!-- markdownlint-disable -->

# Hardening Report: Blockception--action-minecraft-bedrock-diagnose/v1.20.71-1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Blockception--action-minecraft-bedrock-diagnose/v1.20.71-1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in workflow files use mutable tags instead of full 40-character commit SHA pins, making the workflows vulnerable to supply-chain attacks if the referenced action tags are moved or compromised. Failing references: `actions/checkout@v4` (npm-test.yml line 23), `actions/setup-node@v4` (npm-test.yml line 26), `ncipollo/release-action@v1` (tagged-release.yml line 15), `dependabot/fetch-metadata@v1` (dependabot.yml line 15).

Locations:

- `.github/workflows/npm-test.yml:23`
- `.github/workflows/npm-test.yml:26`
- `.github/workflows/tagged-release.yml:15`
- `.github/workflows/dependabot.yml:15`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be broad). Each workflow should declare the minimal required permissions explicitly.

Locations:

- `.github/workflows/npm-test.yml:1`
- `.github/workflows/tagged-release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all four unpinned action references to full 40-char SHAs: actions/checkout@v4 → 11d5960a..., actions/setup-node@v4 → 49933ea5..., ncipollo/release-action@v1 → 339a8189..., dependabot/fetch-metadata@v1 → 8348ea7f.... Added top-level permissions blocks to npm-test.yml (contents: read) and tagged-release.yml (contents: write, needed to create GitHub releases). dependabot.yml already had permissions defined and only needed the action SHA pinned.

