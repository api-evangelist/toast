---
name: toast-submit-and-void-order
description: Submit a guest order to a Toast restaurant location, price it first, and void it if it
  must be taken back. Use when creating, inspecting, or reversing orders on the Toast platform.
api: Toast Orders API 2.9.4
generated: '2026-08-27'
method: generated
source: openapi/toast-orders-api-openapi.yml, openapi/toast-payments-api-openapi.yml,
  openapi/toast-discounts-api-openapi.yml, conventions/toast-conventions.yml,
  https://doc.toasttab.com/doc/devguide/apiCreatingOrders.html,
  https://doc.toasttab.com/doc/devguide/apiVoidOrder.html
operations:
- pricesPost
- applicableDiscountsPost
- ordersPost
- ordersGuidGet
- ordersChecksPaymentsPost
- voidOrder
scopes:
- orders:read
- orders.channel:read
- orders.orders:write
- orders.items:write
- orders.payments:write
- orders.channel:void
---

# Submit and void a Toast order

## Before you start

You cannot call Toast without a hostname Toast issued you privately. Every example below writes
`{toast-host}`; substitute the sandbox or production hostname the Toast integrations team gave you.
Toast never publishes it.

Every request needs two headers:

```
Authorization: Bearer <token from authenticationLoginPost>
Toast-Restaurant-External-ID: <restaurant GUID>
Content-Type: application/json
```

Omitting `Content-Type: application/json` returns **415**, not 400.

## 1. Rehearse the money before you commit

`POST /orders/v2/prices` (`pricesPost`) returns the calculated prices, taxes, service charges and
discounts for an order payload **without creating anything**. Run it first. It is the only dry-run Toast
gives you, and it is the difference between an agent that checks its arithmetic and one that creates a
wrong order it may not be able to take back.

If you intend to apply a discount, call `POST /orders/v2/applicableDiscounts`
(`applicableDiscountsPost`) to learn which discounts actually apply to this order before you attach one.

## 2. Build a valid order

Item references must resolve. A `Selection` points at a menu item by `guid` **or** by
`multiLocationId`; supplying neither returns `Referenced entity (type=MenuItem) must contain either a
GUID or MultiLocationId`. Discounts must carry a GUID — look them up with `discountsGet`
(`GET /config/v2/discounts`).

Get item GUIDs from the menus API (`menusGet`), not from a cached copy: subscribe to the `menus_updated`
webhook, or check `metadataGet` before you trust a cached menu.

## 3. Submit

`POST /orders/v2/orders` (`ordersPost`), scope `orders.orders:write`.

You get back the created `Order` with its `guid`, its checks, and each check's selections. **Persist the
order GUID and the clientId you authenticated with** — you need both to void it later.

## 4. Read it back

`GET /orders/v2/orders/{guid}` (`ordersGuidGet`). If your client created the order, you need **both**
`orders:read` and `orders.channel:read`; with `orders.channel:read` alone you can only see your own
orders. Guest personal information needs `guest.pi:read` on top; delivery addresses need
`delivery_info.address:read`. A 403 here is almost always a missing second scope, not a missing grant.

Do not poll `GET /orders/v2/ordersBulk` for updates. It is rate limited to 5 requests per client per
location per second, historical ranges must be a month or less with calls 5–10 seconds apart, and Toast
explicitly recommends the `order_updated` webhook instead. `GET /orders/v2/orders` for a time period is
deprecated.

## 5. Payment is one-way — decide before you call it

`POST /orders/v2/orders/{orderGuid}/checks/{checkGuid}/payments` (`ordersChecksPaymentsPost`) adds a
payment to a check. **Toast publishes no refund or payment-reversal operation.** An existing payment
cannot be updated; only the tip can be amended, via
`ordersOrderGuidChecksCheckGuidPaymentsPaymentGuidPatch`. Refunding is a Toast Web / POS action a human
performs. Treat taking a payment as irreversible from the API.

## 6. Void — the one reversal Toast gives you

`POST /orders/v2/orders/{orderGuid}/void` (`voidOrder`), scope `orders.channel:void`:

```json
{ "selections": { "voidAll": true }, "payments": { "voidAll": true } }
```

Both `voidAll` values must be `true`. Toast states no time limit, but the void only works when **all**
of these hold:

- the order is not already voided or deleted;
- the order was placed with an **Other** payment option — not cash, not card, not a Toast gift card;
- the order is not restricted;
- you authenticate with the **same clientId** that created the order.

That last condition is the one that bites: an agent that rotates client accounts loses the ability to
undo its own work. Void with the credential that created the order.

After a successful void, `guestOrderStatus` becomes `VOIDED`, `voided` becomes `true`, `paymentStatus`
becomes `VOIDED`, and applied discounts move to `VOID` or `PENDING_VOID`. The order stays readable via
`ordersGuidGet` and `ordersBulkGet`. Once voided it can no longer be updated.

## Errors and limits

- Errors are a proprietary `ErrorMessage` JSON object, not RFC 9457 problem+json. Keep `requestId` —
  Toast support traces 5xx failures by it. See `errors/toast-problem-types.yml`.
- **There is no idempotency key.** A retried `ordersPost` after a timeout may create a second order.
  Read back before retrying a write that may have landed.
- 20 requests/second and 10,000 per 15 minutes. On **429**, back off using `X-Toast-RateLimit-Reset`
  (epoch seconds). There is no `Retry-After`.
- **413** means the order has too many checks.
