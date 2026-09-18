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
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/llms.txt                                  curated entry point
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/okf/manifest.json                         version, counts, entry points
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/okf/overview.md                           what the API is, five shared conventions
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/okf/how-to-use-this-bundle.md             frontmatter contract and navigation rules
https://raw.githubusercontent.com/sathishkumar-ks-8646/analytics-okf/main/okf/references/endpoint-catalog.json      every endpoint, machine-readable
```

**For a human.** Start at [`okf/overview.md`](okf/overview.md), then
[`okf/endpoint-catalog.md`](okf/endpoint-catalog.md) to find an endpoint, then the endpoint document.

**For tooling** such as SDK generators, Postman collections and MCP servers. Read
[`okf/references/endpoint-catalog.json`](okf/references/endpoint-catalog.json) for the inventory and
[`okf/references/openapi/`](okf/references/openapi/) for request and response schemas.

```bash
git clone https://github.com/zoho/analytics-okf.git
```

## What is in the bundle

| Path | Contents |
|---|---|
| `okf/index.md` | Bundle root. Declares `okf_version`. Lists everything below. |
| `okf/overview.md` | What the API is, the object model, the five conventions every call shares. |
| `okf/how-to-use-this-bundle.md` | Directory layout, the `api:` frontmatter contract, navigation rules for agents. |
| `okf/endpoint-catalog.md` | All 168 endpoints in one table. |
| `okf/foundations/` | Rules shared by every call: authentication, data centers, request conventions and CONFIG encoding, response envelope, HTTP statuses, error catalog, OAuth scopes, roles and permissions, permission matrix, identifiers, filter criteria syntax, asynchronous jobs, rate limits, export and import enumerations, White Label, glossary, SDK clients. |
| `okf/domains/` | One document per domain, per API group and per endpoint. |
| `okf/workflows/` | Step-by-step playbooks for multi-endpoint tasks. |
| `okf/sdk-examples/` | Code samples per endpoint in cURL, C#, Go, Java, PHP, Python, Node.js, Ruby and Deluge. |
| `okf/references/` | The OpenAPI 3 specifications and the machine-readable endpoint catalog. |
| `okf/manifest.json` | Bundle name, version, OKF version, counts and entry points. |

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
[`okf/how-to-use-this-bundle.md`](okf/how-to-use-this-bundle.md).

## Versioning

Bundle versions follow semantic versioning, independent of the API version, which is always v2.

| Change | Bump |
|---|---|
| An endpoint is removed or renamed, or the bundle layout changes | major |
| Endpoints, scopes or documents are added | minor |
| Content corrections and clarifications | patch |

Pin a version by cloning a tag or downloading the release tarball. `main` always holds the newest bundle.

## Provenance and trust

Concepts are derived from the Zoho Analytics API reference documents and the OpenAPI specifications
shipped in `okf/references/openapi/`. Each concept records `generated.at` and, where applicable,
`sources`. No concept carries a `verified` entry yet, so the bundle's OKF trust tier is **unverified**:
content is faithful to the source documents but has not been re-confirmed against the live service.
Reviewers should add `verified` entries to the concepts they check.

## Feedback and contributions

Open an issue for anything wrong, missing or ambiguous. Include the bundle version from
`okf/manifest.json` and the path of the document.

If you send a pull request, run the validator first. It is the same check that CI runs, and it is the
only thing in this repository aimed at maintainers rather than consumers. You do not need it to *use*
the bundle.

```bash
python3 tools/validate.py        # finds okf/ automatically; needs Python 3.8+, no dependencies
```

It verifies OKF v0.2 conformance, that no `resource` points outside the bundle, and that every internal
link and anchor resolves. It exits non-zero on any error.

## Licence

See [LICENSE.md](LICENSE.md).

---

Canonical copies: [https://github.com/zoho/analytics-okf](https://github.com/zoho/analytics-okf) and [https://www.zoho.com/analytics/api/v2/okf](https://www.zoho.com/analytics/api/v2/okf).
