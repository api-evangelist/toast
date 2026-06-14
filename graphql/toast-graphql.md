# Toast GraphQL Schema

## Overview

This conceptual GraphQL schema represents the Toast restaurant technology platform API surface. Toast provides cloud-based point-of-sale, payment processing, and business management tools for the restaurant industry. The REST APIs exposed by Toast cover orders, menus, labor management, restaurant configuration, inventory/stock management, authentication, and partner ecosystem access.

This schema is a conceptual mapping derived from the Toast REST API documentation at https://doc.toasttab.com/api/ and the GitHub organization at https://github.com/toasttab. It is intended to illustrate the domain model for restaurant operations, enabling integration planning, documentation, and schema-driven development for Toast platform partners.

## Source

- Provider: Toast
- REST API Docs: https://doc.toasttab.com/api/
- GitHub: https://github.com/toasttab
- Developer Portal: https://developers.toasttab.com/
- Schema File: toast-schema.graphql

## Domain Coverage

The schema covers the following Toast platform domains:

### Restaurant Management
Core restaurant and group identity types representing the physical and organizational structure of Toast restaurant accounts: `Restaurant`, `RestaurantGroup`, `RestaurantInfo`, `RestaurantConfig`, `Section`, `ServiceArea`, `Table`.

### Menu and Catalog
Full menu catalog types aligned to the Toast Menus V2 and V3 API surfaces: `Menu`, `MenuGroup`, `MenuPage`, `MenuItem`, `MenuOption`, `OptionGroup`, `Modifier`, `Price`, `PriceModifier`.

### Orders and Checks
Order lifecycle types covering the full order-to-payment flow used in the Orders API: `Order`, `OrderItem`, `OrderType`, `Check`, `Selection`, `DiningOption`.

### Payments
Payment types covering all Toast-supported tender methods and payment states: `Payment`, `PaymentStatus`, `CashPayment`, `CardPayment`, `GiftCardPayment`, `HouseAccountPayment`, `NonCash`, `AltPayment`, `SupportedPayment`.

### Financials
Discount, tax, service charge, and tip types for financial line items on checks: `Discount`, `AppliedDiscount`, `Tax`, `TaxRate`, `ServiceCharge`, `AppliedServiceCharge`, `TipAmount`, `Refund`.

### Labor and Employees
Employee, role, and scheduling types for the Toast Labor API: `Employee`, `EmployeeRole`, `Labor`, `Shift`, `TimeClock`.

### Customer and Loyalty
CRM, loyalty account, and loyalty program types for guest management and third-party loyalty integrations: `CustomerCRM`, `Customer`, `LoyaltyAccount`, `LoyaltyProgram`.

### Online Ordering
Online ordering configuration types including pre-order scheduling: `OnlineOrdering`, `PreorderTime`.

### Reservations
Open table and reservation management: `OpenTable`.

### Webhooks and Integration
Webhook configuration for outbound Toast integration APIs (gift cards, loyalty, tender): `Webhook`.

## Type Summary

| Type | Domain | Description |
|------|--------|-------------|
| Restaurant | Restaurant Management | Individual restaurant location |
| RestaurantGroup | Restaurant Management | Management group of restaurant locations |
| RestaurantInfo | Restaurant Management | Basic restaurant metadata |
| RestaurantConfig | Restaurant Management | Full restaurant configuration settings |
| Section | Restaurant Management | Dining section within a restaurant |
| ServiceArea | Restaurant Management | Service area grouping tables |
| Table | Restaurant Management | Individual dining table |
| Menu | Menu and Catalog | Top-level menu container |
| MenuGroup | Menu and Catalog | Group of menu pages |
| MenuPage | Menu and Catalog | Page within a menu |
| MenuItem | Menu and Catalog | Individual menu item |
| MenuOption | Menu and Catalog | Option associated with a menu item |
| OptionGroup | Menu and Catalog | Group of modifier options |
| Modifier | Menu and Catalog | Modifier for a menu item |
| Price | Menu and Catalog | Price definition for an item |
| PriceModifier | Menu and Catalog | Price modification rule |
| Order | Orders and Checks | Restaurant order |
| OrderItem | Orders and Checks | Line item within an order |
| OrderType | Orders and Checks | Classification of order (dine-in, takeout, delivery) |
| Check | Orders and Checks | Check or bill associated with an order |
| Selection | Orders and Checks | Menu item selection on a check |
| DiningOption | Orders and Checks | Dining option applied to an order |
| Payment | Payments | Payment record on a check |
| PaymentStatus | Payments | Status of a payment |
| CashPayment | Payments | Cash tender payment |
| CardPayment | Payments | Credit or debit card payment |
| GiftCardPayment | Payments | Gift card tender payment |
| HouseAccountPayment | Payments | House account tender payment |
| NonCash | Payments | Non-cash payment tender |
| AltPayment | Payments | Alternate payment type |
| SupportedPayment | Payments | Payment method supported by restaurant |
| Discount | Financials | Discount definition |
| AppliedDiscount | Financials | Discount applied to a check or selection |
| Tax | Financials | Tax applied to a check |
| TaxRate | Financials | Tax rate definition |
| ServiceCharge | Financials | Service charge definition |
| AppliedServiceCharge | Financials | Service charge applied to a check |
| TipAmount | Financials | Tip amount on a payment |
| Refund | Financials | Refund record |
| Employee | Labor | Restaurant employee record |
| EmployeeRole | Labor | Role assigned to an employee |
| Labor | Labor | Labor record for reporting |
| Shift | Labor | Employee shift record |
| TimeClock | Labor | Time clock entry for an employee |
| CustomerCRM | Customer and Loyalty | CRM record for a restaurant guest |
| Customer | Customer and Loyalty | Customer identity record |
| LoyaltyAccount | Customer and Loyalty | Loyalty account for a guest |
| LoyaltyProgram | Customer and Loyalty | Loyalty program configuration |
| OnlineOrdering | Online Ordering | Online ordering configuration |
| PreorderTime | Online Ordering | Pre-order scheduling time slot |
| OpenTable | Reservations | Open table reservation record |
| Webhook | Integration | Webhook configuration for outbound events |

## Authentication

The Toast REST API uses OAuth 2.0 client credentials flow. All queries in a GraphQL implementation would require a bearer token scoped to a restaurant GUID. Token acquisition maps to the Toast Authentication API at `POST /authentication/v1/authentication/login`.

## Notes

- All identifiers in the Toast platform are GUIDs (UUID strings).
- Restaurant-scoped operations require a `restaurantGuid` context.
- Partner-level access via the Partners API enables multi-restaurant queries.
- Outbound webhook APIs (Gift Cards, Loyalty, Tender) represent partner-hosted endpoints that Toast calls, not inbound API calls.
- This schema does not represent a live GraphQL endpoint; it is a conceptual schema for integration planning.
