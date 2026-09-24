---
title: Technical Standards
parent: General
nav_order: 2
---

# Technical Standards

| Standard | Detail |
| --- | --- |
| Architecture | RESTful API design. |
| Transport | HTTPS is required. |
| Data format | JSON request and response bodies. |
| Authentication | Header-based API key authentication. |
| Versioning | Current calls are prefixed with `/api/v1/`. |

## Base URL

```text
https://api.tolunastart.com/api/v1/
```

## Content Types

Swagger lists JSON request bodies under content types such as:

- `application/json`
- `application/json-patch+json`
- `text/json`
- `application/*+json`

Use `application/json` unless your client or Toluna contact instructs otherwise.
