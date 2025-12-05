---
title: Historical Data
layout: default
parent: Endpoints
nav_order: 7
---

# Historical Data

## Get Price History Graph

Retrieve historical price data for an item.

```
GET /history/{market_hash_name}/graph
```

### Path Parameters

| Parameter | Type | Description |
|:----------|:-----|:------------|
| `market_hash_name` | string | URL-encoded market hash name |

{: .note }
The market hash name must be URL-encoded. Special characters like `★`, `|`, and spaces need proper encoding.

### Response

```json
[
  {
    "day": "2024-01-01",
    "avg_price": 50000,
    "volume": 15
  },
  {
    "day": "2024-01-02",
    "avg_price": 51000,
    "volume": 12
  }
]
```

### Response Fields

| Field | Type | Description |
|:------|:-----|:------------|
| `day` | string | Date (YYYY-MM-DD) |
| `avg_price` | integer | Average sale price in cents |
| `volume` | integer | Number of sales |
