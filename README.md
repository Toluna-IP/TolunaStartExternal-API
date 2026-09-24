# Toluna Start API Guide

This repository contains a Just the Docs-based guide for the Toluna Start API.

The guide includes:

- general API setup and authentication guidance
- endpoint pages for Health, Metadata, Reports, and Surveys
- raw data export format documentation
- how-to guides for common data extraction workflows
- embedded Swagger UI and a local OpenAPI JSON copy

## Local Preview

Install dependencies and run Jekyll:

```bash
bundle install
bundle exec jekyll serve
```

The generated site is written to `_site`.

## OpenAPI Snapshot

The guide stores a local snapshot of the live Swagger spec at:

```text
assets/openapi/toluna-start-openapi.json
```

Refresh it from:

```text
https://{{TolunaDomain}}/swagger/v1/swagger.json
```

[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[Jekyll]: https://jekyllrb.com
[Bundler]: https://bundler.io
