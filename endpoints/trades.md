---
title: Trades
layout: default
parent: Endpoints
nav_order: 2
---

# Trades

## Get User Trades

Retrieves trades for the authenticated user.

```
GET /me/trades
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |

### Query Parameters

| Parameter | Type | Default | Description |
|:----------|:-----|:--------|:------------|
| `state` | string | - | Filter by trade states (comma-separated) |
| `limit` | integer | 3000 | Maximum number of trades to return |

**Available states:** `queued`, `pending`, `verified`, `cancelled`, `refunded`, `failed`, `expired`

### Response

```json
{
  "trades": [
    {
      "id": "trade_id",
      "buyer_id": "...",
      "seller_id": "...",
      "state": "pending",
      "trade_token": "...",
      "trade_url": "https://steamcommunity.com/tradeoffer/new/...",
      "accepted_at": "2024-01-01T00:00:00Z",
      "contract": {
        "state": "pending",
        "price": 10000,
        "item": {
          "market_hash_name": "...",
          "asset_id": "...",
          "float_value": 0.015,
          "paint_seed": 123,
          "paint_index": 415,
          "is_stattrak": false
        }
      }
    }
  ]
}
```

---

## Accept Trade

{: .warning }
**[Untested]**

```
POST /trades/{trade_id}/accept
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |
| `Content-Type` | Yes | `application/json` |

### Path Parameters

| Parameter | Type | Description |
|:----------|:-----|:------------|
| `trade_id` | string | The trade ID to accept |

### Request Body

```json
{
  "trade_token": "..."
}
```

---

## Bulk Accept Trades

{: .warning }
**[Untested]**

```
POST /trades/bulk/accept
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |
| `Content-Type` | Yes | `application/json` |

### Request Body

```json
{
  "trade_ids": ["trade_id_1", "trade_id_2"]
}
```
