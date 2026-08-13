<!-- markdownlint-disable -->

# Hardening Report: Blockception--action-minecraft-bedrock-diagnose/v1.20.62-0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Blockception--action-minecraft-bedrock-diagnose/v1.20.62-0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of full 40-character commit SHA digests, making them vulnerable to supply-chain attacks if the tag is moved.

- .github/workflows/npm-test.yml: `uses: actions/checkout@v4` and `uses: actions/setup-node@v4`
- .github/workflows/tagged-release.yml: `uses: ncipollo/release-action@v1`
- .github/workflows/dependabot.yml: `uses: dependabot/fetch-metadata@v1`

All should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/npm-test.yml:20`
- `.github/workflows/npm-test.yml:25`
- `.github/workflows/tagged-release.yml:13`
- `.github/workflows/dependabot.yml:14`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal `permissions:` block should be added (e.g. `permissions: read-all` or specific scopes).

- .github/workflows/npm-test.yml: no permissions defined at top-level or job level.
- .github/workflows/tagged-release.yml: no permissions defined at top-level or job level.

Locations:

- `.github/workflows/npm-test.yml:1`
- `.github/workflows/tagged-release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four unpinned action references by resolving their full commit SHAs via lookup_action_sha and updating the uses: lines with the format 'owner/repo@SHA # tag'. Added top-level permissions blocks to npm-test.yml (contents: read) and tagged-release.yml (contents: write, required for creating releases). The dependabot.yml already had explicit permissions defined and only needed the action SHA pinned.

