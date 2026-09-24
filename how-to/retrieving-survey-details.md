---
title: Retrieve Survey Details
parent: How-To Guides
nav_order: 3
---

# Retrieve Survey Details

Use these steps when you need survey structure details beyond the standard datamap export.

## If You Already Have the Survey ID

Use the basic endpoint for summary properties:

```bash
curl --location 'https://{{TolunaDomain}}/api/v1/Surveys/<survey ID>/basic' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <workspace ID>'
```

Use the full endpoint for questionnaire structure:

```bash
curl --location 'https://{{TolunaDomain}}/api/v1/Surveys/<survey ID>' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <workspace ID>'
```

## If You Need to Discover Surveys

1. Retrieve workspaces with `GET /api/v1/Metadata/Workspaces`.
2. For each workspace, call `POST /api/v1/Surveys/Search` with the `TolunaWorkspaceID` header.
3. For each survey of interest, call either `/basic` or the full survey details endpoint.

```json
{
  "limit": 20,
  "pageOffset": 0,
  "surveyStatuses": ["Closed"]
}
```

Some workspace names may include placeholder text for internal use and can be ignored.
