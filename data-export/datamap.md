---
title: Datamap
parent: Data Export Format
nav_order: 1
---

# Datamap

The `dataMap` object provides survey metadata, demographic attribute definitions, and question definitions.

| Property | Description | Notes |
| --- | --- | --- |
| `surveyId` | Unique survey identifier. |  |
| `title` | Respondent-facing survey title. |  |
| `internalTitle` | Internal survey title. | Not visible to respondents. |
| `questionnaireType` | Toluna questionnaire type code. | `1` Custom Survey, `2` Concept testing, `3` Package testing, `4` Brand health, `5` Comms post launch, `6` Comms pre launch. Not available for Full Service exports. |
| `status` | Survey status at export time. | `1` Open, `2` Paused, `3` Closed, `4` Paused. Not available for Full Service exports. |
| `targetCompletes` | Target number of completed responses. |  |
| `respondents` | Completed responses collected at export time. |  |
| `reportLink` | Shared survey report URL. |  |
| `cultures` | ISO culture codes for the survey. | Example: `["es-MX"]`. Not available for Full Service exports. |
| `attributes` | Demographic or profile attribute definitions. | Not available for Full Service exports. |
| `questions` | Survey question definitions. |  |
| `researchCategories` | Selected research category IDs and optional custom category text. | Map IDs with `GET /api/v1/Metadata/ResearchCategories`. Not available for Full Service exports. |

## Research Categories

```json
{
  "categoryIds": [999],
  "otherCategory": "Some custom category"
}
```
