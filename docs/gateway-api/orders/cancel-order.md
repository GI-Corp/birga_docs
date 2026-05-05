# Cancel Order

Cancels an existing order in the connected POS system.

## Request

**`POST`** `/api/v1/orders/cancel-order`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |
| `Content-Type` | string | Yes | `application/json` |

### Request Body

```json
{}
```

> The request body is currently empty. The order to cancel is identified by the session context. Contact [support](mailto:gicorp.work@gmail.com) for details on order cancellation parameters.

## Response

### 200 OK

The order was successfully cancelled.

### 400 Bad Request

```json
{
  "code": "INVALID_REQUEST",
  "path": "/api/v1/orders/cancel-order",
  "message": "Order cannot be cancelled in its current state",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/orders/cancel-order",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/orders/cancel-order \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-034" \
  -d '{}'
```
