---
title: Questions and Attributes
parent: Data Export Format
nav_order: 2
---

# Questions and Attributes

`questions` and `attributes` use the same entry format. Each item defines one variable that can be referenced by respondent response records.

```json
{
  "id": "<question precode>",
  "type": "<question type>",
  "text": "<question title>",
  "rows": [
    {
      "id": "<row precode>",
      "text": "<row text>",
      "media": {
        "id": 123,
        "mediaUrl": "https://...",
        "type": "image"
      }
    }
  ],
  "columns": [
    {
      "id": "<column precode>",
      "text": "<column text>"
    }
  ],
  "media": {
    "id": 123,
    "mediaUrl": "https://...",
    "mediaOriginalUrl": "https://...",
    "type": "video"
  }
}
```

| Property | Description | Applies to | Notes |
| --- | --- | --- | --- |
| `id` | Question or attribute precode. | All | Unique within the survey. |
| `type` | Question type. | All | Includes `SingleChoice`, `ScaledSingleChoice`, `MultipleChoice`, `Text`, `DateType`, `Numeric`, `SingleChoiceGrid`, and `MultipleChoiceGrid`. |
| `text` | Respondent-facing question or attribute title. | All |  |
| `rows` | Row answer options. | Choice and grid questions | Each row can include `id`, `text`, and optional media. |
| `columns` | Column answer options. | Grid questions | Each column includes `id`, `text`, and optional media. |
| `media` | Media asset attached at question level. | Optional | Includes optimized `mediaUrl`, expirable `mediaOriginalUrl`, and media type. |

## Media URLs

- `mediaUrl` points to an optimized respondent-view asset. Video links can be HLS `.m3u8` playlists.
- `mediaOriginalUrl` points to the original uploaded asset and expires within 7 days from export time.
