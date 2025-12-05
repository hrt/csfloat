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
| [User]({% link endpoints/user.md %}) | `/me` |
| [Trades]({% link endpoints/trades.md %}) | `/me/trades`, `/trades/{id}/accept` |
| [Listings]({% link endpoints/listings.md %}) | `/listings`, `/listings/{id}`, `/listings/{id}/buy-orders` |
| [Buy Orders]({% link endpoints/buy-orders.md %}) | `/me/buy-orders`, `/buy-orders`, `/buy-orders/{id}` |
| [Inventory]({% link endpoints/inventory.md %}) | `/me/inventory` |
| [User Stall]({% link endpoints/stall.md %}) | `/users/{id}/stall` |
| [History]({% link endpoints/history.md %}) | `/history/{name}/graph` |
