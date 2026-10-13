---
title: Data Extraction API
nav_order: 5
---

# Data Extraction API
{: .no_toc }

The Toluna API offers two distinct collections of endpoints for downloading raw respondent data from surveys:

1. Toluna Start Surveys: Used for exporting data from A/DIY surveys fielded within the Toluna Start platform. Data is available for surveys fielded within the last two years.
2. Full-Service Surveys: Used for exporting data from full-service projects that were scripted in ConfirmIT and fielded by Toluna on behalf of the client. The availability of this data is subject to the data retention contract policy within Toluna Analytics.

* TOC
{:toc}

## A/DIY Surveys - Toluna Start

| Endpoint | Description |
| --- | --- |
| `POST /reports/changeSet` | Designed for routine data retrieval, such as daily retrieval, and returns a list of surveys that have been active within a specified time period. The response includes the survey ID, associated workspace ID, and core survey properties. You can optionally filter by survey status. Surveys with `Pending` or `Scheduled` statuses are excluded because they do not yet contain respondent data. The `TolunaWorkspaceID` header is optional. If provided, changes are limited to the specified workspace; otherwise, results cover all workspaces linked to your API key. The maximum timeframe for a single changeset is 7 days. The earliest acceptable `fromTimestampUTC` date is 30 days prior to the current date. |
| `POST /reports/{surveyId}/startExport` | Initiates a raw data export and returns a unique token to track the process. The export status can be checked using the subsequent API with the returned token. Once complete, the API returns a URL to the generated file. The endpoint supports an optional `includeAttributes` parameter for exporting only a specified subset of demographic attributes. For API keys associated with multiple workspaces, the `TolunaWorkspaceID` header is mandatory. |
| `GET /reports/exportByToken` | Retrieves the status of a raw data export using a provided token and returns the URL to the generated file once available. Exported files are only retained for one month; after this period, a new export must be initiated. If the API key is associated with multiple workspaces, the `TolunaWorkspaceID` header is mandatory. |

### A/DIY Change Set Example

```bash
curl --location --request POST '{{TSAPI_root_URL}}/Reports/ChangeSet' \
  --header 'accept: text/plain' \
  --header 'Content-Type: application/json-patch+json' \
  --header 'x-api-key: <your API key>' \
  --data-raw '{
    "surveyStatuses": ["Closed"],
    "fromTimestampUTC": "2024-03-01T00:00:00Z",
    "toTimestampUTC": "2024-03-07T23:59:59Z"
  }'
```

### A/DIY Start Export Example

```bash
curl --location --request POST '{{TSAPI_root_URL}}/Reports/<your survey ID>/startExport' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json' \
  --data-raw '{"IncludeAttributes": ["1001007", "1001107_7"]}'
```

### A/DIY Export Status Example

```bash
curl --location --request GET '{{TSAPI_root_URL}}/Reports/<your export token>' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>'
```

## Full Service Surveys - ConfirmIT

| Endpoint | Description |
| --- | --- |
| `POST /reports/fullservice/changeSet` | Designed for routine data retrieval, such as daily retrieval, and returns a list of surveys that have been active within a specified time period. The response includes the survey ID, associated workspace ID, and core survey properties. Unlike A/DIY surveys, filtering by survey status is not supported. The `TolunaWorkspaceID` header is optional. If provided, changes are limited to the specified workspace; otherwise, results cover all workspaces linked to your API key. The maximum timeframe for a single changeset is 7 days. The earliest acceptable `fromTimestampUTC` date is 30 days prior to the current date. |
| `POST /reports/fullservice/{surveyId}/startExport` | Initiates a raw data export and returns a unique token to track the process. The export status can be checked using the subsequent API with the returned token. Once complete, the API returns a URL to the generated file. Unlike A/DIY surveys, filtering by demographics attributes is not supported. For API keys associated with multiple workspaces, the `TolunaWorkspaceID` header is mandatory. |
| `GET /reports/fullservice/exportByToken` | Retrieves the status of a raw data export using a provided token and returns the URL to the generated file once available. Exported files are only retained for one month; after this period, a new export must be initiated. If the API key is associated with multiple workspaces, the `TolunaWorkspaceID` header is mandatory. |

