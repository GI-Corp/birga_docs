# Gateway API

The Birga Gateway API provides a unified interface to interact with connected POS systems (IIKO, R-Keeper, Poster). All requests are routed through Birga, which handles protocol translation, retries, and data mapping.

## Base URL

```
https://api.birga-gateway.uz/api/v1
```

## Authentication

All Gateway API endpoints require a valid Bearer token in the `Authorization` header. See the [Authentication](/autorization/index) section to obtain a token.

## Common Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |
| `Content-Type` | string | Yes (POST) | `application/json` |

## Caching

GET endpoints that return restaurant, branch, or menu data are cached. Use the `forceRefresh=true` query parameter to bypass the cache and fetch the latest data directly from the POS system.

## Resource Groups

| Group | Description |
|-------|-------------|
| [Restaurants](/gateway-api/restaurants/index) | Manage restaurant information and synchronization with POS |
| [Branches](/gateway-api/branches/get-branch) | Retrieve branch details |
| [Menu](/gateway-api/menu/get-menu) | Fetch menu categories, items, and modifiers |
| [Orders](/gateway-api/orders/create-order) | Create, retrieve, list, and cancel orders |
| [Delivery](/gateway-api/delivery/create-order) | Create delivery orders |

## Error Format

All errors from the Gateway API follow this structure:

```json
{
  "code": "VALIDATION_ERROR",
  "path": "/api/v1/orders/create-order",
  "message": "branchId is required",
  "details": ["branchId must be a valid UUID"],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `code` | string | Error code |
| `path` | string | Request path that caused the error |
| `message` | string | Human-readable error message |
| `details` | string[] | Additional error details |
| `timestamp` | string | Error timestamp |
