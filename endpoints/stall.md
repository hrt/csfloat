---
title: User Stall
layout: default
parent: Endpoints
nav_order: 6
---

# User Stall

## Get User's Listings

Retrieve a user's public sell listings.

```
GET /users/{user_id}/stall
```

### Path Parameters

| Parameter | Type | Description |
|:----------|:-----|:------------|
| `user_id` | string | Steam ID64 of the user |

### Query Parameters

| Parameter | Type | Default | Description |
|:----------|:-----|:--------|:------------|
| `limit` | integer | 100 | Maximum listings to return |

### Response

```json
{
  "data": [
    {
      "id": "listing_id",
      "price": 50000,
      "type": "buy_now",
      "item": {
        "market_hash_name": "...",
        "float_value": 0.015,
        "paint_seed": 123
      }
    }
  ]
}
```

{: .note }
This endpoint is public and does not require authentication.
