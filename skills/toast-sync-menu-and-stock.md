---
name: toast-sync-menu-and-stock
description: Pull a Toast location's published menu, keep a cached copy fresh, and read or update item
  availability. Use when building an ordering, delivery, or inventory integration against Toast.
api: Toast Menus API 3.4.1 / 2.4.1, Toast Stock API 1.0.0, Toast Configuration API 2.5.0
generated: '2026-08-27'
method: generated
source: openapi/toast-menus-v3-openapi.yaml, openapi/toast-menus-api-openapi.yml,
  openapi/toast-stock-api-openapi.yml, openapi/toast-configuration-openapi.yaml,
  https://doc.toasttab.com/doc/devguide/apiEnsuringYourMenuDataIsUpToDate.html,
  https://doc.toasttab.com/doc/devguide/apiUsingTheStockApi.html
operations:
- menusGet
- metadataGet
- getInventory
- postInventorySearch
- updateInventory
- menuItemsGet
- discountsGet
scopes:
- menus:read
- menus.channel:read
- stock:read
- stock:write
- config:read
---

# Sync a Toast menu and keep stock current

## Pick the right menus version

Toast runs v2 and v3 side by side and they are **not** interchangeable:

- **v3** (`/menus/v3`, scope `menus.channel:read`) — ordering-partner integrations only.
- **v2** (`/menus/v2`, scope `menus:read`) — everyone else.

If you are not an ordering partner, use v2. Both expose the same two operations: `menusGet` and
`metadataGet`.

## Pull the menu

`GET /menus/v{2,3}/menus` (`menusGet`) returns the **fully resolved published** menu for the location —
menus, groups, items, modifier groups, modifier options, prices, tax info, alcohol flags, and (since
2026-04-22) `catalogProductInfo` for retail products. It reflects only what the restaurant has
**published**; unpublished edits in Toast Web are invisible until published.

This endpoint is rate limited to **one request per second per location**, tighter than anything else on
the platform. Cache the result. Do not fan out menu pulls across many locations without pacing them.

## Keep the cache fresh — two mechanisms, use both

1. `GET /menus/v{2,3}/metadata` (`metadataGet`) returns the last-published timestamp. Compare it to the
   one you stored with your cached menu; refetch only when it moves.
2. Subscribe to the `menus_updated` webhook. Toast fires it when a location publishes menu changes.
   Your endpoint must return 2xx **within 2 seconds, before any business logic**, then refetch
   asynchronously.

Polling `menusGet` on a timer is the wrong shape — it burns the 1 rps budget and still lags a publish.

## Identifiers: guid vs multiLocationId

Menu entities carry three identifiers and they mean different things:

- `guid` — this entity **at this location**.
- `multiLocationId` — the same logical item **across every location in the group**. This is the one you
  key your own catalog on for a multi-location brand.
- `masterId` — Toast's internal master reference.

An order `Selection` may reference an item by `guid` **or** `multiLocationId`; supplying neither is the
error `Referenced entity (type=MenuItem) must contain either a GUID or MultiLocationId`.

## Read stock

- `GET /stock/v1/inventory` (`getInventory`) — availability for menu items and modifier options.
- `POST /stock/v1/inventory/search` (`postInventorySearch`) — filtered lookup when you only care about
  specific items.

Scope `stock:read`.

## Update stock

`PUT /stock/v1/inventory/update` (`updateInventory`), scope `stock:write`.

This is an **absolute state write with no undo**. Toast publishes no reversal operation for inventory —
"undoing" means writing the previous value back, which you can only do if you captured it first. Read
with `getInventory` before you write, and keep the prior value until the write is confirmed.

## React to stock changes

Subscribe to the stock webhook rather than polling. Three event types: `in_stock`, `low_quantity`,
`out_of_stock`. Each carries `Toast-Restaurant-External-ID` identifying the location.

## Configuration lookups

The configuration API (`/config/v2`, scope `config:read`) is the flat reference layer the menu and order
graphs point at by GUID — 24 collections, 47 operations, each with a list and a get-by-GUID:
`discountsGet`, `diningOptionsGet`, `taxRatesGet`, `revenueCentersGet`, `serviceAreasGet`, `tablesGet`,
`printersGet`, `voidReasonsGet` and more.

Paginate it with the page token, not with `pageSize`/`page` — those are deprecated and are being
removed. Read `Toast-Next-Page-Token` from the response header and replay it as the `pageToken` query
parameter; no header means you are done.

## Watch for open enums

Since 2026-07-20 Toast may add values to any existing enum with **no notice** — new dining options, new
card types, new order states are no longer breaking changes. Every switch or match over a Toast enum
needs a safe default branch, or your sync will crash on a value Toast shipped this morning.
