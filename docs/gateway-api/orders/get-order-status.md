# Get Order Status

Returns the current status of a specific order.

## Request

**`GET`** `/api/v1/orders/get-order-status/{orderId}`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `orderId` | string | Yes | Order identifier (max 255 chars) |

## Response

### 200 OK

Returns the current order status.

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/orders/get-order-status/{orderId}",
  "message": "orderId is required",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/orders/get-order-status/{orderId}",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/orders/get-order-status/7c9e6679-7425-40de-944b-e07fc1f90ae7" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-032"
```
