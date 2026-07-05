# Skimmer (skimmer-pool)

Skimmer is pool-service business management software used by residential and commercial pool-service companies to run customers, bodies of water (pools), service locations, technician routes and service stops, work orders, quotes, invoices, and billing. Skimmer exposes a **real, documented public REST API** at `https://publicapi.getskimmer.com`, with a Zudoku-based developer portal at [devportal.getskimmer.com](https://devportal.getskimmer.com/introduction).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/skimmer-pool/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/skimmer-pool/refs/heads/main/apis.yml)

## API access model (read this first)

The Skimmer Public API is **enterprise-oriented and sales-led**:

- **Documented and public-facing** — the developer portal, reference, rate-limit, and search docs are open to read.
- **Gated for use** — access is available **only on Skimmer's top tier** ("Owning the Market" / "Skimmer for Enterprise"), which carries custom pricing and targets operations servicing 1,000+ pools/month. Per Skimmer's CEO, "This isn't a plug-and-play app store integration, it's an invitation to collaborate and build." Keys are provisioned by Skimmer's sales team (sales@getskimmer.com, (855) 452-1737), not via self-service signup.
- **Authentication** — a per-account key sent in the `skimmer-api-key` request header.
- **Rate limit** — 500 requests per minute per API key; overage returns `429 Too Many Requests` with a `Retry-After` header. Responses carry `RateLimit-Limit`, `RateLimit-Remaining`, and `RateLimit-Reset` headers.
- **Transport** — request/response REST over HTTPS. **No** WebSocket or SSE streaming surface is documented (see `review.yml`).

## Tags

- Pool Service
- Field Service Management
- Pool Maintenance
- Scheduling
- Routes
- Work Orders
- Invoicing
- Vertical SaaS

## Timestamps

- **Created:** 2026-07-04
- **Modified:** 2026-07-04

## APIs

All APIs share base URL `https://publicapi.getskimmer.com` and the `skimmer-api-key` header.

### Skimmer Customers API
CRUD, search, activate/deactivate customers, plus customer activity logs. Search supports Sieve-style `filters`, `sorts`, `page`, `pageSize` (e.g. `filters=BillingState==TX`).

### Skimmer Bodies of Water API
CRUD and search over the pools and other bodies of water Skimmer services (name, gallons, filter, notes).

### Skimmer Service Locations API
CRUD and search over service locations — the physical sites Skimmer bills on (one billing unit = one serviced location).

### Skimmer Work Orders API
Create, update, retrieve, and search work orders, and list work order types.

### Skimmer Routes API
Retrieve a single technician's route (`GetTechRoute`) or all technicians' routes for a day (`GetAllRoutesForDay`), keyed by service date.

### Skimmer Invoices and Billing API
Get/list/search invoices and pull billable service activity from the `Billing` endpoint (read-oriented).

### Skimmer Quotes API
List quotes (optionally by customer / including deleted) and get full quote detail.

### Skimmer Products API
CRUD and search over the product catalog and product categories, plus a bulk `Products/prices` update endpoint.

### Skimmer Users API
List account users — owners, admins, and technicians — for mapping techs to routes and work orders.

## Artifacts

- [OpenAPI](openapi/skimmer-pool-openapi.yml) — modeled from the public developer portal (paths/methods/auth are sourced; body schemas are representative, not authoritative)
- [Postman Collection](collections/skimmer-pool.postman_collection.json)
- [Plans / Pricing](plans/skimmer-pool-plans-pricing.yml)
- [Rate Limits](rate-limits/skimmer-pool-rate-limits.yml)
- [FinOps](finops/skimmer-pool-finops.yml)

## Pricing (summary)

Skimmer bills **per serviced location per month**: "Getting Started" $1/location ($49/mo minimum), "Scaling Up" $2/location ($98/mo minimum, first month free). **Public API access is included only on the custom-priced Enterprise ("Owning the Market") tier.** See `plans/`.

## Common Properties

- [Website](https://www.getskimmer.com)
- [LinkedIn](https://www.linkedin.com/company/skimmer-pool-service-software)
- [Documentation](https://devportal.getskimmer.com/introduction)
- [API Reference](https://devportal.getskimmer.com/api)
- [Enterprise / Sign Up](https://www.getskimmer.com/enterprise)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
