---
title: Home
layout: home
nav_order: 1
---

# Toluna Start API Guide

This site helps developers integrate with the Toluna Start API for survey management, metadata lookups, and raw respondent data extraction.

The guide is organized around the same core areas exposed in Swagger:

- [General]({{ site.baseurl }}/general/) - technical standards, authentication, and quick-start guidance.
- [API Reference]({{ site.baseurl }}/api/) - Health, Metadata, Reports, and Surveys endpoints.
- [Data Export Format]({{ site.baseurl }}/data-export/) - datamap, questions, attributes, and respondent response structure.
- [How-To Guides]({{ site.baseurl }}/how-to/) - common export workflows and practical integration recipes.
- [Swagger and Schemas]({{ site.baseurl }}/reference/openapi/) - embedded Swagger UI plus selected OpenAPI schema notes.

## Base URL

All current API calls use version `v1`:

```text
https://{{TolunaDomain}}/api/v1/
```

## Common Flow

1. Request API access and receive an `x-api-key`.
2. Use [Metadata]({{ site.baseurl }}/api/metadata/) endpoints to map workspaces, cultures, categories, and research categories.
3. Use [Surveys]({{ site.baseurl }}/api/surveys/) endpoints to create, find, inspect, launch, pause, or monitor surveys.
4. Use [Reports]({{ site.baseurl }}/api/reports/) endpoints to identify changed surveys and download raw respondent export files.
5. Parse the export using the [Data Export Format]({{ site.baseurl }}/data-export/) reference.

## Live Swagger

Use the hosted [Swagger UI](https://api.tolunastart.com/swagger/index.html) for interactive request and response models. This guide also includes a local copy of the OpenAPI JSON at [assets/openapi/toluna-start-openapi.json]({{ site.baseurl }}/assets/openapi/toluna-start-openapi.json).
