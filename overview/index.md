---
title: Overview
nav_order: 2
---

# Overview
{: .no_toc }

* TOC
{:toc}

## Toluna Start API Overview

The Toluna Start API offers a robust, programmatic interface to the Toluna platform, built on industry-standard technologies to ensure secure and efficient integration.

The API is structured around two core functional areas:

| Area | Description |
| --- | --- |
| Survey Management | Allows users to programmatically create, launch, and monitor Toluna Start surveys. This functionality minimizes or eliminates the need for manual interaction with the platform's user interface. |
| Data Extraction | Provides endpoints for downloading raw respondent data from A/DIY surveys scripted and fielded within Toluna Start for the last two years, and from Full-Service surveys scripted in Confirmit and fielded by Toluna on behalf of the client, subject to the data retention policy in Toluna Analytics. |

Additionally, a Metadata collection of endpoints is provided, enabling the extraction of essential supporting information, such as lists of supported cultures and survey categories.

Key capabilities are outlined in this document. For further technical specifications, including information on endpoints and data formatting, please refer to the public Swagger documentation:

```text
https://api.tolunastart.com/swagger/index.html
```

## Technical Standards

The Toluna Start API adheres to the following established industry conventions:

| Standard | Description |
| --- | --- |
| Architecture | Implemented using RESTful principles. |
| Data Format | Utilizes JSON for both request and response models. |
| Security | Requires HTTPS for all secure communication. |
| Authentication | Mandatory and achieved via a client-specific API key. |

## Authentication and Authorization

To successfully authenticate API requests, customers must include the following required headers:

| Header | Requirement | Description |
| --- | --- | --- |
| `x-api-key` | Mandatory | The unique API key assigned to the customer and obtained through the support team. It functions as the primary authentication token for the Toluna Start API. Depending on the client's configuration on the Toluna Start platform, this key may be linked to one or multiple workspaces. |
| `TolunaWorkspaceID` | Mandatory for some requests | Required for calls targeting a specific workspace when the API key is associated with multiple workspaces. It specifies the workspace where the API call should be executed. Failing to include this header or providing a workspace ID not associated with the current API key will result in a `401 Unauthorized` response. |

## Example

```bash
curl --location --request POST '{{TSAPI_root_URL}}/Surveys/Search' \
  --header 'accept: text/plain' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json-patch+json' \
  --data-raw '{
    "limit": 20,
    "pageOffset": 0,
    "surveyStatuses": ["Closed"]
  }'
```

