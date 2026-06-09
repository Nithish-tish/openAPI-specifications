# Crustdata API Specifications

This repository contains the specification file for [Crustdata APIs](https://docs.crustdata.com).

Crustdata provides the real-time data layer behind sales, recruiting, and research workflows: search indexed datasets of companies, people, and jobs, enrich known entities with fresh attributes, resolve identifiers, search the web, and fetch page content over a single versioned REST API.

In order to use the APIs, you need to have an API key. You can get an API key by signing up on the [Crustdata website](https://crustdata.com).

The specification lives in [`crustdata-specs.json`](./crustdata-specs.json) and follows the [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0) standard. To try the APIs in [Postman](https://www.postman.com/), open Postman, choose **Import**, and select `crustdata-specs.json` to generate a ready-to-use collection.

## Authentication

Every request needs two headers:

```
Authorization: Bearer YOUR_API_KEY
x-api-version: 2025-11-01
```

- **Base URL:** `https://api.crustdata.com`
- All endpoints use the `POST` method and `application/json`.

## Quickstart

Find a company by its domain and return its headcount and funding:

```bash
curl https://api.crustdata.com/company/search \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{
    "filters": { "field": "basic_info.primary_domain", "type": "=", "value": "hubspot.com" },
    "fields": ["basic_info", "headcount", "funding"],
    "limit": 1
  }'
```

## API Endpoints

### Company

[Search Companies](https://docs.crustdata.com/company-docs/search/introduction) — `POST /company/search`

The Company Search API gives you access to Crustdata's full company dataset, which you can filter and segment using a search query over indexed fields.

```bash
curl https://api.crustdata.com/company/search \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{
    "filters": { "field": "basic_info.primary_domain", "type": "=", "value": "hubspot.com" },
    "fields": ["basic_info", "headcount", "funding"],
    "limit": 1
  }'
```

[Enrich Companies](https://docs.crustdata.com/company-docs/enrichment/introduction) — `POST /company/enrich`

The Company Enrichment API lets you enrich data on a company by performing a one-to-one match against the company profiles hosted in our dataset, returning firmographics, headcount, funding, web traffic, and more. Provide exactly one identifier type.

```bash
curl https://api.crustdata.com/company/enrich \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{
    "domains": ["serverobotics.com"],
    "fields": ["basic_info", "headcount", "funding"]
  }'
```

[Identify Companies](https://docs.crustdata.com/company-docs/identify/introduction) — `POST /company/identify`

The Company Identify API resolves a name, domain, Crustdata ID, or profile URL to a single company, scoring and sorting matches by confidence.

```bash
curl https://api.crustdata.com/company/identify \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{ "domains": ["serverobotics.com"] }'
```

[Company Autocomplete](https://docs.crustdata.com/company-docs/autocomplete/introduction) — `POST /company/search/autocomplete`

The Company Autocomplete API returns suggested values for a company search field, for example industries starting with "tech".

```bash
curl https://api.crustdata.com/company/search/autocomplete \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{ "field": "basic_info.industries", "query": "tech", "limit": 5 }'
```

### Person

[Search People](https://docs.crustdata.com/person-docs/search/introduction) — `POST /person/search`

The Person Search API gives you access to Crustdata's full people dataset, which you can filter and segment using a search query over attributes such as title, seniority, company, location, and education.

```bash
curl https://api.crustdata.com/person/search \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{
    "filters": {
      "op": "and",
      "conditions": [
        { "field": "experience.employment_details.current.title", "type": "=", "value": "CTO" },
        { "field": "experience.employment_details.current.company_headcount_range", "type": "in", "value": ["51-200", "201-500"] }
      ]
    },
    "limit": 2
  }'
```

[Enrich People](https://docs.crustdata.com/person-docs/enrichment/introduction) — `POST /person/enrich`

The Person Enrichment API lets you enrich data on a person by performing a one-to-one match using a profile URL or business email, returning profile, experience, education, and contact details. Provide exactly one identifier type.

```bash
curl https://api.crustdata.com/person/enrich \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{ "business_emails": ["abhilash@crustdata.com"] }'
```

[Person Autocomplete](https://docs.crustdata.com/person-docs/autocomplete/introduction) — `POST /person/search/autocomplete`

The Person Autocomplete API returns suggested values for a person search field, for example job titles starting with "VP".

```bash
curl https://api.crustdata.com/person/search/autocomplete \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{ "field": "experience.employment_details.current.title", "query": "VP", "limit": 5 }'
```

### Job

[Search Jobs](https://docs.crustdata.com/job-docs/search/introduction) — `POST /job/search`

The Job Search API gives you access to Crustdata's indexed job dataset, which you can filter, sort, and aggregate by company, category, location, and posting date.

```bash
curl https://api.crustdata.com/job/search \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{
    "filters": {
      "op": "and",
      "conditions": [
        { "field": "company.basic_info.company_id", "type": "=", "value": 631394 },
        { "field": "job_details.category", "type": "=", "value": "Engineering" }
      ]
    },
    "limit": 20
  }'
```

### Web

[Web Search](https://docs.crustdata.com/web-docs/search/introduction) — `POST /web/search/live`

The Web Search API runs a live search across web, news, scholar, AI, and social sources, with optional location and date filtering.

```bash
curl https://api.crustdata.com/web/search/live \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{ "query": "crustdata", "location": "US", "sources": ["web", "news"], "page": 1 }'
```

[Web Fetch](https://docs.crustdata.com/web-docs/fetch/introduction) — `POST /web/enrich/live`

The Web Fetch API retrieves the full page content for a list of URLs.

```bash
curl https://api.crustdata.com/web/enrich/live \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "x-api-version: 2025-11-01" \
  -H "Content-Type: application/json" \
  -d '{ "urls": ["https://example.com"] }'
```

## Rate Limits

Default rate limits apply per endpoint (for example, 30 requests per minute for search). See [Rate Limits](https://docs.crustdata.com/general/rate-limits) for details, and contact [gtm@crustdata.co](mailto:gtm@crustdata.co) for higher limits.

## License

Released under the [MIT License](./LICENSE).
