# Get Restaurant Branches

Returns a paginated list of branches for a specific restaurant.

## Request

**`GET`** `/api/v1/restaurants/get-restaurant-branches/{restaurantId}`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `restaurantId` | uuid | Yes | Restaurant identifier |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `PageNum` | integer | Yes | — | Page number (1–100000) |
| `PageSize` | integer | Yes | — | Number of results per page (1–500) |
| `forceRefresh` | boolean | No | `false` | Bypass cache and fetch latest data from POS |

## Response

### 200 OK

```json
{
  "totalCount": 3,
  "data": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "restaurantId": "9b1c3e70-1234-4abc-b3fc-2c963f66afa6",
      "name": "Main Branch",
      "externalId": "iiko-branch-001",
      "posSystemName": "iiko",
      "posSystemId": "pos-001",
      "updatedAt": "2024-01-15T10:30:00Z"
    }
  ]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `totalCount` | integer | Total number of branches across all pages |
| `data` | array | Array of branch objects for the current page |

**Branch object:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | uuid | Branch identifier |
| `restaurantId` | uuid | Parent restaurant identifier |
| `name` | string | Branch name |
| `externalId` | string | ID in the connected POS system |
| `posSystemName` | string | Connected POS system (e.g., `iiko`, `rkeeper`, `poster`) |
| `posSystemId` | string | POS system instance identifier |
| `updatedAt` | datetime | Last updated timestamp (ISO 8601) |

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/restaurants/get-restaurant-branches/{restaurantId}",
  "message": "PageNum must be between 1 and 100000",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/restaurants/get-restaurant-branches/{restaurantId}",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/restaurants/get-restaurant-branches/9b1c3e70-1234-4abc-b3fc-2c963f66afa6?PageNum=1&PageSize=20" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-011"
```
