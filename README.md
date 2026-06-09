# Crustdata API Specifications

This repository contains the specification file for [Crustdata APIs](https://docs.crustdata.com).

In order to use the APIs, you need to have an API key. You can get an API key by signing up on the [Crustdata website](https://crustdata.com).

The specification lives in [`crustdata-specs.json`](./crustdata-specs.json) and follows the [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0) standard. To try the APIs in [Postman](https://www.postman.com/), open Postman, choose **Import**, and select `crustdata-specs.json` to generate a ready-to-use collection.

## API Endpoints

### Company

[Search Companies](https://docs.crustdata.com/company-docs/search/introduction)

The Company Search API gives you access to Crustdata's full company dataset, which you can filter and segment using a search query over indexed fields.

[Enrich Companies](https://docs.crustdata.com/company-docs/enrichment/introduction)

The Company Enrichment API lets you enrich data on a company by performing a one-to-one match against the company profiles hosted in our dataset, returning firmographics, headcount, funding, web traffic, and more.

[Identify Companies](https://docs.crustdata.com/company-docs/identify/introduction)

The Company Identify API resolves a name, domain, Crustdata ID, or profile URL to a single company, scoring and sorting matches by confidence.

[Company Autocomplete](https://docs.crustdata.com/company-docs/autocomplete/introduction)

The Company Autocomplete API returns suggested values for a company search field, for example industries starting with "tech".

### Person

[Search People](https://docs.crustdata.com/person-docs/search/introduction)

The Person Search API gives you access to Crustdata's full people dataset, which you can filter and segment using a search query over attributes such as title, seniority, company, location, and education.

[Enrich People](https://docs.crustdata.com/person-docs/enrichment/introduction)

The Person Enrichment API lets you enrich data on a person by performing a one-to-one match using a profile URL or business email, returning profile, experience, education, and contact details.

[Person Autocomplete](https://docs.crustdata.com/person-docs/autocomplete/introduction)

The Person Autocomplete API returns suggested values for a person search field, for example job titles starting with "VP".

### Job

[Search Jobs](https://docs.crustdata.com/job-docs/search/introduction)

The Job Search API gives you access to Crustdata's indexed job dataset, which you can filter, sort, and aggregate by company, category, location, and posting date.

### Web

[Web Search](https://docs.crustdata.com/web-docs/search/introduction)

The Web Search API runs a live search across web, news, scholar, AI, and social sources, with optional location and date filtering.

[Web Fetch](https://docs.crustdata.com/web-docs/fetch/introduction)

The Web Fetch API retrieves the full page content for a list of URLs.

## License

Released under the [MIT License](./LICENSE).
