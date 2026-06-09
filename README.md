# Crustdata OpenAPI Specification

The official [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0) specification for the
[Crustdata](https://crustdata.com) REST API.

Crustdata provides the real-time data layer behind sales, recruiting, and research
workflows: search indexed datasets of companies, people, and jobs, enrich known
entities with fresh attributes, resolve identifiers, search the web, and fetch page
content over a single versioned REST surface.

The machine-readable spec lives in [`openapi.yaml`](./openapi.yaml). It is generated
from the public documentation at [docs.crustdata.com](https://docs.crustdata.com) and
published for use with Swagger UI, Postman, and OpenAPI client/code generators.

## Authentication

Get an API key from your Crustdata account, then send these headers with every request:

```
Authorization: Bearer <YOUR_API_KEY>
x-api-version: 2025-11-01
```

All endpoints are `POST` and use `application/json`. The base URL is
`https://api.crustdata.com`.

## Endpoints

| API | Method | Path | Description |
| --- | --- | --- | --- |
| **Company** | POST | `/company/search` | Search the indexed company dataset by filters. |
| | POST | `/company/enrich` | Return full company data for known companies. |
| | POST | `/company/identify` | Resolve a name, domain, ID, or profile URL to a company. |
| | POST | `/company/search/autocomplete` | Suggest values for a company search field. |
| **Person** | POST | `/person/search` | Search the indexed people dataset by filters. |
| | POST | `/person/enrich` | Return enriched profiles for known people. |
| | POST | `/person/search/autocomplete` | Suggest values for a person search field. |
| **Job** | POST | `/job/search` | Search the indexed job dataset with filters and aggregations. |
| **Web** | POST | `/web/search/live` | Live search across web, news, scholar, AI, and social sources. |
| | POST | `/web/enrich/live` | Fetch full page content for up to 10 URLs. |

## Using the spec

### View it

Paste `openapi.yaml` into the [Swagger Editor](https://editor.swagger.io/) to browse
every endpoint, schema, and example interactively.

### Import into Postman

Postman → **Import** → drop in `openapi.yaml`. Postman builds a ready-to-use
collection. Add your API key and `x-api-version` header, then send requests.

### Generate a client

Generate an SDK in your language of choice with
[openapi-generator](https://openapi-generator.tech/):

```bash
openapi-generator-cli generate -i openapi.yaml -g python -o ./crustdata-python-client
```

### Validate it

```bash
pip install openapi-spec-validator
python -c "from openapi_spec_validator import validate; import yaml; validate(yaml.safe_load(open('openapi.yaml')))"
```

## Documentation

- API docs: [docs.crustdata.com](https://docs.crustdata.com)
- Pricing and rate limits: [docs.crustdata.com/general/pricing](https://docs.crustdata.com/general/pricing)
- Contact: [gtm@crustdata.co](mailto:gtm@crustdata.co)

## License

Released under the [MIT License](./LICENSE).
