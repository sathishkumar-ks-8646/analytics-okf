# Bundle Update Log

## 2026-09-30
* **Fix**: Filled the empty `api.permission_required` of ten endpoints in Synchronous Data Export, Asynchronous Data Export and Data Sync & Connectivity, and the ten matching rows of [Permission matrix](foundations/permission-matrix.md), which had rendered as `-`. The values were taken from each group's own **Permission Model** table.
* **Creation**: Added [Custom roles](foundations/custom-roles.md) - the three access permission levels, the permission catalogue by category, the mapping onto this bundle's permission vocabulary, and how a custom role name reaches the API. Derived from the Zoho Analytics help documentation, not the API reference; the document says so in its body.

## 2026-09-16
* **Creation**: Generated the Zoho Analytics REST API v2 OKF v0.2 bundle from the markdown reference docs, OpenAPI specifications and SDK samples in `api-docs/`: 168 endpoint concepts across 10 domains and 33 groups, 166 SDK example concepts, an error catalog with 278 codes, and the shared foundations (authentication, conventions, scopes, roles, identifiers, criteria syntax, asynchronous jobs, rate limits, white label, glossary).
* **Note**: Content is machine-generated from the source documents listed in each concept's `sources`. Add `verified` entries after human review.
