# CSFloat API Reference

LLM generated docs of endpoints I've used.

## Table of Contents

- [Base URL](#base-url)
- [Authentication](#authentication)
- [Endpoints](#endpoints)
  - [User Information](#user-information)
    - [Get Current User Info](#get-current-user-info)
  - [Trades](#trades)
    - [Get User Trades](#get-user-trades)
    - [Accept Trade](#accept-trade--untested)
    - [Bulk Accept Trades](#bulk-accept-trades--untested)
  - [Listings](#listings)
    - [Get Listings](#get-listings)
    - [Create Listing](#create-listing)
    - [Update Listing Price](#update-listing-price)
    - [Delete Listing](#delete-listing)
    - [Get Buy Orders for Listing](#get-buy-orders-for-listing)
  - [Buy Orders](#buy-orders)
    - [Get My Buy Orders](#get-my-buy-orders)
    - [Create Buy Order (Expression-based)](#create-buy-order-expression-based)
    - [Create Buy Order (Market Hash Name)](#create-buy-order-market-hash-name)
    - [Delete Buy Order](#delete-buy-order)
  - [Inventory](#inventory)
    - [Get User Inventory](#get-user-inventory)
  - [User Stall](#user-stall)
    - [Get User's Listings (Stall)](#get-users-listings-stall)
  - [Historical Data](#historical-data)
    - [Get Price History Graph](#get-price-history-graph)
- [Item Definition Indices](#item-definition-indices)
  - [Knives](#knives)
  - [Weapons](#weapons)
  - [Gloves](#gloves)
- [Float Value Ranges (Wear Conditions)](#float-value-ranges-wear-conditions)
- [Rate Limiting](#rate-limiting)
- [Error Handling](#error-handling)
- [Notes](#notes)

---

## Base URL

```
https://csfloat.com/api/v1
```

## Authentication

All authenticated endpoints require an `Authorization` header with your CSFloat API key:

```
Authorization: <your-api-key>
```

---

## Endpoints

### User Information

#### Get Current User Info

Retrieves information about the authenticated user.

```
GET /me
```

**Headers:**
- `Authorization: <api-key>` (required)

**Response:**
```json
{
  "user": {
    "steam_id": "12345678",
    "balance": 150000,           // Balance in cents
    "pending_balance": 5000,     // Pending balance in cents
    "actionable_trades": 2       // Number of trades requiring action
  }
}
```

---

### Trades

#### Get User Trades

Retrieves trades for the authenticated user.

```
GET /me/trades
```

**Headers:**
- `Authorization: <api-key>` (required)

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `state` | string | Filter by trade states (comma-separated). Values: `queued`, `pending`, `verified`, `cancelled`, `refunded`, `failed`, `expired` |
| `limit` | integer | Maximum number of trades to return (default: 3000) |

**Example:**
```
GET /me/trades?state=queued,pending&limit=3000
```

**Response:**
```json
{
  "trades": [
    {
      "id": "trade_id_string",
      "buyer_id": "123...",
      "seller_id": "123...",
      "state": "pending",
      "trade_token": "abc123",
      "trade_url": "https://steamcommunity.com/tradeoffer/new/...",
      "accepted_at": "2024-01-01T00:00:00Z",
      "verify_sale_at": null,
      "wait_for_cancel_ping": false,
      "contract": {
        "state": "pending",
        "price": 10000,  // Price in cents
        "item": {
          "market_hash_name": "★ Karambit | Doppler (Factory New)",
          "asset_id": "123456789",
          "wear_name": "Factory New",
          "float_value": 0.015,
          "paint_seed": 123,
          "paint_index": 415,
          "phase": "Phase 2",
          "is_stattrak": false,
          "type": "skin"
        }
      }
    }
  ]
}
```

#### Accept Trade  [untested]

Accept a single trade.

```
POST /trades/{trade_id}/accept
```

**Headers:**
- `Authorization: <api-key>` (required)
- `Content-Type: application/json`

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `trade_id` | string | The trade ID to accept |

**Request Body:**
```json
{
  "trade_token": "abc123"
}
```

**Response:**
```json
{
  // Trade details after acceptance
}
```

#### Bulk Accept Trades  [untested]

Accept multiple trades at once.

```
POST /trades/bulk/accept
```

**Headers:**
- `Authorization: <api-key>` (required)
- `Content-Type: application/json`

**Request Body:**
```json
{
  "trade_ids": ["trade_id_1", "trade_id_2", "trade_id_3"]
}
```

---

### Listings

#### Get Listings

Fetch market listings with various filters.

```
GET /listings
```

**Headers:**
- `Authorization: <api-key>` (optional - required for some features)

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `def_index` | integer | Item definition index (e.g., 507 for Karambit) |
| `paint_index` | integer | Paint/skin index |
| `market_hash_name` | string | Full market hash name of the item |
| `type` | string | Listing type: `buy_now` |
| `min_price` | integer | Minimum price in cents |
| `max_price` | integer | Maximum price in cents |
| `min_float` | float | Minimum float value (0.0-1.0) |
| `max_float` | float | Maximum float value (0.0-1.0) |
| `category` | integer | `0` = all, `1` = non-StatTrak only |
| `sort_by` | string | Sort order: `highest_discount`, `lowest_price`, `lowest_float` |
| `limit` | integer | Results per page (default: 50) |

**Example:**
```
GET /listings?def_index=507&type=buy_now&min_price=10000&max_price=100000&sort_by=highest_discount&limit=50
```

**Response:**
```json
{
  "data": [
    {
      "id": "listing_id",
      "price": 50000,  // Price in cents
      "type": "buy_now",
      "created_at": "2024-01-01T00:00:00Z",
      "item": {
        "market_hash_name": "★ Karambit | Doppler (Factory New)",
        "float_value": 0.015,
        "paint_seed": 123,
        "paint_index": 415,
        "is_stattrak": false,
        "wear_name": "Factory New",
        "phase": "Phase 2"
      }
    }
  ]
}
```

#### Create Listing

Create a new sell listing for an item.

```
POST /listings
```

**Headers:**
- `Authorization: <api-key>` (required)
- `Content-Type: application/json`

**Request Body:**
```json
{
  "asset_id": "steam_asset_id",
  "price": 50000,      // Price in cents
  "type": "buy_now"
}
```

**Response:**
```json
{
  "id": "new_listing_id",
  "price": 50000,
  // ... other listing details
}
```

#### Update Listing Price

Update the price of an existing listing.

```
PATCH /listings/{listing_id}
```

**Headers:**
- `Authorization: <api-key>` (required)
- `Content-Type: application/json`

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `listing_id` | string | The listing ID to update |

**Request Body:**
```json
{
  "price": 45000  // New price in cents
}
```

#### Delete Listing

Remove/delist an item.

```
DELETE /listings/{listing_id}
```

**Headers:**
- `Authorization: <api-key>` (required)

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `listing_id` | string | The listing ID to delete |

**Response:**
```json
{
  // Success confirmation
}
```

#### Get Buy Orders for Listing

Get all buy orders that match a specific listing.

```
GET /listings/{listing_id}/buy-orders
```

**Headers:**
- `Authorization: <api-key>` (optional)

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `listing_id` | string | The listing ID |

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `limit` | integer | Maximum number of orders to return (default: 10) |

**Response:**
```json
[
  {
    "id": "order_id",
    "price": 48000,  // Price in cents
    "qty": 1,
    // ... other order details
  }
]
```

---

### Buy Orders

#### Get My Buy Orders

Retrieve all buy orders for the authenticated user.

```
GET /me/buy-orders
```

**Headers:**
- `Authorization: <api-key>` (required)

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `page` | integer | Page number (default: 0) |
| `limit` | integer | Results per page (default: 50) |
| `order` | string | Sort order: `desc`, `asc` |

**Response:**
```json
{
  "orders": [
    {
      "id": "order_id",
      "price": 48000,      // Max price in cents
      "qty": 2,            // Quantity
      "market_hash_name": "Sticker | Team Liquid (Holo) | Austin 2025",
      "expression": "DefIndex == 507 AND PaintIndex == 415 AND FloatValue < 0.07 AND StatTrak == false"
    }
  ],
  "count": 10
}
```

#### Create Buy Order (Expression-based)

Create a buy order using filter expressions (for skins/knives).

```
POST /buy-orders
```

**Headers:**
- `Authorization: <api-key>` (required)
- `Content-Type: application/json`

**Request Body:**
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
  "max_price": 50000,   // Max price in cents
  "quantity": 2
}
```

#### Create Buy Order (Market Hash Name)

Create a buy order using market hash name (for stickers, cases, etc.).

```
POST /buy-orders
```

**Headers:**
- `Authorization: <api-key>` (required)
- `Content-Type: application/json`

**Request Body:**
```json
{
  "market_hash_name": "Sticker | Team Liquid (Holo) | Austin 2025",
  "max_price": 1500,    // Max price in cents
  "quantity": 5
}
```

#### Delete Buy Order

Remove an existing buy order.

```
DELETE /buy-orders/{order_id}
```

**Headers:**
- `Authorization: <api-key>` (required)

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `order_id` | string | The buy order ID to delete |

**Response:**
```json
{
  "message": "successfully removed the order"
}
```

---

### Inventory

#### Get User Inventory

Retrieve the authenticated user's inventory.

```
GET /me/inventory
```

**Headers:**
- `Authorization: <api-key>` (required)

**Response:**
```json
[
  {
    "asset_id": "123456789",
    "market_hash_name": "★ Karambit | Doppler (Factory New)",
    "tradable": 1,           // 1 = tradable, 0 = not tradable
    "listing_id": null       // null if not listed, otherwise listing ID
  }
]
```

---

### User Stall

#### Get User's Listings (Stall)

Retrieve a user's current sell listings.

```
GET /users/{user_id}/stall
```

**Headers:**
- `Authorization: <api-key>` (optional)

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `user_id` | string | Steam ID64 of the user |

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `limit` | integer | Maximum listings to return (default: 100) |

**Response:**
```json
{
  "data": [
    {
      "id": "listing_id",
      "price": 50000,
      "type": "buy_now",
      "item": {
        "market_hash_name": "★ Karambit | Doppler (Factory New)",
        // ... item details
      }
    }
  ]
}
```

---

### Historical Data

#### Get Price History Graph

Retrieve historical price data for an item.

```
GET /history/{market_hash_name}/graph
```

**Headers:**
- `Authorization: <api-key>` (optional)

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `market_hash_name` | string | URL-encoded market hash name |

**Response:**
```json
[
  {
    "day": "2022-11-01",
    "avg_price": 50000,    // Average price in cents
    "volume": 15           // Number of sales
  },
  {
    "day": "2022-11-02",
    "avg_price": 51000,
    "volume": 12
  }
]
```

---

## Item Definition Indices

Common item definition indices used in the API:

### Knives
| Item | def_index |
|------|-----------|
| Karambit | 507 |
| Butterfly Knife | 515 |
| M9 Bayonet | 508 |
| Bayonet | 500 |
| Flip Knife | 505 |
| Gut Knife | 506 |
| Huntsman Knife | 509 |
| Falchion Knife | 512 |
| Bowie Knife | 514 |
| Shadow Daggers | 516 |
| Ursus Knife | 519 |
| Navaja Knife | 520 |
| Stiletto Knife | 522 |
| Talon Knife | 523 |
| Classic Knife | 503 |
| Paracord Knife | 517 |
| Survival Knife | 518 |
| Nomad Knife | 521 |
| Skeleton Knife | 525 |
| Kukri Knife | 526 |

### Weapons
| Item | def_index |
|------|-----------|
| AK-47 | 7 |
| M4A4 | 16 |
| M4A1-S | 60 |
| Desert Eagle | 1 |
| USP-S | 61 |
| Glock-18 | 4 |

### Gloves
| Item | def_index |
|------|-----------|
| Bloodhound Gloves | 5027 |
| Sport Gloves | 5030 |
| Driver Gloves | 5031 |
| Hand Wraps | 5032 |
| Moto Gloves | 5033 |
| Specialist Gloves | 5034 |
| Hydra Gloves | 5035 |
| Broken Fang Gloves | 4725 |

---

## Float Value Ranges (Wear Conditions)

| Wear | Float Range |
|------|-------------|
| Factory New | 0.00 - 0.07 |
| Minimal Wear | 0.07 - 0.15 |
| Field-Tested | 0.15 - 0.38 |
| Well-Worn | 0.38 - 0.45 |
| Battle-Scarred | 0.45 - 1.00 |

---

## Rate Limiting

The CSFloat API implements rate limiting. Common HTTP status codes:

| Status | Meaning |
|--------|---------|
| 200 | Success |
| 401 | Unauthorized (invalid/missing API key) |
| 404 | Resource not found |
| 429 | Rate limited (too many requests) |

**Recommended intervals:**
- Buy order operations: 30 seconds between creations
- Listing fetches: 5-20 seconds between requests
- General API calls: 0.5-2 seconds between requests

---

## Error Handling

When rate limited (429), implement exponential backoff:
```python
if response.status == 429:
    await asyncio.sleep(5)  # Wait 5 seconds before retry
```

---

## Notes

1. **Prices**: All prices in the API are in **cents** (USD × 100). Divide by 100 to get USD.

2. **Steam IDs**: User IDs are Steam ID64 format.

3. **Trade Token**: Required for accepting trades; obtained from the trade object.

4. **Expression Syntax**: Buy order expressions use a specific format:
   - `DefIndex == 507` - Item type
   - `PaintIndex == 415` - Skin pattern
   - `FloatValue < 0.07` - Float restriction
   - `StatTrak == false` - StatTrak filter

5. **Seller Fee**: CSFloat charges a 2% seller fee on completed sales.
