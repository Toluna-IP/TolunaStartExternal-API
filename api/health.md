---
title: Health
parent: API Reference
nav_order: 1
---

# Health

Health endpoints are useful for connectivity checks and version verification.

| Method | Endpoint | Response |
| --- | --- | --- |
| `GET` | `/api/v1/Ping` | Boolean status. |
| `GET` | `/api/v1/Version` | API version string. |

## Ping

```text
curl --location 'https://{{TolunaDomain}}/api/v1/Ping' \
  --header 'x-api-key: <your API key>'
```

## Version

```text
curl --location 'https://{{TolunaDomain}}/api/v1/Version' \
  --header 'x-api-key: <your API key>'
```
