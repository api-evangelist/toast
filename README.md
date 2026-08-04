# Toast (toast)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Toast is a restaurant technology platform providing cloud-based point-of-sale, payment processing, and business management tools for the restaurant industry. The Toast platform exposes REST APIs enabling technology partners to build integrations for orders, menus, labor management, restaurant configuration, inventory/stock management, authentication, and partner ecosystem access. APIs use OAuth 2.0 client credentials authentication with GUIDs for resource identification. Toast serves 120,000+ restaurant locations and offers both partner integrations (requiring formal partnership) and custom integrations via the developer portal.

**URL:** [https://doc.toasttab.com/doc/devguide/index.html](https://doc.toasttab.com/doc/devguide/index.html)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Food Service, Point of Sale, Restaurants, Hospitality

## Timestamps

- **Created:** 2025-02-08
- **Modified:** 2026-06-03

## APIs

### Toast Orders API
The Toast Orders API enables retrieval of restaurant orders, checks, and payment information. Supports bulk order queries by date range and individual order retrieval by GUID. Used for building order management, reporting, and delivery integrations.

**Human URL:** [https://doc.toasttab.com/openapi/orders/overview/](https://doc.toasttab.com/openapi/orders/overview/)

#### Tags:

 - Orders, Payments, Point of Sale

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/orders/overview/)
- [OpenAPI](openapi/toast-orders-openapi.yaml)
- [NaftikoCapability](capabilities/orders-discounts.yaml)
- [NaftikoCapability](capabilities/orders-orders.yaml)
- [NaftikoCapability](capabilities/orders-payments.yaml)

### Toast Menus API
The Toast Menus API provides complete menu data retrieval including items, modifiers, prices, and availability. Enables POS-synchronized menu display for online ordering and third-party menu management integrations.

**Human URL:** [https://doc.toasttab.com/openapi/menus/overview/](https://doc.toasttab.com/openapi/menus/overview/)

#### Tags:

 - Menus, Food Service

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/menus/overview/)
- [OpenAPI](openapi/toast-menus-openapi.yaml)
- [NaftikoCapability](capabilities/menus-general.yaml)

### Toast Labor API
The Toast Labor API manages employee records, schedules, and shift data for restaurant locations. Supports employee CRUD operations, time entry management, and payroll integration workflows.

**Human URL:** [https://doc.toasttab.com/openapi/labor/overview/](https://doc.toasttab.com/openapi/labor/overview/)

#### Tags:

 - Labor, Employees, Scheduling

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/labor/overview/)
- [OpenAPI](openapi/toast-labor-openapi.yaml)
- [NaftikoCapability](capabilities/labor-employees.yaml)
- [NaftikoCapability](capabilities/labor-jobs.yaml)
- [NaftikoCapability](capabilities/labor-shifts.yaml)
- [NaftikoCapability](capabilities/labor-time-entries.yaml)

### Toast Restaurants API
The Toast Restaurants API provides location configuration data including restaurant settings, hours, payment options, and management group restaurant discovery for multi-location operations.

**Human URL:** [https://doc.toasttab.com/openapi/restaurants/overview/](https://doc.toasttab.com/openapi/restaurants/overview/)

#### Tags:

 - Restaurants, Configuration

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/restaurants/overview/)
- [OpenAPI](openapi/toast-restaurants-openapi.yaml)
- [NaftikoCapability](capabilities/restaurants-general.yaml)

### Toast Stock API
The Toast Stock API manages inventory for menu items and modifiers, allowing integration with inventory management systems to track stock levels and trigger restocking alerts for restaurant operations.

**Human URL:** [https://doc.toasttab.com/openapi/stock/overview/](https://doc.toasttab.com/openapi/stock/overview/)

#### Tags:

 - Stock, Inventory

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/stock/overview/)
- [OpenAPI](openapi/toast-stock-openapi.yaml)
- [NaftikoCapability](capabilities/stock-stock.yaml)

### Toast Partners API
The Toast Partners API provides partner accounts with access to list connected restaurants, enabling multi-restaurant management and partner-level operations across restaurant locations.

**Human URL:** [https://doc.toasttab.com/openapi/partners/overview/](https://doc.toasttab.com/openapi/partners/overview/)

#### Tags:

 - Partners, Multi-Location

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/partners/overview/)
- [OpenAPI](openapi/toast-partners-openapi.yaml)
- [NaftikoCapability](capabilities/partners-general.yaml)

### Toast Authentication API
The Toast Authentication API implements OAuth 2.0 client credentials flow for obtaining access tokens used across all Toast platform APIs. Tokens are scoped to restaurant GUIDs and expire after a configurable period.

**Human URL:** [https://doc.toasttab.com/openapi/authentication/overview/](https://doc.toasttab.com/openapi/authentication/overview/)

#### Tags:

 - Authentication, OAuth

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/authentication/overview/)
- [OpenAPI](openapi/toast-authentication-openapi.yaml)
- [NaftikoCapability](capabilities/authentication-authentication.yaml)

### Toast Configuration API
The Toast Configuration API returns information about the configuration of a restaurant and its menus, such as menu items and alternate payment types, plus physical configuration including cash drawers, dining options, revenue centers, service areas, tables, and tax rates. Archived or removed entities are excluded from results.

**Human URL:** [https://doc.toasttab.com/openapi/configuration/overview/](https://doc.toasttab.com/openapi/configuration/overview/)

#### Tags:

 - Configuration, Restaurants

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/configuration/overview/)

### Toast Analytics API
The Toast Analytics API provides an enterprise reporting and analytics service with operations that retrieve data for all or a subset of restaurants in a management group, create requests for reporting data, and retrieve the results. Reporting data includes aggregated sales, check, labor, and guest reporting data.

**Human URL:** [https://doc.toasttab.com/openapi/analytics/overview/](https://doc.toasttab.com/openapi/analytics/overview/)

#### Tags:

 - Analytics, Reporting

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/analytics/overview/)

### Toast Cash Management API
The Toast Cash Management API provides information about cash operations that add cash to or remove cash from a restaurant cash drawer, separately from cash transaction payments.

**Human URL:** [https://doc.toasttab.com/openapi/cashmanagement/overview/](https://doc.toasttab.com/openapi/cashmanagement/overview/)

#### Tags:

 - Cash Management, Payments

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/cashmanagement/overview/)

### Toast Kitchen API
The Toast Kitchen API returns information about kitchen operations for a restaurant, supporting kitchen display and fulfillment workflow integrations.

**Human URL:** [https://doc.toasttab.com/openapi/kitchen/overview/](https://doc.toasttab.com/openapi/kitchen/overview/)

#### Tags:

 - Kitchen, Food Service

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/kitchen/overview/)

### Toast Credit Cards API
The Toast Credit Cards API is a simple, single-request, synchronous API to authorize credit card transactions associated with a Toast Orders API order.

**Human URL:** [https://doc.toasttab.com/openapi/creditcards/overview/](https://doc.toasttab.com/openapi/creditcards/overview/)

#### Tags:

 - Credit Cards, Payments

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/creditcards/overview/)

### Toast Menus V3 API
The Toast Menus V3 API is the next-generation menu retrieval API, returning structured menu, item, modifier, and pricing data for a restaurant in an updated catalog-oriented model alongside the existing Menus V2 surface.

**Human URL:** [https://doc.toasttab.com/openapi/menusv3/overview/](https://doc.toasttab.com/openapi/menusv3/overview/)

#### Tags:

 - Menus, Food Service

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/menusv3/overview/)

### Toast Gift Cards Integration API
The Toast Gift Cards integration specification is an outbound API. The partner hosts an HTTPS endpoint that accepts POST requests from the Toast platform to process gift card transactions (balance inquiry, activation, redemption, reload) for restaurants using a third-party gift card provider.

**Human URL:** [https://doc.toasttab.com/openapi/giftcards/overview/](https://doc.toasttab.com/openapi/giftcards/overview/)

#### Tags:

 - Gift Cards, Webhooks

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/giftcards/overview/)

### Toast Loyalty Integration API
The Toast Loyalty integration specification is an outbound API. The partner hosts an HTTPS endpoint that accepts POST requests from the Toast platform to handle loyalty program transactions (accrual, redemption, inquiry) for restaurants using a third-party loyalty provider.

**Human URL:** [https://doc.toasttab.com/openapi/loyalty/overview/](https://doc.toasttab.com/openapi/loyalty/overview/)

#### Tags:

 - Loyalty, Webhooks

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/loyalty/overview/)

### Toast Tender Integration API
The Toast Tender integration specification is an outbound API. The partner hosts an HTTPS endpoint that accepts POST requests from the Toast platform to receive tender transaction data for alternate or third-party payment tender types processed at the restaurant.

**Human URL:** [https://doc.toasttab.com/openapi/tender/overview/](https://doc.toasttab.com/openapi/tender/overview/)

#### Tags:

 - Tender, Payments, Webhooks

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/tender/overview/)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/toast-inc)
- [Website](https://pos.toasttab.com/)
- [Documentation](https://doc.toasttab.com/doc/devguide/index.html)
- [Portal](https://doc.toasttab.com/openapi/)
- [SignUp](https://developers.toasttab.com/)
- [GitHubOrganization](https://github.com/toasttab)
- [SpectralRules](rules/toast-spectral-rules.yml)
- [Vocabulary](vocabulary/toast-vocabulary.yaml)

## Features

| Name | Description |
|------|-------------|
| Orders API | Retrieve restaurant orders, checks, and payment data by GUID or bulk date queries. |
| Menus API | Full menu data retrieval including items, modifiers, prices, and availability. |
| Labor Management API | Employee CRUD operations, shift management, and payroll integration support. |
| Restaurant Configuration API | Location settings, payment options, and management group restaurant discovery. |
| Stock and Inventory API | Inventory management for menu items and modifiers with stock level tracking. |
| OAuth 2.0 Authentication | Client credentials OAuth flow with GUID-scoped tokens for secure API access. |
| Partner Integration Program | Formal partner program enabling multi-restaurant access and ecosystem integrations. |
| Webhook Support | Outbound integration webhooks for real-time event delivery (gift cards, loyalty, tender). |

## Use Cases

| Name | Description |
|------|-------------|
| Online Ordering Integration | Connect third-party online ordering platforms to Toast POS for order injection and menu sync. |
| Payroll and Labor Integration | Sync Toast employee and shift data with payroll systems using the Labor API. |
| Reporting and Analytics | Pull order and payment data via bulk orders API for custom reporting and business intelligence. |
| Inventory Management | Integrate restaurant inventory systems with Toast Stock API for real-time stock tracking. |
| Loyalty and Gift Cards | Build loyalty program and gift card integrations using Toast outbound webhook APIs. |
| Multi-Location Management | Partner integrations managing hundreds of restaurant locations via Partners API. |

## Integrations

| Name | Description |
|------|-------------|
| DoorDash | Third-party delivery platform integrated with Toast for order injection. |
| UberEats | Delivery platform integration for menu sync and order management. |
| QuickBooks | Accounting integration for restaurant financial data via Toast reporting APIs. |
| ADP | Payroll platform integration using Toast Labor API data. |
| OpenTable | Reservation system integration with Toast for guest management. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Toast Authentication API](openapi/toast-authentication-openapi.yaml)
- [Toast Labor API](openapi/toast-labor-openapi.yaml)
- [Toast Menus API](openapi/toast-menus-openapi.yaml)
- [Toast Orders API](openapi/toast-orders-openapi.yaml)
- [Toast Partners API](openapi/toast-partners-openapi.yaml)
- [Toast Restaurants API](openapi/toast-restaurants-openapi.yaml)
- [Toast Stock API](openapi/toast-stock-openapi.yaml)

### JSON Schema

112 JSON Schema files defining Toast request, response, and entity structures across all seven specified APIs. See [`json-schema/`](json-schema/).

### JSON Structure

110 JSON Structure files documenting the shape of Toast entities. See [`json-structure/`](json-structure/).

### JSON-LD

Linked-data context files mapping each API's vocabulary.

- [Toast Authentication Context](json-ld/toast-authentication-context.jsonld)
- [Toast Labor Context](json-ld/toast-labor-context.jsonld)
- [Toast Menus Context](json-ld/toast-menus-context.jsonld)
- [Toast Orders Context](json-ld/toast-orders-context.jsonld)
- [Toast Partners Context](json-ld/toast-partners-context.jsonld)
- [Toast Restaurants Context](json-ld/toast-restaurants-context.jsonld)
- [Toast Stock Context](json-ld/toast-stock-context.jsonld)

### Examples

91 example request/response payloads covering Toast entities and operations. See [`examples/`](examples/).

## Capabilities

Self-contained Naftiko capabilities, one per business surface (OpenAPI tag), each inlining its `consumes` block plus REST and MCP exposers. Grouped below under their owning API.

### Toast Orders API

- [Orders](capabilities/orders-orders.yaml) — 8 operations
- [Payments](capabilities/orders-payments.yaml) — 4 operations
- [Discounts](capabilities/orders-discounts.yaml) — 3 operations

### Toast Labor API

- [Employees](capabilities/labor-employees.yaml) — 10 operations
- [Shifts](capabilities/labor-shifts.yaml) — 5 operations
- [Jobs](capabilities/labor-jobs.yaml) — 4 operations
- [Time Entries](capabilities/labor-time-entries.yaml) — 2 operations

### Toast Menus API

- [General](capabilities/menus-general.yaml) — 2 operations

### Toast Restaurants API

- [General](capabilities/restaurants-general.yaml) — 2 operations

### Toast Stock API

- [Stock](capabilities/stock-stock.yaml) — 3 operations

### Toast Partners API

- [General](capabilities/partners-general.yaml) — 2 operations

### Toast Authentication API

- [Authentication](capabilities/authentication-authentication.yaml) — 1 operation

## Vocabulary

- [Toast Vocabulary](vocabulary/toast-vocabulary.yaml) — Unified taxonomy mapping 7 resources, 5 actions, 1 workflow, and 3 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Plans & Pricing

- [Toast Plans & Pricing](plans/toast-plans-pricing.yml) — Commercial offering described with API Commons Plans 0.1

## Rate Limits

- [Toast Rate Limits](rate-limits/toast-rate-limits.yml) — Request-rate, concurrency, and quota policies described with API Commons Rate Limits 0.1

## FinOps

- [Toast FinOps](finops/toast-finops.yml) — Billing surface aligned to the FinOps Framework / FOCUS data spec

## Rules

- [Toast Spectral Rules](rules/toast-spectral-rules.yml) — 29 rules enforcing Toast API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
