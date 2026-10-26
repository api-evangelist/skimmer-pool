# Skimmer (skimmer-pool)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
