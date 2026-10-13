---
title: How-To Guides
nav_order: 6
---

# How-To Guides

## Working with Common Demographic Attributes in Toluna Start A/DIY Surveys

For Toluna Start A/DIY surveys, common demographic attributes are included in the default data extraction. When exporting data from an A/DIY survey, you have the option to specify a subset of attribute IDs to customize the report's content.

An Attribute ID is a unique alphanumeric identifier. For attributes that are specific to a particular language or audience, the ID will be followed by the culture ID, such as `1001107_7` for `Education level` for the German audience. Non-culture-specific attributes, like `Gender`, use the simple ID, such as `1001007`.

The following table lists standard demographic attributes typically found in reports. Additional reusable attributes could be identified based on specific client reports.

| AttributeID | Description |
| --- | --- |
| `1001001_7` or `1001018` | Country |
| `1001007` | Gender |
| `1001018` | Age Brackets |
| `profile_question_zipcode` | Zipcode/Postal Code |
| `1001101_7` | Education Level |
| `1001107_7` | Household Yearly Income |
| `1001108_7` | Number of People in Household |
| `1001109_7` | Number of Children under 18 in Household |
| `1001291_7` | Shopping Decision Maker |
| `1005145_7` | Employment |

## Ongoing Respondent Data Extraction for Toluna Start A/DIY Surveys

This section offers a step-by-step guide detailing the process for accessing respondent data for Toluna Start A/DIY surveys.

### 1. Retrieve Surveys with Recent Activity

Retrieve the list of surveys having activity in the specified timeframe, such as the last 24 hours. The system considers an activity as either a modification on the survey content, a respondent completing the survey in the given timeframe, or data cleanup applied.

```http
POST /Reports/ChangeSet
```

```json
{
  "surveyStatuses": ["Closed"],
  "fromTimestampUTC": "2024-03-05T00:00:00Z",
  "toTimestampUTC": "2024-03-10T23:59:59Z"
}
```

The response returns the survey ID, workspace ID, last activity date, audience type, survey status, and category information.

