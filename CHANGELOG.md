# Changelog

All notable changes to this bundle are recorded here. Versions follow semantic versioning: major for a
removed or renamed endpoint or a layout change, minor for additions, patch for corrections.

## Unreleased

### Changed

- **Repository layout.** The bundle moved from `okf/` to `v2/` so future API versions can live
  alongside it in the same repository. Bundle content is byte-identical: no document, link or
  frontmatter path changed. The v2 bundle version remains 1.0.0.
- `llms.txt` at the repository root is now a version router. The full V2 link list moved to
  `v2/llms.txt`.
- `tools/validate.py` discovers `v<N>/` bundle directories instead of a hardcoded `okf/`, and CI
  validates every `v*/` directory, so adding `v3/` needs no further change.

### Added

- Root `manifest.json`: a machine-readable index of every available API version, its status and its
  bundle manifest. Tools should read this instead of hard-coding `v2/`.
- A CI check that the root `manifest.json` stays in sync with the version directories on disk.

### Migration

- Replace `.../main/okf/<path>` with `.../main/v2/<path>` in any pinned raw URL.
- The pre-move layout stays reachable at the `layout-okf-v1` tag: substitute `main` with
  `layout-okf-v1` in an old URL to resolve it unchanged.

## 1.0.0 - 2026-09-16

### Added

- First public release of the Zoho Analytics REST API v2 Open Knowledge Format bundle (OKF v0.2).
- 168 endpoint concepts across 10 domains and 33 API groups.
- Foundations covering authentication, data centers, request conventions, response envelope, HTTP statuses,
  OAuth scopes, roles and permissions, the permission matrix, identifiers, filter criteria syntax,
  asynchronous jobs, rate limits and quotas, export and import enumerations, White Label behaviour,
  the glossary and SDK clients.
- Error catalog with 278 codes plus a compact quick reference.
- 8 workflow playbooks for multi-endpoint tasks.
- 166 SDK example documents covering 9 languages.
- Machine-readable `manifest.json` and `references/endpoint-catalog.json`, and the OpenAPI 3 specifications.

### Known limitations

- Trust tier is `unverified`: no concept carries a `verified` entry yet.
- Two endpoints, Fetch All Embed URLs and Delete Embed URL, are documented from the API reference only.
  They are absent from the OpenAPI specifications and their documents say so.
