---
title: Endpoints
layout: default
nav_order: 2
has_children: true
---

# API Endpoints

Base URL: `https://csfloat.com/api/v1`

## Authentication

Most endpoints require the `Authorization` header:

```
Authorization: <your-api-key>
```

## Available Endpoints

| Category | Endpoints |
|:---------|:----------|
| [User]({{ site.baseurl }}{% link endpoints/user.md %}) | `/me` |
| [Trades]({{ site.baseurl }}{% link endpoints/trades.md %}) | `/me/trades`, `/trades/{id}/accept` |
| [Listings]({{ site.baseurl }}{% link endpoints/listings.md %}) | `/listings`, `/listings/{id}`, `/listings/{id}/buy-orders` |
| [Buy Orders]({{ site.baseurl }}{% link endpoints/buy-orders.md %}) | `/me/buy-orders`, `/buy-orders`, `/buy-orders/{id}` |
| [Inventory]({{ site.baseurl }}{% link endpoints/inventory.md %}) | `/me/inventory` |
| [User Stall]({{ site.baseurl }}{% link endpoints/stall.md %}) | `/users/{id}/stall` |
| [History]({{ site.baseurl }}{% link endpoints/history.md %}) | `/history/{name}/graph` |
