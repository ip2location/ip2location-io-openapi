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

### Import into Postman

[Postman](https://www.postman.com/) supports importing OpenAPI definitions to create an API collection.

1. Open Postman and select **Import**.
2. Choose **File** and upload a definition from this repository's `json/` or `yaml/` directory.
3. Review the imported requests and configure the required API key and parameters.
4. Select an operation and send a test request.

See the [Postman guide to importing API specifications](https://learning.postman.com/docs/getting-started/importing-and-exporting/importing-from-swagger/) for more information.

### View a Definition in Swagger Editor

You can also use [Swagger Editor](https://editor.swagger.io/) to inspect an OpenAPI definition:

1. Open Swagger Editor.
2. Paste or import the contents of a JSON or YAML definition file.
3. Review the operations, parameters, schemas, and any validation messages.

Swagger Editor is useful for exploring a definition before integrating it into an application. Its displayed operations and authentication requirements are determined by the imported file.

### Explore Documentation with Redocly

[Redocly](https://redocly.com/) provides tools for viewing, validating, and publishing OpenAPI reference documentation.

1. Choose a definition from the `json/` or `yaml/` directory.
2. Open the file using a Redocly tool that supports the specification version.
3. Browse the endpoints, request parameters, authentication requirements, response schemas, and examples.

**Compatibility:** These repository definitions use OpenAPI 3.2.0. Check that your Redocly tool or version supports OpenAPI 3.2 before importing them.

### Use with OpenAPI Tooling

OpenAPI-compatible tools may support generating client code, producing reference documentation, or validating specifications. Download the appropriate definition and follow the instructions for your chosen tool.

> **Note:** Generated clients and documentation depend on the capabilities of the tool and the contents of the selected specification. Review and test generated code before using it in production.

## API Access and Authentication

IP2Location.io offers IP intelligence services with features and query limits that vary by API and subscription plan.

- **API key:** Configure credentials as required by the operation or imported specification. Do not commit real keys to source control.
- **Keyless access:** Certain IP geolocation REST requests may support keyless access; this does not imply that every operation in the repository works without authentication.
- **Plan-dependent fields:** Not all response fields are available on every subscription plan or for every IP address.
- **Rate limits and quotas:** Check the current [API pricing and plans](https://www.ip2location.io/pricing) before building high-volume workflows.

See the [official API documentation](https://www.ip2location.io/ip2location-documentation) for current authentication parameters and service behavior.

## Common Use Cases

| Use case | How the definitions help |
|---|---|
| API testing | Import operations into Postman and test requests and responses. |
| API exploration | Inspect parameters and response schemas before writing integration code. |
| Client development | Use compatible OpenAPI tools as a starting point for generated clients. |
| API documentation | Render supported definitions in an OpenAPI documentation viewer. |
| Integration review | Compare application requests against the documented API contract. |

## Troubleshooting

| Issue | Suggested action |
|---|---|
| A definition fails to import | Try the alternate JSON/YAML representation and inspect the tool's validation message. |
| An operation is missing | Confirm that you imported the definition for the intended API. |
| Authentication fails | Check the API key and the authentication configuration for that operation. |
| The response contains fewer fields than expected | Confirm your API plan and whether the queried IP has data for those fields. |
| A generated client fails | Check the generator's OpenAPI support and review the generated request and authentication handling. |

If you believe a specification is incorrect, open an issue with the **filename, operation, expected behavior, and observed behavior**.

## Related IP2Location Products

| Product | Purpose |
|---|---|
| [IP2Location.io](https://www.ip2location.io/) | Hosted IP geolocation, ASN, and network intelligence APIs. |
| [IP2Location LITE](https://www.ip2location.com/database/lite) | Free downloadable IP geolocation and ASN databases for offline use. |
| [IP2Location Database](https://www.ip2location.com/database/ip2location) | Commercial offline IP geolocation databases. |
| [IP2Proxy](https://www.ip2location.com/database/ip2proxy) | IP proxy, VPN, TOR and anonymizer intelligence. |
| [IP2WHOIS](https://www.ip2whois.com/) | Domain WHOIS lookup services. |

## Support

- [IP2Location.io API documentation](https://www.ip2location.io/ip2location-documentation)
- [API plans and pricing](https://www.ip2location.io/pricing)
- [Report issues or request features](https://github.com/ip2location/ip2location-io-openapi/issues)

## License

Licensed under the **MIT License**. See [LICENSE](https://github.com/ip2location/ip2location-io-openapi/blob/main/LICENSE).
