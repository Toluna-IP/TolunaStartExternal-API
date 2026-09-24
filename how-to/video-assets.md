---
title: Work With Video Assets
parent: How-To Guides
nav_order: 4
---

# Work With Video Assets

Surveys with video assets can include media links in survey structure and datamap objects.

| Field | Description |
| --- | --- |
| `mediaUrl` | Optimized streaming asset for respondent view. Video assets can be `.m3u8` HLS playlists. |
| `mediaOriginalUrl` | Original uploaded file, such as `.mp4`. This URL expires within 7 days from export time. |

For permanent access to the original media, download and store the file before `mediaOriginalUrl` expires.

## Original Media URL Endpoint

Swagger exposes `POST /api/v1/Reports/GetOriginalMediaUrl` and `POST /api/v1/Surveys/DecryptMedia` for media-link workflows. Use the hosted Swagger UI to inspect the current request and response shapes.
