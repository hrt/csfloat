---
title: Buy Orders
layout: default
parent: Endpoints
nav_order: 4
---

# Buy Orders

## Get My Buy Orders

Retrieve all buy orders for the authenticated user.

```
GET /me/buy-orders
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |

### Query Parameters

| Parameter | Type | Default | Description |
|:----------|:-----|:--------|:------------|
| `page` | integer | 0 | Page number |
| `limit` | integer | 50 | Results per page |
| `order` | string | - | Sort order: `desc`, `asc` |

### Response

```json
{
  "orders": [
    {
      "id": "order_id",
      "price": 48000,
      "qty": 2,
      "market_hash_name": "...",
      "expression": "DefIndex == 507 AND PaintIndex == 415 AND FloatValue < 0.07"
    }
  ],
  "count": 10
}
```

---

## Create Buy Order (Expression-based)

For skins/knives with specific filters.

```
POST /buy-orders
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |
| `Content-Type` | Yes | `application/json` |

### Request Body

```json
{
  "expression": {
    "condition": "and",
    "rules": [
      {"field": "DefIndex", "operator": "==", "value": {"constant": "507"}},
      {"field": "PaintIndex", "operator": "==", "value": {"constant": "415"}},
      {"field": "FloatValue", "operator": "<", "value": {"constant": "0.07"}},
      {"field": "StatTrak", "operator": "==", "value": {"constant": "false"}}
    ]
  },
  "max_price": 50000,
  "quantity": 2
}
```

### Expression Fields

| Field | Description |
|:------|:------------|
| `DefIndex` | Item definition index |
| `PaintIndex` | Paint/skin index |
| `FloatValue` | Float value |
| `StatTrak` | StatTrak status (`true`/`false`) |

### Operators

| Operator | Description |
|:---------|:------------|
| `==` | Equal to |
| `<` | Less than |
| `<=` | Less than or equal |
| `>` | Greater than |
| `>=` | Greater than or equal |

---

## Create Buy Order (Market Hash Name)

For stickers, cases, and other items.

```
POST /buy-orders
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |
| `Content-Type` | Yes | `application/json` |

### Request Body

```json
{
  "market_hash_name": "Sticker | ...",
  "max_price": 1500,
  "quantity": 5
}
```

---

## Delete Buy Order

```
DELETE /buy-orders/{order_id}
```

### Headers

| Header | Required | Description |
|:-------|:---------|:------------|
| `Authorization` | Yes | Your CSFloat API key |

### Response

```json
{
  "message": "successfully removed the order"
}
```
