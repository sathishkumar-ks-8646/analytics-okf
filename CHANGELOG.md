# Changelog

All notable changes to this bundle are recorded here. Versions follow semantic versioning: major for a
removed or renamed endpoint or a layout change, minor for additions, patch for corrections.

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
