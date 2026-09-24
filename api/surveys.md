---
title: Surveys
parent: API Reference
nav_order: 4
---

# Surveys

Survey endpoints support creating, cloning, updating, deleting, launching, pausing, and inspecting Toluna Start surveys.

{: .note }
For multi-workspace API keys, include `TolunaWorkspaceID` on survey endpoints that act within a specific workspace.

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/api/v1/Surveys/Search` | Returns a paginated list of surveys. Can be filtered by status. Report links and research categories must be retrieved per survey. |
| `POST` | `/api/v1/Surveys` | Creates a survey from questionnaire structure and target details. |
| `POST` | `/api/v1/Surveys/{id}/clone` | Duplicates the survey, including questionnaire, target, and quota configuration. |
| `GET` | `/api/v1/Surveys/{id}` | Returns full survey details, questionnaire structure, and basic target information. |
| `PUT` | `/api/v1/Surveys/{id}` | Overrides an existing survey with a new structure. |
| `DELETE` | `/api/v1/Surveys/{id}` | Deletes a survey. |
| `GET` | `/api/v1/Surveys/{id}/basic` | Returns basic survey properties, status, test links, report link, and live link when applicable. |
| `GET` | `/api/v1/Surveys/{id}/billing` | Returns estimated cost, account credits, and payment history. |
| `GET` | `/api/v1/Surveys/{id}/feasibility` | Returns estimated feasibility based on expected LOI and sample requirements. |
| `PUT` | `/api/v1/Surveys/{id}/launch` | Processes payment and launches or relaunches the survey. |
| `PUT` | `/api/v1/Surveys/{id}/pause` | Places the survey on hold. |
| `GET` | `/api/v1/Surveys/{id}/fieldwork` | Returns achieved complete counts and fieldwork statistics. |
| `POST` | `/api/v1/Surveys/DecryptMedia` | Returns decrypted media links in the same order as submitted encrypted links. |
| `POST` | `/api/v1/Surveys/LocateSurveysInWorkspaces` | Returns workspace ID and location status for each submitted survey ID. |

## Search Surveys

```bash
curl --location --request POST 'https://{{TolunaDomain}}/api/v1/Surveys/Search' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "limit": 20,
    "pageOffset": 0,
    "surveyStatuses": ["Closed"]
  }'
```

## Retrieve Survey Details

Use `/basic` for status, links, and summary properties. Use the full survey endpoint when you need questionnaire structure and target details.

```bash
curl --location 'https://{{TolunaDomain}}/api/v1/Surveys/<survey ID>/basic' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>'
```

```bash
curl --location 'https://{{TolunaDomain}}/api/v1/Surveys/<survey ID>' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>'
```
