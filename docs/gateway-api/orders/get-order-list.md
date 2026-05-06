# Get Order List

Returns a paginated list of orders for a branch, optionally filtered to active orders only.

## Request

**`GET`** `/api/v1/orders/get-order-list`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `BranchId` | uuid | Yes | — | Branch to retrieve orders for |
| `OnlyActive` | boolean | Yes | — | `true` returns only active/open orders; `false` returns all |
| `PageNumber` | integer | No | — | Page number for pagination |
| `PageSize` | integer | No | — | Number of results per page |

## Response

### 200 OK

```json
{
  "totalCount": 42,
  "data": [
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
      "items": []
    }
  ]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `totalCount` | integer | Total number of orders matching the query |
| `data` | array | Array of order objects for the current page |

See [Get Order](/gateway-api/orders/get-order) for the full order object schema.

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/orders/get-order-list",
  "message": "BranchId is required",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/orders/get-order-list",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/orders/get-order-list?BranchId=3fa85f64-5717-4562-b3fc-2c963f66afa6&OnlyActive=true&PageNumber=1&PageSize=20" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-033"
```
