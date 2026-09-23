---
name: toast-receive-webhooks
description: Build and operate a webhook endpoint that receives Toast platform events, verify the
  signature, and meet Toast's 2-second acknowledgement requirement. Use when implementing the
  Toast-calls-you side of an integration.
api: Toast webhooks (8 event categories, 12 event types)
generated: '2026-08-27'
method: generated
source: asyncapi/toast-webhooks.yml, conventions/toast-conventions.yml,
  https://doc.toasttab.com/doc/devguide/apiWebhookBasics.html,
  https://doc.toasttab.com/doc/devguide/apiMessageSigning.html,
  https://doc.toasttab.com/doc/devguide/apiTimeouts.html,
  https://doc.toasttab.com/doc/devguide/apiEndpointRequirements.html
operations: []
scopes: []
---

# Receive Toast webhooks

Toast's event surface is webhooks only — there is **no AsyncAPI document, no streaming endpoint, and no
subscription API**. Read `asyncapi/toast-webhooks.yml` in this repository for the full catalogue.

## You do not create your own subscription

A webhook subscription binds one endpoint URL to one event category, and it is created and maintained by
**Toast support** (or, for Standard API access customers, in Toast Web). There is no self-service
subscription endpoint. Plan for a human step in your onboarding.

Each subscription gets its **own secret**, per environment. A stock subscription and a partners
subscription for the same partner in the same environment have different secrets. Store them keyed by
(environment, category), not one global secret.

## The 2-second rule

This is the requirement most implementations get wrong:

- Connection timeout: **2 seconds**.
- Socket timeout: **2 seconds**.
- Your endpoint must return **2xx within that window, before running any business logic**.

Acknowledge first, enqueue, process asynchronously. An endpoint that validates, writes to a database and
then returns 200 will time out under load and Toast will retry — giving you duplicates on top of the
latency problem.

Return **429** if you are genuinely overloaded; Toast treats it as a retryable signal. Restaurant
availability updates retry five times within a minute.

## Verify the signature

Every POST carries `Toast-Signature`: an HMAC computed over the message body and timestamp using that
subscription's secret. Toast says verification is optional; treat it as mandatory. An unverified webhook
endpoint is a public write path into your system.

Compare with a constant-time comparison. Reject on mismatch **before** parsing the body.

## Know which restaurant it is

`Toast-Restaurant-External-ID` carries the location GUID. It is **omitted** on events with no restaurant
context — partners events are the case you will hit. Do not assume the header is present.

## The event catalogue

| Category | Event types | What it means |
|---|---|---|
| orders | `order_updated`, `orders_updated`, `channel_order_updated` | An order changed. Use this instead of polling `/ordersBulk`. |
| guest order fulfillment | `guest_order_status` | Fulfillment status transition. |
| menus | `menus_updated` | A location published menu changes — your cached menu JSON is stale. |
| stock | `in_stock`, `low_quantity`, `out_of_stock` | Item availability transition. |
| partners | `partner_added`, `partner_removed`, `partner_updated` | A location connected or disconnected your integration. No restaurant header. |
| restaurant availability | `availability_online`, `availability_offline` | The location toggled online ordering. |
| ordering schedule | `ordering_schedule_updated` | Online ordering hours changed; now carries `acceptScheduledOrders`. |
| packaging preferences | `packaging_updated` | Packaging configuration changed. |

## Handle the partners events properly

`partner_added` and `partner_removed` are your access-control feed. When a restaurant removes your
integration you lose the right to send its GUID in `Toast-Restaurant-External-ID`, and further calls will
403. Reconcile against `GET /partners/v1/connectedRestaurants` (`connectedRestaurantsGet`) rather than
trusting your local list. Since 2026-07-07 the partner access record also carries the granted `scopes`.

## Expect unknown values

Since 2026-07-20 Toast may add values to any enum with no notice. Event payload enums included. Log and
ignore what you do not recognise; never crash on it.

## If you also implement an outbound API

Gift cards, loyalty and tender are different: those are full OpenAPI specifications where **you** host
the server and Toast is the client (see `openapi/toast-gift-cards-openapi.yaml`,
`openapi/toast-loyalty-openapi.yaml`, `openapi/toast-tender-openapi.yaml`). Toast requires those
endpoints to be **idempotent** — it retries on network failure, and a non-idempotent loyalty endpoint
will double-apply a redemption.
