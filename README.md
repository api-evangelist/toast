# Toast (toast)
Toast is a restaurant technology platform providing cloud-based point-of-sale, payment processing, and business management tools for the restaurant industry. The Toast platform exposes REST APIs enabling technology partners to build integrations for orders, menus, labor management, restaurant configuration, inventory/stock management, authentication, and partner ecosystem access. APIs use OAuth 2.0 client credentials authentication with GUIDs for resource identification. Toast serves 120,000+ restaurant locations and offers both partner integrations (requiring formal partnership) and custom integrations via the developer portal.

**URL:** [https://doc.toasttab.com/doc/devguide/index.html](https://doc.toasttab.com/doc/devguide/index.html)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Food Service, Point of Sale, Restaurants, Hospitality

## Timestamps

- **Created:** 2025-02-08
- **Modified:** 2026-05-03

## APIs

### Toast Orders API
The Toast Orders API enables retrieval of restaurant orders, checks, and payment information. Supports bulk order queries by date range and individual order retrieval by GUID.

**Human URL:** [https://doc.toasttab.com/openapi/orders/overview/](https://doc.toasttab.com/openapi/orders/overview/)

#### Tags:

 - Orders, Payments, Point of Sale

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/orders/overview/)
- [OpenAPI](openapi/toast-orders-openapi.yaml)

### Toast Menus API
The Toast Menus API provides complete menu data retrieval including items, modifiers, prices, and availability.

**Human URL:** [https://doc.toasttab.com/openapi/menus/overview/](https://doc.toasttab.com/openapi/menus/overview/)

#### Tags:

 - Menus, Food Service

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/menus/overview/)
- [OpenAPI](openapi/toast-menus-openapi.yaml)

### Toast Labor API
The Toast Labor API manages employee records, schedules, and shift data for restaurant locations.

**Human URL:** [https://doc.toasttab.com/openapi/labor/overview/](https://doc.toasttab.com/openapi/labor/overview/)

#### Tags:

 - Labor, Employees, Scheduling

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/labor/overview/)
- [OpenAPI](openapi/toast-labor-openapi.yaml)

### Toast Restaurants API
The Toast Restaurants API provides location configuration data including restaurant settings, hours, payment options, and management group restaurant discovery.

**Human URL:** [https://doc.toasttab.com/openapi/restaurants/overview/](https://doc.toasttab.com/openapi/restaurants/overview/)

#### Tags:

 - Restaurants, Configuration

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/restaurants/overview/)
- [OpenAPI](openapi/toast-restaurants-openapi.yaml)

### Toast Stock API
The Toast Stock API manages inventory for menu items and modifiers.

**Human URL:** [https://doc.toasttab.com/openapi/stock/overview/](https://doc.toasttab.com/openapi/stock/overview/)

#### Tags:

 - Stock, Inventory

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/stock/overview/)
- [OpenAPI](openapi/toast-stock-openapi.yaml)

### Toast Partners API
The Toast Partners API provides partner accounts with access to list connected restaurants.

**Human URL:** [https://doc.toasttab.com/openapi/partners/overview/](https://doc.toasttab.com/openapi/partners/overview/)

#### Tags:

 - Partners, Multi-Location

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/partners/overview/)
- [OpenAPI](openapi/toast-partners-openapi.yaml)

### Toast Authentication API
The Toast Authentication API implements OAuth 2.0 client credentials flow for obtaining access tokens.

**Human URL:** [https://doc.toasttab.com/openapi/authentication/overview/](https://doc.toasttab.com/openapi/authentication/overview/)

#### Tags:

 - Authentication, OAuth

#### Properties

- [Documentation](https://doc.toasttab.com/openapi/authentication/overview/)
- [OpenAPI](openapi/toast-authentication-openapi.yaml)

## Common Properties

- [Website](https://pos.toasttab.com/)
- [Documentation](https://doc.toasttab.com/doc/devguide/index.html)
- [Portal](https://doc.toasttab.com/openapi/)
- [SignUp](https://developers.toasttab.com/)
- [GitHubOrganization](https://github.com/toasttab)

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

- [Toast Orders API](openapi/toast-orders-openapi.yaml)
- [Toast Menus API](openapi/toast-menus-openapi.yaml)
- [Toast Labor API](openapi/toast-labor-openapi.yaml)
- [Toast Restaurants API](openapi/toast-restaurants-openapi.yaml)
- [Toast Stock API](openapi/toast-stock-openapi.yaml)
- [Toast Partners API](openapi/toast-partners-openapi.yaml)
- [Toast Authentication API](openapi/toast-authentication-openapi.yaml)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Toast Orders](capabilities/shared/orders.yaml) — 3 operations for order and payment retrieval
- [Toast Labor](capabilities/shared/labor.yaml) — 5 operations for employee management

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Restaurant Operations](capabilities/restaurant-operations.yaml) | Toast Orders, Toast Labor | 8 | Restaurant Manager, Operations Team |

## Vocabulary

- [Toast Vocabulary](vocabulary/toast-vocabulary.yaml) — Unified taxonomy mapping 7 resources, 5 actions, 1 workflow, and 3 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Toast Spectral Rules](rules/toast-spectral-rules.yml) — 26 rules across 9 categories enforcing Toast API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
