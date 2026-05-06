# Create Delivery Order

Creates a new delivery order in the connected POS system.

## Request

**`POST`** `/api/v1/delivery/create-order`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |
| `Content-Type` | string | Yes | `application/json` |

### Request Body

```json
{
  "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderId": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
  "comment": "Leave at the door",
  "items": [
    {
      "itemId": "item-001",
      "quantity": 2,
      "modifiers": [
        {
          "modifierId": "mod-001",
          "quantity": 1
        }
      ]
    }
  ]
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `branchId` | uuid | Yes | Branch fulfilling the delivery order |
| `orderId` | uuid | Yes | Your unique order identifier |
| `comment` | string | No | Delivery instructions (max 255 chars) |
| `items` | array | No | List of items to include in the order |

**Item object:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `itemId` | string | Yes | Menu item identifier from the POS |
| `quantity` | integer | Yes | Number of units |
| `modifiers` | array | No | Selected modifiers for this item |

**Modifier object:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `modifierId` | string | Yes | Modifier identifier from the POS |
| `quantity` | integer | Yes | Number of modifier units |

## Response

### 200 OK

```json
{
  "id": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
  "externalId": "iiko-delivery-5541",
  "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "sessionId": 88,
  "status": "New"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `id` | uuid | Birga order identifier |
| `externalId` | string | Order ID in the connected POS system |
| `branchId` | uuid | Branch handling the delivery |
| `sessionId` | integer | POS session identifier |
| `status` | string | Initial order status |

### 400 Bad Request

```json
{
  "code": "VALIDATION_ERROR",
  "path": "/api/v1/delivery/create-order",
  "message": "branchId is required",
  "details": ["branchId must be a valid UUID"],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/delivery/create-order",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/delivery/create-order \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-040" \
  -d '{
    "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderId": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
    "comment": "Leave at the door",
    "items": [
      { "itemId": "item-001", "quantity": 1 }
    ]
  }'
```
