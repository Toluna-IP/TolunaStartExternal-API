---
title: Metadata
parent: API Reference
nav_order: 2
---

# Metadata

Metadata endpoints return lookup values that support survey discovery, survey creation, and report interpretation.

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/api/v1/Metadata/Categories` | Retrieves category ID to category title mappings. |
| `GET` | `/api/v1/Metadata/ResearchCategories` | Retrieves research category ID to title mappings. |
| `GET` | `/api/v1/Metadata/Cultures` | Retrieves culture ID to ISO culture code mappings. |
| `GET` | `/api/v1/Metadata/Workspaces` | Retrieves workspaces linked to the API key. Workspace IDs are required for workspace-scoped calls. |

## Workspaces

Use this endpoint early in an integration to determine whether `TolunaWorkspaceID` is needed for subsequent calls.

```text
curl --location 'https://{{TolunaDomain}}/api/v1/Metadata/Workspaces' \
  --header 'x-api-key: <your API key>'
```

Response objects use the `WorkSpaceInfo` schema:

```json
{
  "id": 99999,
  "name": "Workspace name"
}
```

## Categories and Research Categories

Use category and research category metadata to translate IDs returned from survey search, survey details, change sets, and export datamaps into human-readable names.
