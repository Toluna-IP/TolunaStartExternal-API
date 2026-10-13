---
title: Survey Management API
nav_order: 4
---

# Survey Management API

The Toluna Start API provides endpoints for programmatically creating, launching, and monitoring Toluna Start surveys. This functionality allows users to bypass or significantly reduce reliance on the platform's user interface.

If you are using a multi-workspace API key, you must include the `TolunaWorkspaceID` header in all requests to these endpoints.

Refer to Swagger documentation for request and response format details. Data samples can be provided upon request.

| Endpoint | Description |
| --- | --- |
| `POST /surveys/search` | Returns a paginated list of surveys with basic information, including ID, titles, and other fields typically required for a summary view on the projects. Can be filtered by survey status. Report links need to be retrieved individually per survey. |
| `POST /surveys` | Creates a survey with provided questionnaire structure and target details, including Toluna or own audience, culture, IR, and sample size. For Toluna Influencers audience, quota is set to a client-specific template or, if not configured, defaulted to a standard NatRep for the specified target country. |
| `POST /surveys/{surveyId}/clone` | Duplicates specified survey, including the questionnaire, target, and quota configuration. |
| `PUT /surveys/{surveyId}` | Updates or overrides the survey with the provided new structure. |
| `DELETE /surveys/{surveyId}` | Deletes a survey. |
| `GET /surveys/{surveyId}` | Returns details for the specified survey, including full questionnaire and basic target information, including audience type, sample size, IR, and audience culture. |
| `GET /surveys/{surveyId}/basic` | Returns basic information on the survey, including ID, title, status, and test links. For launched surveys also returns a live link for own audience only and the report link. |
| `GET /surveys/{surveyId}/billing` | Returns billing information for the survey including estimated costs, credits available for the account, and payment history if the survey is already live. |
| `GET /surveys/{surveyId}/feasibility` | Returns estimated feasibility for the survey based on the expected LOI and required sample. |
| `PUT /surveys/{surveyId}/launch` | Processes payment and initiates launch or relaunch of the survey. Survey price in credits has to be retrieved from the billing details and passed to this call as a safety measure. |
| `PUT /surveys/{surveyId}/pause` | Puts the survey on hold. |
| `GET /surveys/{surveyId}/fieldwork` | Returns the number of achieved completes for the survey. |

