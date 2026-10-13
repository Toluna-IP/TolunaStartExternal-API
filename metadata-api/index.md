---
title: Metadata API
nav_order: 3
---

# Metadata API

The following endpoints allow for the retrieval of supporting information related to key concepts, such as available cultures and categories.

| Endpoint | Description |
| --- | --- |
| `GET /Metadata/Categories` | Retrieves the mapping between category IDs and their human-readable titles. |
| `GET /Metadata/Cultures` | Retrieves the mapping between culture ID and its corresponding ISO code. |
| `GET /Metadata/ResearchCategories` | Retrieves the human-readable title corresponding to a research category ID. |
| `GET /Metadata/Workspaces` | Retrieves a list of ID/name pairs for all DIY survey workspaces linked to the provided API key. The Workspace ID is essential for authorization when accessing specific endpoints that operate within the scope of a particular survey or workspace. |

