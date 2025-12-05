---
title: Inventory
layout: default
parent: Endpoints
nav_order: 5
---

# Inventory

## Get User Inventory

Retrieve the authenticated user's inventory.

```
GET /me/inventory
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |

### Response

```json
[
  {
    "asset_id": "123456789",
    "market_hash_name": "...",
    "tradable": 1,
    "listing_id": null
  }
]
```

### Response Fields

| Field | Type | Description |
|:------|:-----|:------------|
| `asset_id` | string | Steam asset ID |
| `market_hash_name` | string | Full market name |
| `tradable` | integer | `1` = tradable, `0` = trade hold |
| `listing_id` | string/null | CSFloat listing ID if listed |
