---
title: Data Export Format
nav_order: 4
has_children: true
---

# Data Export Format

Raw respondent export files share the same top-level structure for Toluna Start A/DIY surveys and Full Service surveys, with some fields unavailable for Full Service exports.

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
      "categoryIds": [999],
      "otherCategory": "Some custom category"
    },
    "targetCompletes": 400,
    "reportLink": "https://reports.tolunastart.com/sharedLink.do?...",
    "respondents": 157,
    "attributes": [],
    "questions": []
  },
  "respondents": []
}
```

Use the child pages for the detailed object layouts:

- [Datamap]({{ site.baseurl }}/data-export/datamap/)
- [Questions and Attributes]({{ site.baseurl }}/data-export/questions-and-attributes/)
- [Respondents]({{ site.baseurl }}/data-export/respondents/)
