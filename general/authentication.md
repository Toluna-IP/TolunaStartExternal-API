---
title: Authentication
parent: General
nav_order: 3
---

# Authentication

Requests authenticate with customer-specific headers.

| Header | Required | Purpose |
| --- | --- | --- |
| `x-api-key` | Yes | Primary API key assigned by Toluna. |
| `TolunaWorkspaceID` | Required for some requests | Selects the workspace for calls made with a multi-workspace API key. |

{: .warning }
If an API key is associated with multiple workspaces and a workspace-specific endpoint is called without `TolunaWorkspaceID`, the API can return `401 Unauthorized`.

## Example Request

```bash
curl --location --request POST 'https://{{TolunaDomain}}/api/v1/Surveys/Search' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "limit": 20,
    "pageOffset": 0,
    "surveyStatuses": ["Closed"]
  }'
```

## Swagger Security Schemes

The OpenAPI spec also lists additional API-key headers used by the service, including `SF_ROOT_ID`, `SU_TOKEN`, and `ClientConfig`. Customer integrations should use the headers provided by Toluna for their account.
