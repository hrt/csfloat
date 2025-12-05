---
title: Listings
layout: default
parent: Endpoints
nav_order: 3
---

# Listings

## Get Listings

Fetch market listings with filters.

```
GET /listings
```

### Query Parameters

| Parameter | Type | Description |
|:----------|:-----|:------------|
| `def_index` | integer | Item definition index |
| `paint_index` | integer | Paint/skin index |
| `market_hash_name` | string | Full market hash name |
| `type` | string | Listing type: `buy_now` |
| `min_price` | integer | Minimum price in cents |
| `max_price` | integer | Maximum price in cents |
| `min_float` | float | Minimum float value |
| `max_float` | float | Maximum float value |
| `category` | integer | `0` = all, `1` = non-StatTrak only |
| `sort_by` | string | `highest_discount`, `lowest_price`, `lowest_float` |
| `limit` | integer | Results per page (default: 50) |

### Response

```json
{
  "data": [
    {
      "id": "listing_id",
      "price": 50000,
      "type": "buy_now",
      "created_at": "2024-01-01T00:00:00Z",
      "item": {
        "market_hash_name": "...",
        "float_value": 0.015,
        "paint_seed": 123,
        "paint_index": 415,
        "is_stattrak": false,
        "wear_name": "Factory New"
      }
    }
  ]
}
```

---

## Create Listing

```
POST /listings
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |
| `Content-Type` | Yes | `application/json` |

### Request Body

```json
{
  "asset_id": "steam_asset_id",
  "price": 50000,
  "type": "buy_now"
}
```

---

## Update Listing Price

```
PATCH /listings/{listing_id}
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |
| `Content-Type` | Yes | `application/json` |

### Request Body

```json
{
  "price": 45000
}
```

---

## Delete Listing

```
DELETE /listings/{listing_id}
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |

---

## Get Buy Orders for Listing

Get buy orders matching a specific listing.

```
GET /listings/{listing_id}/buy-orders
```

### Query Parameters

| Parameter | Type | Default | Description |
|:----------|:-----|:--------|:------------|
| `limit` | integer | 10 | Maximum orders to return |

### Response

```json
[
  {
    "id": "order_id",
    "price": 48000,
    "qty": 1
  }
]
```
