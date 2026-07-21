# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) presets for my repos.

## Usage

In a repo's `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>modem7/renovate-config"]
}
```

This resolves to [`default.json`](default.json), which pulls in [`shared.json`](shared.json) —
the common baseline: `config:recommended`, assignee/label/timezone, GitHub Action digest pinning,
Dockerfile digest pinning, and automerge for low-risk CI plumbing updates.

## Optional extras

Add these alongside the default extend when a repo needs them:

- `github>modem7/renovate-config:docker` — for repos with a Dockerfile using s6-overlay and
  `ARG ALPINE_VERSION` / `ARG PYTHON_VERSION` pins.
- `github>modem7/renovate-config:automergePatch` — automerge patch updates, not just digests.
- `github>modem7/renovate-config:automergeDigest` — automerge digest updates outside office hours
  (already included via `automergePatch`).

Repo-specific rules (e.g. version pins, path exclusions) belong in that repo's own
`renovate.json`, extending this config rather than duplicating it.

## Repo scaffolding

This repo also carries the same `.github` scaffolding as my other repos:

- `settings.yml` — repository metadata + the standard label set, applied by the
  [Repository Settings App](https://github.com/apps/settings)
- `workflows/autoassign.yml` — assigns new issues to `modem7`
- `workflows/test.yml` — validates every preset file with `renovate-config-validator`
- `CODEOWNERS`, `FUNDING.yml` — same as elsewhere
