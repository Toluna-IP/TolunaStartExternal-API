---
title: Quick Start
parent: General
nav_order: 1
---

# Quick Start

Use this page as the shortest path from API access to a working integration.

## 1. Get Credentials

Request API access from Toluna. Each API request must include an `x-api-key` header. Some requests also require `TolunaWorkspaceID`, especially when one API key is linked to multiple workspaces.

## 2. Confirm Connectivity

Call the Health endpoints:

```bash
curl --location 'https://api.tolunastart.com/api/v1/Ping' \
  --header 'x-api-key: <your API key>'
```

```bash
curl --location 'https://api.tolunastart.com/api/v1/Version' \
  --header 'x-api-key: <your API key>'
```

## 3. Discover Workspaces

```bash
curl --location 'https://api.tolunastart.com/api/v1/Metadata/Workspaces' \
  --header 'x-api-key: <your API key>'
```

If the response includes multiple workspaces, include `TolunaWorkspaceID` on workspace-specific requests.

## 4. Find Surveys

```bash
curl --location --request POST 'https://api.tolunastart.com/api/v1/Surveys/Search' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "limit": 20,
    "pageOffset": 0,
    "surveyStatuses": ["Closed"]
  }'
```

## 5. Export Respondent Data

For ongoing integrations, use the Reports change set endpoint to identify surveys with recent activity, then start an export for each returned survey and poll the export token until the file URL is available.

See [Ongoing A/DIY Data Extraction]({{ site.baseurl }}/how-to/diy-ongoing-export/) and [Ongoing Full Service Data Extraction]({{ site.baseurl }}/how-to/full-service-ongoing-export/) for complete workflows.