### Full Service Change Set Example

```bash
curl --location --request POST '{{TSAPI_root_URL}}/Reports/FullService/ChangeSet' \
  --header 'accept: text/plain' \
  --header 'Content-Type: application/json-patch+json' \
  --header 'x-api-key: <your API key>' \
  --data-raw '{
    "fromTimestampUTC": "2024-03-01T00:00:00Z",
    "toTimestampUTC": "2024-03-07T23:59:59Z"
  }'
```

### Full Service Start Export Example

```bash
curl --location --request POST '{{TSAPI_root_URL}}/Reports/FullService/<your survey ID>/startExport' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json'
```

### Full Service Export Status Example

```bash
curl --location --request GET '{{TSAPI_root_URL}}/Reports/FullService/<your export token>' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>'
```

## Data Export Format

The format for exporting respondent data is consistent across both Toluna Start DIY and Fully Serviced surveys with specific exceptions noted below. Data samples can be provided upon request.

```json
{
  "dataMap": {
    "surveyId": "1234567",
    "title": "Survey title",
    "internalTitle": "Survey internal title",
    "questionnaireType": 1,
    "status": 1,
    "cultures": ["es-mx"],
    "researchCategories": {
      "CategoryIds": [999],
      "OtherCategory": "Some custom category"
    },
    "targetCompletes": 400,
    "reportlink": "https://reports.tolunastart.com/sharedLink.do?...",
    "respondents": 157,
    "attributes": [
      {"attribute": "attribute 1 details"},
      {"attribute": "attribute 2 details"}
    ],
    "questions": [
      {"question": "question 1 details"},
      {"question": "question 2 details"}
    ]
  },
  "respondents": [
    {"respondent": "respondent 1 details and responses"},
    {"respondent": "respondent 2 details and responses"}
  ]
}
```

## Datamap

The `dataMap` object provides core survey metadata and properties, detailing demographic attributes and survey questions.

| Property Name | Description | Notes |
| --- | --- | --- |
| `surveyId` | A unique identifier for the survey. |  |
| `title` | The title of the survey shown to respondents. |  |
| `internalTitle` | The internal-facing title of the survey. | Not visible to respondents. |
| `questionnaireType` | The type of questionnaire, based on Toluna's predefined codes. | `1` Custom Survey, `2` Concept testing, `3` Package testing, `4` Brand health, `5` Comms post launch, `6` Comms pre launch. Not available for Full Service data exports. |
| `status` | The survey's current status at the time of data export. | `1` Open, `2` Paused, `3` Closed, `4` Paused. Not available for Full Service data exports. |
| `targetCompletes` | The target number of completed responses for the survey. |  |
| `respondents` | The number of completed responses collected at the time of export. |  |
| `reportLink` | A publicly shared link to the survey report. |  |
| `cultures` | An array of ISO culture codes for the survey, such as `["es-MX"]`. | Not available for Full Service data exports. |
| `attributes` | An array of objects providing detailed information about demographic or profile attributes. | Not available for Full Service data exports. |
| `questions` | An array of objects providing detailed information about the survey's questions. |  |
| `researchCategories` | An array of selected research category objects with `categoryIds` and `otherCategory`. | Category IDs can be mapped to names via `GET /Metadata/ResearchCategories`. Not available for Full Service data exports. |

## Questions and Attributes

The `questions` object is an array, with each entry representing a question specific to the survey. Similarly, the `attributes` object is an array, where each entry is a socio-demographic attribute relevant to the respondents in the survey's market. Both arrays share the same entry format.

