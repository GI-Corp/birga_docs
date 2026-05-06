# Get Order

Returns full details for a specific order, including items, pricing, and status.

## Request

**`GET`** `/api/v1/orders/get-order`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |

### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `BranchId` | uuid | Yes | Branch identifier |
| `OrderId` | uuid | Yes | Order identifier |
| `ExternalId` | string | No | Order ID in the POS system (max 255 chars) |
| `SessionId` | string | No | POS session identifier (max 255 chars) |
| `Guid` | string | No | Alternative unique identifier (max 255 chars) |
| `forceRefresh` | boolean | No | Bypass cache — default `false` |

## Response

### 200 OK

```json
{
  "id": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
  "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "externalId": "iiko-order-8821",
  "sessionId": 112,
  "status": "InProgress",
  "type": "DineIn",
  "totalItems": 3,
  "totalPrice": 37.50,
  "tableId": 5,
  "tableName": "Table 5",
  "waiterId": 42,
  "waiterName": "John",
  "creatorId": 1,
  "creatorName": "Admin",
  "createdAt": "2024-01-15T10:00:00Z",
  "updatedAt": "2024-01-15T10:15:00Z",
  "items": [
    {
      "id": "item-001",
      "name": "Caesar Salad",
      "description": "Classic Caesar",
      "price": 12.50,
      "imageUrl": "https://cdn.example.com/caesar.jpg",
      "isActive": true,
      "modifiers": []
    }
  ]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `id` | uuid | Birga order identifier |
| `branchId` | uuid | Branch identifier |
| `externalId` | string | Order ID in the POS system |
| `sessionId` | integer | POS session identifier |
| `status` | string | Current order status |
| `type` | string | Order type |
| `totalItems` | integer | Total item count |
| `totalPrice` | number | Total price |
| `tableId` | integer | Table number |
| `tableName` | string | Table name |
| `waiterId` | integer | Assigned waiter ID |
| `waiterName` | string | Assigned waiter name |
| `creatorId` | integer | Creator user ID |
| `creatorName` | string | Creator user name |
| `createdAt` | datetime | Order creation timestamp |
| `updatedAt` | datetime | Last update timestamp |
| `items` | array | Order line items (see [Menu item schema](/gateway-api/menu/get-menu)) |

### 204 No Content

No order found for the given parameters.

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/orders/get-order",
  "message": "BranchId and OrderId are required",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/orders/get-order",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/orders/get-order?BranchId=3fa85f64-5717-4562-b3fc-2c963f66afa6&OrderId=7c9e6679-7425-40de-944b-e07fc1f90ae7" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-031"
```
