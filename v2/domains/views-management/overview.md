---
type: API Domain
title: Views Management
description: "API for Views Management in Zoho Analytics — covering view operations, auto analysis, favorites, and trash management."
tags:
  - zoho-analytics
  - rest-api-v2
  - views-management
  - api-domain
api:
  domain: views-management
  groups:
    - group: view-operations
      title: View Operations
      doc: "/domains/views-management/view-operations/overview.md"
      endpoint_count: 10
    - group: view-preferences
      title: View Preferences
      doc: "/domains/views-management/view-preferences/overview.md"
      endpoint_count: 2
    - group: trash-management
      title: Trash Management
      doc: "/domains/views-management/trash-management/overview.md"
      endpoint_count: 3
    - group: auto-analysis
      title: Auto Analysis
      doc: "/domains/views-management/auto-analysis/overview.md"
      endpoint_count: 2
  endpoint_count: 17
  openapi: "/references/openapi/views-management-grouped-api.json"
sources:
  - id: openapi-spec
    resource: "/references/openapi/views-management-grouped-api.json"
    title: OpenAPI 3 specification - views-management-grouped-api.json
    author: team:zoho-analytics-api-docs
    last_modified: 2026-09-10T10:56:21Z
generated:
  at: 2026-09-16T07:44:37Z
status: stable
---

# Summary

API for Views Management in Zoho Analytics — covering view operations, auto analysis, favorites, and trash management.

# API Groups

| Group | Endpoints | Description |
|---|---|---|
| [View Operations](view-operations/overview.md) | 10 | APIs for creating, copying, renaming, deleting, and retrieving views. |
| [View Preferences](view-preferences/overview.md) | 2 | APIs to mark a view as a favorite for the authenticated user and to remove it from the favorites list. |
| [Trash Management](trash-management/overview.md) | 3 | APIs to list the views available in the trash of a workspace, restore a trashed view back to the workspace, and permanently delete a view from the trash. |
| [Auto Analysis](auto-analysis/overview.md) | 2 | APIs to automatically generate a curated set of views - charts, pivot tables and summary views - from an entire table or from a single column of it. |

# Endpoints

| Endpoint | Method | Path | Operation ID | OAuth scope | Success |
|---|---|---|---|---|---|
| [Save As View](view-operations/save-as-view.md) | POST | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/saveas` | `saveAsView` | `ZohoAnalytics.modeling.create` | 200 |
| [Copy Views](view-operations/copy-views.md) | POST | `/restapi/v2/workspaces/{workspace-id}/views/copy` | `copyViews` | `ZohoAnalytics.modeling.create` | 200 |
| [Create Similar Views](view-operations/create-similar-views.md) | POST | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/similarviews` | `createSimilarViews` | `ZohoAnalytics.modeling.create` | 204 |
| [Rename View](view-operations/rename-view.md) | PUT | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}` | `renameView` | `ZohoAnalytics.modeling.update` | 204 |
| [Delete View](view-operations/delete-view.md) | DELETE | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}` | `deleteView` | `ZohoAnalytics.modeling.delete` | 204 |
| [Get View List](view-operations/get-views.md) | GET | `/restapi/v2/workspaces/{workspace-id}/views` | `getViews` | `ZohoAnalytics.metadata.read` | 200 |
| [Get View Details](view-operations/get-view-details.md) | GET | `/restapi/v2/views/{view-id}` | `getViewDetails` | `ZohoAnalytics.metadata.read` | 200 |
| [Get View URL](view-operations/get-view-url.md) | GET | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/publish` | `getViewUrl` | `ZohoAnalytics.embed.read` | 200 |
| [Get View Dependents](view-operations/get-view-dependents.md) | GET | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/dependents` | `getViewDependents` | `ZohoAnalytics.metadata.read` | 200 |
| [Get Recent Views](view-operations/get-recent-views.md) | GET | `/restapi/v2/recentviews` | `getRecentViews` | `ZohoAnalytics.metadata.read` | 200 |
| [Add Favourite View](view-preferences/add-favorite-view.md) | POST | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/favorite` | `addFavoriteView` | `ZohoAnalytics.metadata.update` | 204 |
| [Remove Favourite View](view-preferences/remove-favorite-view.md) | DELETE | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/favorite` | `removeFavoriteView` | `ZohoAnalytics.metadata.update` | 204 |
| [Get Trash Views](trash-management/get-trash-views.md) | GET | `/restapi/v2/workspaces/{workspace-id}/trash` | `getTrashViews` | `ZohoAnalytics.metadata.read` | 200 |
| [Restore Trash View](trash-management/restore-trash-view.md) | POST | `/restapi/v2/workspaces/{workspace-id}/trash/{view-id}` | `restoreTrashView` | `ZohoAnalytics.modeling.create` | 204 |
| [Delete Trash View](trash-management/delete-trash-view.md) | DELETE | `/restapi/v2/workspaces/{workspace-id}/trash/{view-id}` | `deleteTrashView` | `ZohoAnalytics.modeling.delete` | 204 |
| [Auto Analyse View](auto-analysis/auto-analyse-view.md) | POST | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/autoanalyse` | `autoAnalyseView` | `ZohoAnalytics.modeling.create` | 200 |
| [Auto Analyse Column](auto-analysis/auto-analyse-column.md) | POST | `/restapi/v2/workspaces/{workspace-id}/views/{view-id}/columns/{column-id}/autoanalyse` | `autoAnalyseColumn` | `ZohoAnalytics.modeling.create` | 200 |

# Related

- [All domains](../index.md)
- [OpenAPI specification for this domain](../../references/openapi/views-management-grouped-api.json)
- [Foundations](../../foundations/index.md)
