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
| [User Info]({{ site.baseurl }}{% link endpoints/user.md %}) | Get account info and balance |
| [Trades]({{ site.baseurl }}{% link endpoints/trades.md %}) | Manage trades |
| [Listings]({{ site.baseurl }}{% link endpoints/listings.md %}) | Browse and manage listings |
| [Buy Orders]({{ site.baseurl }}{% link endpoints/buy-orders.md %}) | Create and manage buy orders |
| [Inventory]({{ site.baseurl }}{% link endpoints/inventory.md %}) | Access your CS2 inventory |
| [Historical Data]({{ site.baseurl }}{% link endpoints/history.md %}) | Price history |

## Reference

| Section | Description |
|:--------|:------------|
| [Item Definition Indices]({{ site.baseurl }}{% link reference/def-indices.md %}) | def_index values for items |
| [Float Ranges]({{ site.baseurl }}{% link reference/float-ranges.md %}) | Wear condition float ranges |

## Notes

- All prices are in **cents** (USD × 100)
- User IDs are Steam ID64 format
- CSFloat charges a 2% seller fee
