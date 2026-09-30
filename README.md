# Zoho Analytics REST API v2 - Open Knowledge Format bundle

Machine-readable, agent-friendly knowledge base for the [Zoho Analytics REST API v2](https://www.zoho.com/analytics/api/v2/).
It packages every public endpoint, the conventions they share, and their error codes, OAuth scopes
and permissions as an [Open Knowledge Format](https://github.com/GoogleCloudPlatform/open-knowledge-format)
(OKF v0.2) bundle: a directory of markdown files with YAML frontmatter.

**Bundle version 1.0.0** - 168 endpoints, 10 domains, 33 groups,
278 error codes, 31 OAuth scopes, 8 workflow playbooks,
166 SDK example documents in 9 languages.

This is documentation, not a client library. For the SDKs themselves see the
[Zoho Analytics API documentation](https://www.zoho.com/analytics/api/v2/).

## Quick start

**For an AI assistant or agent.** Point it at [`llms.txt`](https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/llms.txt) and let it follow the links.
Inside the bundle, links between documents are relative to the linking document, so they resolve both on GitHub and in a local clone.

```
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/llms.txt                                  curated entry point, lists every version
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/manifest.json                             version index for tooling
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/v2/manifest.json                         version, counts, entry points
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/v2/overview.md                           what the API is, five shared conventions
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/v2/how-to-use-this-bundle.md             frontmatter contract and navigation rules
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/v2/references/endpoint-catalog.json      every endpoint, machine-readable
```

**For a human.** Start at [`v2/overview.md`](v2/overview.md), then
[`v2/endpoint-catalog.md`](v2/endpoint-catalog.md) to find an endpoint, then the endpoint document.

**For tooling** such as SDK generators, Postman collections and MCP servers. Read
[`v2/references/endpoint-catalog.json`](v2/references/endpoint-catalog.json) for the inventory and
[`v2/references/openapi/`](v2/references/openapi/) for request and response schemas.

```bash
git clone https://github.com/zoho/analytics-okf.git
```

## Repository layout

Each Zoho Analytics REST API version is a self-contained OKF bundle in its own top-level
directory. The two root files route agents and tooling to the right one.

| Path | Contents |
|---|---|
| `llms.txt` | AI agent entry point. Lists every available API version and links to each one. |
| `manifest.json` | Machine-readable version index. Read this rather than hard-coding a version directory. |
| `v2/` | The Zoho Analytics REST API **v2** bundle: current and stable. |
| `tools/` | Maintainer tooling. Shared across versions. |

### Inside a version bundle (`v2/`)

| Path | Contents |
|---|---|
| `v2/index.md` | Bundle root. Declares `okf_version`. Lists everything below. |
| `v2/overview.md` | What the API is, the object model, the five conventions every call shares. |
| `v2/how-to-use-this-bundle.md` | Directory layout, the `api:` frontmatter contract, navigation rules for agents. |
| `v2/endpoint-catalog.md` | All 168 endpoints in one table. |
| `v2/foundations/` | Rules shared by every call: authentication, data centers, request conventions and CONFIG encoding, response envelope, HTTP statuses, error catalog, OAuth scopes, roles and permissions, permission matrix, identifiers, filter criteria syntax, asynchronous jobs, rate limits, export and import enumerations, White Label, glossary, SDK clients. |
| `v2/domains/` | One document per domain, per API group and per endpoint. |
| `v2/workflows/` | Step-by-step playbooks for multi-endpoint tasks. |
| `v2/sdk-examples/` | Code samples per endpoint in cURL, C#, Go, Java, PHP, Python, Node.js, Ruby and Deluge. |
| `v2/references/` | The OpenAPI 3 specifications and the machine-readable endpoint catalog. |
| `v2/manifest.json` | Bundle name, version, OKF version, counts and entry points. |
| `v2/llms.txt` | Curated entry point for this version, with the full link list. |

## How the documents are structured

Every endpoint document carries an `api:` block in its frontmatter so tools never have to parse prose:

```yaml
type: API Endpoint
title: Share Views
api:
  operation_id: shareViews
  method: POST
  path: /restapi/v2/workspaces/{workspace-id}/share
  oauth_scopes: [ZohoAnalytics.share.create]
  org_id_header: required
  config_parameter: { location: form, required: true }
  success_status: 204
  error_codes: [7301, 7307, 7320]
  openapi: { file: /references/openapi/share-publish-grouped-api.json, pointer: "#/paths/..." }
```

The body always uses the same H1 sections in the same order: Summary, Endpoint, Request, Response,
Examples, Notes and Behaviour, Error Codes, Related. Full contract in
[`v2/how-to-use-this-bundle.md`](v2/how-to-use-this-bundle.md).

## Versions

Each API version ships as a self-contained OKF bundle in its own top-level directory.
Adding a version never moves an existing one.

| Version | Status | Path | Manifest |
|---|---|---|---|
| v2 | stable | [`v2/`](v2/index.md) | [`v2/manifest.json`](v2/manifest.json) |

V3 will be added under `v3/` when available. Tools should read the root
[`manifest.json`](manifest.json) and follow `versions[].path` rather than assuming `v2/`.

## Versioning

Two version numbers are in play and they move independently.

- The **API version** is the directory name: `v2/`. It changes only when Zoho ships a new REST API version.
- The **bundle version** is semantic versioning applied to the documentation itself, recorded in
  `v<N>/manifest.json`. Each version directory carries its own.

Bundle version bumps within a single API version:

| Change | Bump |
|---|---|
| An endpoint is removed or renamed, or the layout inside the bundle changes | major |
| Endpoints, scopes or documents are added | minor |
| Content corrections and clarifications | patch |

Pin a version by cloning a tag or downloading the release tarball. `main` always holds the newest bundle.

Moving the bundle from `okf/` to `v2/` was a repository-layout change, not a bundle change: no
document, link or frontmatter path was altered, so the v2 bundle version stays 1.0.0. Raw URLs
pinned to the old `okf/` path remain resolvable at the `layout-okf-v1` tag.

## Provenance and trust

Concepts are derived from the Zoho Analytics API reference documents and the OpenAPI specifications
shipped in `v2/references/openapi/`. Each concept records `generated.at` and, where applicable,
`sources`. No concept carries a `verified` entry yet, so the bundle's OKF trust tier is **unverified**:
content is faithful to the source documents but has not been re-confirmed against the live service.
Reviewers should add `verified` entries to the concepts they check.

## Feedback and contributions

Open an issue for anything wrong, missing or ambiguous. Include the bundle version from
`v2/manifest.json` and the path of the document.

If you send a pull request, run the validator first. It is the same check that CI runs, and it is the
only thing in this repository aimed at maintainers rather than consumers. You do not need it to *use*
the bundle.

```bash
python3 tools/validate.py        # finds the newest v<N>/ automatically; needs Python 3.8+, no dependencies
```

It verifies OKF v0.2 conformance, that no `resource` points outside the bundle, and that every internal
link and anchor resolves. It exits non-zero on any error.

## Licence

See [LICENSE.md](LICENSE.md).

---

Canonical copies: [https://github.com/zoho/analytics-okf](https://github.com/zoho/analytics-okf) and [https://www.zoho.com/analytics/api/v2/okf](https://www.zoho.com/analytics/api/v2/okf).
