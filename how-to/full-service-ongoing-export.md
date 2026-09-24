---
title: Ongoing Full Service Data Extraction
parent: How-To Guides
nav_order: 5
---

# Ongoing Full Service Data Extraction

Use this workflow to retrieve respondent data for eligible Toluna Full Service surveys scripted in ConfirmIT and fielded by Toluna.

## 1. Retrieve Recently Active Surveys

Filtering by survey status is not available for Full Service change sets.

```bash
curl --location --request POST 'https://{{TolunaDomain}}/api/v1/Reports/FullService/ChangeSet' \
  --header 'x-api-key: <your API key>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
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
  "tolunaWorkspaceID": 99999
}
```

## 2. Start an Export

```bash
curl --location --request POST 'https://{{TolunaDomain}}/api/v1/Reports/FullService/<survey ID>/startExport' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <workspace ID>' \
  --header 'Content-Type: application/json'
```

## 3. Poll for Completion

```bash
curl --location 'https://{{TolunaDomain}}/api/v1/Reports/FullService/<export token>' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <workspace ID>'
```

Poll until the response includes `exportStatus: "Complete"` and an `exportURL`.

## Notes

- Maximum timeframe for a single change set is 7 days.
- Daily exports covering the last 24 hours or less are recommended for ongoing integrations.
- Category, research category, and survey status information are not available for Full Service studies in the API.
- Overwrite local data copies for every survey appearing in the change set to keep downstream storage consistent with Toluna systems.
