---
title: Home
layout: home
nav_order: 1
---

# CSFloat API Documentation

Unofficial API reference for [CSFloat.com](https://csfloat.com) - the CS2 skin marketplace.

Entirely LLM generated so use at your own risk.

{: .warning }
This is an **unofficial** documentation. Endpoints may change without notice.

## Base URL

```
https://csfloat.com/api/v1
```

## Authentication

Authenticated endpoints require an `Authorization` header:

```
Authorization: <your-api-key>
```

## Quick Links

| Section | Description |
|:--------|:------------|
| [User Info]({% link endpoints/user.md %}) | Get account info and balance |
| [Trades]({% link endpoints/trades.md %}) | Manage trades |
| [Listings]({% link endpoints/listings.md %}) | Browse and manage listings |
| [Buy Orders]({% link endpoints/buy-orders.md %}) | Create and manage buy orders |
| [Inventory]({% link endpoints/inventory.md %}) | Access your CS2 inventory |
| [Historical Data]({% link endpoints/history.md %}) | Price history |

## Reference

| Section | Description |
|:--------|:------------|
| [Item Definition Indices]({% link reference/def-indices.md %}) | def_index values for items |
| [Float Ranges]({% link reference/float-ranges.md %}) | Wear condition float ranges |

## Notes

- All prices are in **cents** (USD × 100)
- User IDs are Steam ID64 format
- CSFloat charges a 2% seller fee
