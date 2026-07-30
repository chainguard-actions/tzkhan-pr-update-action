<!-- markdownlint-disable -->

# Hardening Report: tzkhan--pr-update-action/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **tzkhan--pr-update-action/v1.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references `tzkhan/pr-update-action@v1`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling a supply-chain attack. It should be pinned to a full SHA, e.g. `tzkhan/pr-update-action@<40-char-sha> # v1`.

Locations:

- `.github/workflows/test.yml:8`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` block and the single job `pr_update_text` also has no job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary. A minimal permissions block (e.g. `permissions: pull-requests: write`) should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned `tzkhan/pr-update-action@v1` to its full commit SHA `4cf7489d84ffcb296ea2f771a15e035bff8e3122` with the tag preserved as a comment. (2) Added a top-level `permissions:` block with `pull-requests: write` — the minimum permission required for the action to update PR titles and bodies.

