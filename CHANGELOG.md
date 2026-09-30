# Changelog

All notable changes to this bundle are recorded here. Versions follow semantic versioning: major for a
removed or renamed endpoint or a layout change, minor for additions, patch for corrections.

## Unreleased

### Fixed

- **`generated.by` is now present on every concept.** OKF v0.2 §5.2 marks `by` as required inside
  `generated`, and §5.3 derives the trust tier from the actor prefix, but the bundle emitted
  `generated.at` alone and `tools/validate.py` actively rejected `generated.by` as if it were
  forbidden. The check was inverted: it now requires `generated.by` and validates that it, and every
  other actor, matches an OKF §7 form (`<producer>/<version>`, `human:<id>` or `process:<id>`). All
  407 concepts and `v2/manifest.json` now carry `generated.by: process:build_okf`. The generator in
  the maintainer repository must be updated to emit it.
- Dead links in `README.md`: the clone URL pointed at `github.com/zoho/analytics-okf` and the
  canonical-copy footer at `zoho.com/analytics/api/v2/okf`, both of which 404.
- `v2/how-to-use-this-bundle.md` referred to `tools/validate_okf.py`; the validator is
  `tools/validate.py`.

### Changed

- **Root `manifest.json` states the version contract explicitly** (`schema_version` 1.1). Added
  `latest_path` so a consumer can resolve the current bundle without joining strings, a `resolution`
  note, a `status_vocabulary` defining `beta`/`stable`/`deprecated`/`sunset`, per-version
  `deprecated_on`, `sunset_on` and `superseded_by` fields, an `okf_spec` link and a per-version
  `api_reference` link. No existing key changed meaning.
- CI additionally checks that `latest_path` agrees with `latest`, that every `status` is in the
  vocabulary, that `latest` is neither deprecated nor sunset, and that a deprecated or sunset version
  carries `deprecated_on` and a `superseded_by` that names a listed version.
- `README.md` is no longer written as if the repository held only v2. It leads with the two
  unversioned entry points, marks the `v2/` URLs as the pin-deliberately case, documents the
  lifecycle vocabulary and the deprecation path, and records OKF conformance clause by clause
  including the one deliberate deviation from §6.1 (document-relative body links).
- `llms.txt` states the "use `latest` unless pinned" rule in its body rather than in the `## Optional`
  section, whose defined meaning is "links an agent may skip when short on context". `## Optional`
  now holds the changelog, log and licence, which are genuinely skippable.

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

- Replace `.../main/okf/<path>` with `.../main/v2/<path>` in any pinned raw URL. The bundle
  content at the new path is byte-identical, so nothing but the prefix changes.

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
