---
title: Reports
parent: API Reference
nav_order: 3
---

# Reports

Reports endpoints support raw respondent data extraction for Toluna Start A/DIY surveys and eligible Full Service surveys.

## A/DIY Survey Reports

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/api/v1/Reports/ChangeSet` | Returns surveys with activity during a specified time period. Can be filtered by survey status. |
| `POST` | `/api/v1/Reports/{id}/startExport` | Starts raw data export for a survey and returns an export token. |
| `GET` | `/api/v1/Reports/{exportToken}` | Returns export status and the generated file URL when available. |
| `POST` | `/api/v1/Reports/GetOriginalMediaUrl` | Returns a decrypted original media URL for an encrypted media link. |

## Full Service Reports

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/api/v1/Reports/FullService/ChangeSet` | Returns Full Service surveys with activity during a specified time period. Status filtering is not supported for Full Service extraction. |
| `POST` | `/api/v1/Reports/FullService/{id}/startExport` | Starts raw data export for a Full Service survey and returns an export token. |
| `GET` | `/api/v1/Reports/FullService/{exportToken}` | Returns export status and the generated file URL when available. |

## Change Set Limits

- Maximum timeframe for a single change set is 7 days.
- The earliest accepted `fromTimestampUTC` is 30 days before the current date.
- Smaller ranges improve performance for ongoing integrations.
- For ongoing extraction, run daily exports covering the last 24 hours or less.

{: .note }
The live OpenAPI schema names the end timestamp field `toTimeStampUTC`. Some older examples may show `toTimestampUTC`; use the casing expected by your API version.

## Start A/DIY Export

```bash
curl --location --request POST 'https://{{TolunaDomain}}/api/v1/Reports/<survey ID>/startExport' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "includeAttributes": ["1001007", "1001107_7"]
  }'
```

`includeAttributes` is optional. When provided, it limits the export to the selected demographic attribute IDs.

## Poll Export Status

```bash
curl --location 'https://{{TolunaDomain}}/api/v1/Reports/<export token>' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>'
```

Example response:

```json
{
  "surveyId": 12345678,
  "exportStatus": "Complete",
  "exportURL": "https://tsapi-exports-prod.s3.amazonaws.com/12345678/12345678-20251201174734.json?AWS..."
}
```

Exported files are retained for one month. After that, start a new export.
