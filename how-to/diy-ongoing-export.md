---
title: Ongoing A/DIY Data Extraction
parent: How-To Guides
nav_order: 2
---

# Ongoing A/DIY Data Extraction

Use this workflow to retrieve respondent data for Toluna Start A/DIY surveys on a schedule.

## 1. Retrieve Recently Active Surveys

Activity includes survey content modification, respondent completion, or data cleanup.

```bash
curl --location --request POST 'https://api.tolunastart.com/api/v1/Reports/ChangeSet' \
  --header 'x-api-key: <your API key>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "surveyStatuses": ["Closed"],
    "fromTimestampUTC": "2024-03-05T00:00:00Z",
    "toTimeStampUTC": "2024-03-10T23:59:59Z"
  }'
```

Example response item:

```json
{
  "surveyID": 12345678,
  "lastActivityDate": "2024-03-07T05:26:17",
  "audienceType": "TolunaInfluencers",
  "surveyStatus": "Closed",
  "tolunaWorkspaceID": 99999,
  "categoryId": 104,
  "researchCategories": {
    "categoryIds": [999],
    "otherCategory": "Ad reactions testing"
  }
}
```

## 2. Start an Export for Each Survey

Use the survey ID and workspace ID from the change set.

```bash
curl --location --request POST 'https://api.tolunastart.com/api/v1/Reports/<survey ID>/startExport' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <workspace ID>' \
  --header 'Content-Type: application/json'
```

The response is an export token such as:

```text
12345678-20251201174734
```

## 3. Poll for Completion

```bash
curl --location 'https://api.tolunastart.com/api/v1/Reports/<export token>' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <workspace ID>'
```

Poll until `exportStatus` is `Complete` and `exportURL` is populated.

## 4. Download the Export

Download the JSON file from `exportURL`. Exported files are retained for one month.

## Metadata Lookups

Use Metadata endpoints to map IDs to names:

- `GET /api/v1/Metadata/Categories`
- `GET /api/v1/Metadata/ResearchCategories`
- `GET /api/v1/Metadata/Workspaces`
