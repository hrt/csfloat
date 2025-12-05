---
title: User Information
layout: default
parent: Endpoints
nav_order: 1
---

# User Information

## Get Current User Info

Retrieves information about the authenticated user.

```
GET /me
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |

### Response

```json
{
  "user": {
    "steam_id": "...",
    "balance": 150000,
    "pending_balance": 5000,
    "actionable_trades": 2
  }
}
```

### Response Fields

| Field | Type | Description |
|:------|:-----|:------------|
| `steam_id` | string | User's Steam ID64 |
| `balance` | integer | Available balance in cents |
| `pending_balance` | integer | Pending balance in cents |
| `actionable_trades` | integer | Number of trades requiring action |
