# IP2Location.io OpenAPI Definitions

IP2Location.io provides [various APIs](https://www.ip2location.io/documentation) to look up geolocation, network, mobile, proxy and WHOIS data for IP addresses and domain names.

This repository contains the API definitions in the OpenAPI Specification format, one definition per API, in both JSON and YAML.

## APIs covered

| API | Endpoint | Definition |
| --- | --- | --- |
| IP Geolocation | `https://api.ip2location.io` | `IPGeolocation` |
| Bulk IP Geolocation | `https://bulk.ip2location.io` | `BulkIPGeolocation` |
| Domain WHOIS | `https://api.ip2whois.com/v2` | `DomainWHOIS` |
| Hosted Domain | `https://domains.ip2whois.com/domains` | `HostedDomain` |

Each definition covers the full request surface: authentication, every query parameter with its allowed values, request and response examples for each plan, the complete response schema with field descriptions, and the documented error responses.

## Folder structure

API definitions in this repository are organized into two sub-folders:

```
   /json – Definition files in the json format.
   /yaml – Definition files in the yaml format.
```

Both folders contain the same four definitions. The JSON files are the source of truth; the YAML files mirror them, and CI checks that the two stay in sync. Use whichever format your tooling prefers.

## Authentication

Send your API key as a Bearer token in the `Authorization` header:

```
curl -H "Authorization: Bearer {YOUR_API_KEY}" "https://api.ip2location.io/?ip=8.8.8.8"
```

The `key` query parameter is also supported as an alternative:

```
curl "https://api.ip2location.io/?key={YOUR_API_KEY}&ip=8.8.8.8"
```

The IP Geolocation API can be called without a key, limited to 1,000 queries per day per client IP. The Domain WHOIS and Hosted Domain APIs require a key, and the Bulk IP Geolocation API requires a paid plan. Sign up for a free key at [ip2location.io](https://www.ip2location.io/sign-up).

## Response formats

The IP Geolocation, Domain WHOIS and Hosted Domain APIs return JSON by default and also support XML with `format=xml`. The Bulk IP Geolocation API returns JSON by default and supports CSV with `format=csv`.

Responses are plan-dependent: the Free, Starter, Plus and Security plans return progressively more fields. Every response field is therefore optional in the schemas, except the fields that identify the result, such as `ip` or `domain`. The IP Geolocation definition includes one example response per plan.

## Errors

Failed requests return an error object with a numeric code and a message:

```json
{
  "error": {
    "error_code": 10001,
    "error_message": "Invalid IP address."
  }
}
```

Each definition lists the error codes it can return, mapped to their HTTP status codes and grouped as response examples. An exhausted query allowance returns HTTP 401 with error code 10000; the API does not use 429 or rate-limit headers.

## Usage

Typically, you can import and use the API definition files in [Postman](https://www.postman.com/). Postman allows you to quickly set up an API request by importing an existing definition file. You can follow their tutorial (https://learning.postman.com/docs/getting-started/importing-and-exporting/importing-from-swagger/) to learn more on how to do it.

The definitions are written to OpenAPI 3.2.0 and work with [Postman](https://www.postman.com/), [Redocly](https://redocly.com/) and other clients and code generators that support OpenAPI 3.2.

## License

MIT license, refer to the LICENSE file.
