---
title: Common Demographic Attributes
parent: How-To Guides
nav_order: 1
---

# Common Demographic Attributes

Toluna Start A/DIY exports include common demographic attributes by default. When starting an export, you can optionally pass `includeAttributes` to restrict the export to a subset of demographic attributes.

An attribute ID is a unique alphanumeric identifier. Culture-specific attributes include a culture suffix, such as `1001107_7` for German household income. Attributes that are not culture-specific use a simple ID, such as `1001007` for gender.

| Attribute ID | Description |
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

## Export Selected Attributes

```text
curl --location --request POST 'https://{{TolunaDomain}}/api/v1/Reports/<survey ID>/startExport' \
  --header 'x-api-key: <your API key>' \
  --header 'TolunaWorkspaceID: <your workspace ID>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "includeAttributes": ["1001007", "1001107_7"]
  }'
```
