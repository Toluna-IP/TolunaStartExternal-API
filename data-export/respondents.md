---
title: Respondents
parent: Data Export Format
nav_order: 3
---

# Respondents

The `respondents` array contains each respondent and their collected responses. Response rows reference variables defined in the datamap.

```json
{
  "startDate": "2024-03-05T00:00:00Z",
  "endDate": "2024-03-05T00:08:17Z",
  "modifiedDate": "2024-03-05T00:08:17Z",
  "interviewStatusType": "complete",
  "responses": [
    {
      "questionExtId": "q1",
      "answerData": "",
      "rowAnswerExtId": "1",
      "columnAnswerExtId": null,
      "numericAnswerData": 0,
      "createdDate": "2024-03-05T00:01:00Z",
      "modifiedDate": "2024-03-05T00:01:00Z"
    }
  ]
}
```

## Respondent Properties

| Property | Description | Notes |
| --- | --- | --- |
| `startDate` | Interview start timestamp. | ISO `yyyy-MM-dd'T'HH:mm:ss'Z'`. |
| `endDate` | Interview end timestamp. |  |
| `modifiedDate` | Last modification timestamp, such as when an incomplete interview is resumed. |  |
| `interviewStatusType` | Interview status. | Values include `complete`, `screenout`, and `quotafull`. |

## Response Properties

| Property | Description | Applies to | Notes |
| --- | --- | --- | --- |
| `questionExtId` | Question precode for the response. | All | Matches `dataMap.questions[].id` or `dataMap.attributes[].id`. |
| `answerData` | Text response data. | Open-end questions |  |
| `rowAnswerExtId` | Selected row precode. | Single choice, multiple choice, and grids | Matches row `id` in the datamap. |
| `columnAnswerExtId` | Selected column precode. | Grids | Matches column `id` in the datamap. |
| `numericAnswerData` | Numeric response value. | Numeric questions |  |
| `createdDate` | Response creation timestamp. | All |  |
| `modifiedDate` | Response modification timestamp. | All |  |