```json
{
  "id": "<question precode>",
  "type": "<question type>",
  "text": "<question title>",
  "rows": [
    {
      "id": "<row 1 precode>",
      "text": "<row 1 text>",
      "media": {
        "id": "<unique id>",
        "mediaUrl": "url to the media asset",
        "type": "<media type - image or video>"
      }
    }
  ],
  "columns": [
    {
      "id": "<column 1 precode>",
      "text": "<column 1 text>"
    }
  ],
  "media": {
    "id": "<unique id>",
    "mediaUrl": "<url to the media asset optimized for respondent view>",
    "mediaOriginalUrl": "<url to the originally uploaded media asset; expirable>",
    "type": "<media type - image or video>"
  }
}
```

| Property Name | Description | Applicable to Question Types | Notes |
| --- | --- | --- | --- |
| `id` | Represents the precode of the question. | All | Unique within the survey. |
| `type` | Denotes the type of question. | All | `SingleChoice`, `ScaledSingleChoice`, `MultipleChoice`, `Text`, `DateType`, `Numeric`, `SingleChoiceGrid`, `MultipleChoiceGrid`. |
| `text` | Contains the title for the question as seen by respondents. | All |  |
| `rows` | Array of row objects. | `SingleChoice`, `ScaledSingleChoice`, `MultipleChoice`, `SingleChoiceGrid`, `MultipleChoiceGrid` | Each row object contains `id`, `text`, and optionally media details including ID, URL, and type. |
| `columns` | Array of column objects. | `SingleChoiceGrid`, `MultipleChoiceGrid` | Each column object contains `id`, `text`, and optionally media details including ID, URL, and type. |
| `media` | Media asset details, set at the question level. | Optional | Includes `id`, `mediaUrl`, `mediaOriginalUrl`, and type. `mediaOriginalUrl` expires within 7 days from the export time. |

## Respondents

The `respondents` object is an array where each entry represents an individual respondent and their collected responses. Each response object is linked to the relevant variable defined in the `dataMap`.

```json
{
  "startDate": "<timestamp in yyyy-MM-dd'T'HH:mm:ss'Z' format>",
  "endDate": "<timestamp>",
  "modifiedDate": "<timestamp>",
  "interviewStatusType": "complete",
  "responses": [
    {
      "questionExtId": "<question 1 precode>",
      "answerData": "",
      "rowAnswerExtId": "<row 1 precode>",
      "columnAnswerExtId": null,
      "numericAnswerData": 0,
      "createdDate": "<timestamp>",
      "modifiedDate": "<timestamp>"
    }
  ]
}
```

### Respondent Level Properties

| Property Name | Description | Notes |
| --- | --- | --- |
| `startDate` | Indicates the start time of the interview session. | ISO standard `yyyy-MM-dd'T'HH:mm:ss'Z'`. |
| `endDate` | Indicates the end time of the interview session. |  |
| `modifiedDate` | Represents the last modification timestamp of the interview record, if an incomplete interview was resumed. |  |
| `interviewStatusType` | Denotes the status of the interview session. | Values: `complete`, `screenout`, or `quotafull`. |

### Response Level Properties

| Property Name | Description | Applicable to Question Types | Notes |
| --- | --- | --- | --- |
| `questionExtId` | Represents the precode of the question to which the response belongs. | All | Corresponds to the `id` field at the question level in the datamap. |
| `answerData` | Contains the response data. | Open-end questions only |  |
| `rowAnswerExtId` | Represents the precode of the row, if applicable. | Single/multiple choice, grids | Corresponds to the `id` field at the row level in the datamap. |
| `columnAnswerExtId` | Represents the precode of the column, if applicable. | Grids only | Corresponds to the `id` field at the column level in the datamap. |
| `numericAnswerData` | Contains numeric response data. | Numeric questions only |  |
| `createdDate` | Indicates the creation timestamp of the response record. | All |  |
| `modifiedDate` | Indicates the last modification timestamp of the response record. | All |  |

