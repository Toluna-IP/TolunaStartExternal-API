---
title: Schema Reference
parent: Swagger and Schemas
nav_order: 2
---

# Schema Reference

This page summarizes the most useful objects from the OpenAPI spec. For the complete schema set, use the local OpenAPI JSON or hosted Swagger UI.

## Common Response Schemas

### `WorkSpaceInfo`

| Property | Type | Notes |
| --- | --- | --- |
| `id` | number | Workspace ID. |
| `name` | string | Workspace name. |

### `BasicSurvey`

| Property | Type | Notes |
| --- | --- | --- |
| `surveyId` | number | Survey ID. |
| `title` | string | Respondent-facing title. |
| `internalTitle` | string | Internal title. |
| `testLink` | string | Test link. |
| `status` | `SurveyStatus` | `Pending`, `Open`, `Closed`, `Paused`, or `Scheduled`. |
| `reportLink` | string | Shared report link when available. |
| `liveLink` | string | Own-audience live link when available. |
| `creatorUser` | string | Creator user. |
| `cultures` | string array | Survey cultures. |
| `questionnaireType` | `QuestionnaireType` | Questionnaire type. |
| `audienceType` | `AudienceType` | Audience type. |
| `researchCategories` | `TqsResearchCategories` | Research category IDs and custom category text. |
| `targetCompletes` | number | Target completes. |
| `createdDate` | date-time string | Creation timestamp. |
| `categoryId` | number | Category ID. |
| `dataCleanupStatus` | `DataCleanupStatus` | Cleanup status. |

### `ChangeSet`

| Property | Type | Notes |
| --- | --- | --- |
| `surveyID` | number | Survey ID. |
| `title` | string | Survey title. |
| `internalTitle` | string | Internal title. |
| `lastActivityDate` | date-time string | Last activity timestamp. |
| `audienceType` | `AudienceType` | Audience type. |
| `surveyStatus` | `SurveyStatus` | Survey status. |
| `tolunaWorkspaceID` | number | Workspace ID to use for follow-up export calls. |
| `categoryId` | number | Category ID. |
| `dataCleanupStatus` | `DataCleanupStatus` | Cleanup status. |
| `researchCategories` | `ResearchCategories` | Research category IDs and custom category text. |

### `ReportExportResult`

| Property | Type | Notes |
| --- | --- | --- |
| `surveyId` | number | Survey ID. |
| `exportStatus` | `ExportStatus` | Export status. |
| `exportURL` | string | Populated when export is complete. |

## Request Schemas

### `SearchSurveysInputModel`

```json
{
  "limit": 20,
  "pageOffset": 0,
  "surveyStatuses": ["Closed"]
}
```

### `ChangeSetQuery`

```json
{
  "surveyStatuses": ["Open", "Paused", "Closed"],
  "fromTimestampUTC": "2024-03-01T00:00:00Z",
  "toTimeStampUTC": "2024-03-07T23:59:59Z"
}
```

### `FullServiceChangeSetQuery`

```json
{
  "fromTimestampUTC": "2024-03-01T00:00:00Z",
  "toTimeStampUTC": "2024-03-07T23:59:59Z"
}
```

### `StartExportIncludeAttributesModel`

```json
{
  "includeAttributes": ["1001007", "1001107_7"]
}
```

## Survey Creation Root Schema

The `Survey` schema is the root object for survey create, update, and detail responses.

| Property | Type | Notes |
| --- | --- | --- |
| `surveyId` | number | Survey ID. |
| `audience` | `Audience` | Audience type, target completes, country/culture, incidence rate, and exclusions. |
| `category` | number | Category ID. |
| `researchCategories` | `TqsResearchCategories` | Research category IDs and optional custom category. |
| `questionnaire` | `QuestionnaireStructure` | Questionnaire metadata, blocks, filters, quotas, scripts, and respondent experience settings. |

## Enumerations

| Schema | Values |
| --- | --- |
| `SurveyStatus` | `Pending`, `Open`, `Closed`, `Paused`, `Scheduled` |
| `QuestionnaireType` | `CUSTOM_SURVEY`, `CONCEPT_TESTING`, `PACKAGE_TESTING`, `BRAND_HEALTH`, `COMMS_POST_LAUNCH`, `COMMS_PRE_LAUNCH` |
| `MediaType` | `VIDEO`, `IMAGE`, `AUDIO`, `TEXT` |
| `SurveyLocationStatus` | `Found`, `Unavailable` |
