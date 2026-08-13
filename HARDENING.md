<!-- markdownlint-disable -->

# Hardening Report: Blockception--action-minecraft-bedrock-diagnose/v1.21.44

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Blockception--action-minecraft-bedrock-diagnose/v1.21.44** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files use mutable tag/version references instead of pinned 40-character SHA commit digests, making the action vulnerable to supply-chain attacks if the referenced action is compromised or the tag is moved.

- .github/workflows/dependabot.yml: `uses: dependabot/fetch-metadata@v2`
- .github/workflows/npm-test.yml: `uses: actions/checkout@v4`
- .github/workflows/npm-test.yml: `uses: actions/setup-node@v4`
- .github/workflows/tagged-release.yml: `uses: ncipollo/release-action@v1`

Locations:

- `.github/workflows/dependabot.yml:15`
- `.github/workflows/npm-test.yml:21`
- `.github/workflows/npm-test.yml:26`
- `.github/workflows/tagged-release.yml:13`

### missing-permissions (severity: medium)

The workflow files npm-test.yml and tagged-release.yml have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions. Each workflow should declare minimal required permissions.

Locations:

- `.github/workflows/npm-test.yml:1`
- `.github/workflows/tagged-release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all four unpinned action references to full 40-character SHA digests while preserving the original tag in a comment. Added top-level `permissions: contents: read` to npm-test.yml and `permissions: contents: write` to tagged-release.yml (write is required for the release-action to create GitHub releases). The dependabot.yml already had a permissions block so only the SHA pinning was needed there.