```json
{
  "surveyID": "12345678",
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

### 2. Start the Export for Each Survey

Use `POST /Reports/{surveyID}/startExport` and include the `TolunaWorkspaceID` header using the ID from the previous step. The response returns a unique export token in a format like `12345678-20251201174734`.

### 3. Poll for Export Status and Download the File

Use `GET /Reports/{exportToken}` with the token from the previous step and the same `TolunaWorkspaceID` header. Poll until the export status returns as `Complete` and the response includes the export file URL.

```json
{
  "surveyId": "12345678",
  "exportStatus": "Complete",
  "exportURL": "https://tsapi-exports-prod.s3.amazonaws.com/12345678/12345678-20251201174734.json?AWS..."
}
```

### 4. Download the Export File

Download the export file using the provided URL.

### Metadata Lookups

You can map IDs to names using Metadata endpoints as follows. For example, you may choose to export only surveys belonging to a specific category.

- `GET /Metadata/Categories` - category ID to category name
- `GET /Metadata/ResearchCategories` - research category ID to name
- `GET /Metadata/Workspaces` - workspace ID to name

### Performance Recommendations

- The maximum supported timeframe for a single change set is 7 days. Smaller ranges improve performance.
- For ongoing integrations, it is recommended to run daily exports covering the last 24 hours or less.

### Additional Notes

- The earliest acceptable `fromTimestampUTC` is 30 days prior to the current date.
- Older surveys can still be exported using their survey ID and workspace ID, provided they fall within the data retention policy.
- For guidance on historical data extraction, contact your Toluna representative.

## Retrieving Survey Details for Toluna Start A/DIY Surveys

If you need survey structure details beyond what is included in the standard datamap export, follow the steps below.

If you already have the survey ID and simply want to retrieve its structure, use one of the following endpoints. Include the numeric `TolunaWorkspaceID` header along with your authentication key.

- `GET /Surveys/{surveyID}/basic` - retrieves the survey's basic properties
- `GET /Surveys/{surveyID}` - retrieves the full survey structure

If you want to browse or discover surveys under your account:

1. Retrieve the list of workspaces using `GET /Metadata/Workspaces` to obtain all workspace IDs and names. Some workspace names may include `placeholder` text; these are for internal use only and can be ignored.
2. List surveys available to you. You can look up surveys within a single workspace at a time using `POST /Surveys/Search`. Include the `TolunaWorkspaceID` header along with your authentication key.
3. Retrieve survey structure details. For each survey, call `GET /Surveys/{surveyID}/basic` for summary structure, or `GET /Surveys/{surveyID}` for full structure. Include the `TolunaWorkspaceID` header along with your authentication key.

The survey search request expects the following payload for pagination and status filtering:

```json
{ "limit": 20, "pageOffset": 0, "surveyStatuses": ["Closed"] }
```

## Working with Video Assets for Toluna Start A/DIY Surveys

For surveys with video assets, links to media files are provided in survey structure and the data map in two formats:

| Field | Description |
| --- | --- |
| `mediaUrl` | A link to the optimized streaming playlist. These files are in `.m3u8` format, which is a standard format for HLS streams. Various options, including Chrome extensions like `HLS Player - m3u8 HTTP Live Streaming (HLS) Player`, are available for playback. Ensure your media player supports HLS. |
| `mediaOriginalUrl` | A link to the original file in its original format, such as `.mp4`. The link expires within 7 days from the moment of the data export. To ensure permanent access, the media file should be downloaded and stored at the client's facility. |

## Ongoing Respondent Data Extraction for Full Service Surveys

This section offers a step-by-step guide detailing the process for accessing respondent data for Toluna Full Service surveys. The process is similar to that for A/DIY Toluna Start surveys.

### 1. Retrieve Surveys with Recent Activity

Retrieve the list of surveys having activity in the specified timeframe, such as the last 24 hours. The system considers an activity as either a modification on the survey content, a respondent completing the survey in the given timeframe, or data cleanup applied. Filtering by survey status is not available.

```http
POST /Reports/FullService/ChangeSet
```

```json
{
  "fromTimestampUTC": "2024-03-05T00:00:00Z",
  "toTimestampUTC": "2024-03-10T23:59:59Z"
}
```

The response returns the survey ID, workspace ID, last activity date, and audience type.

```json
{
  "surveyID": "12345678",
  "lastActivityDate": "2024-03-07T05:26:17",
  "audienceType": "TolunaInfluencers",
  "tolunaWorkspaceID": 99999
}
```

### 2. Start the Export for Each Survey

Use `POST /Reports/FullService/<survey ID>/startExport` and include the `TolunaWorkspaceID` header using the ID from the previous step. The response returns a unique export token in a format like `12345678-20251201174734`.

### 3. Poll for Export Status and Download the File

Use `GET /Reports/FullService/{exportToken}` with the token from the previous step and the same `TolunaWorkspaceID` header. Poll until the export status returns as `Complete` and the response includes the export file URL.

```json
{
  "surveyId": "12345678",
  "exportStatus": "Complete",
  "exportURL": "https://tsapi-exports-prod.s3.amazonaws.com/12345678/12345678-20251201174734.json?AWS..."
}
```

### 4. Download the Export File

Download the export file using the provided URL.

### Performance Recommendations

- The maximum supported timeframe for a single change set is 7 days. Smaller ranges improve performance.
- For ongoing integrations, it is recommended to run daily exports covering the last 24 hours or less.

### Additional Notes

- The earliest acceptable `fromTimestampUTC` is 30 days prior to the current date.
- Older surveys can still be exported using their survey ID and workspace ID, provided they fall within the data retention policy.
- For guidance on historical data extraction, contact your Toluna representative.
- Category, research category, and survey status information are not available for full service studies in the API.
- Clients are expected to overwrite their local data copies for every survey appearing in the change set to ensure data consistency with Toluna internal systems.

