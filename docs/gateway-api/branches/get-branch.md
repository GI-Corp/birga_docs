# Get Branch

Returns details for a specific branch by its ID.

## Request

**`GET`** `/api/v1/branches/get-branch/{branchId}`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `branchId` | uuid | Yes | Branch identifier |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `forceRefresh` | boolean | No | `false` | Bypass cache and fetch latest data from POS |

## Response

### 200 OK

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "restaurantId": "9b1c3e70-1234-4abc-b3fc-2c963f66afa6",
  "name": "Downtown Branch",
  "externalId": "iiko-branch-001",
  "posSystemName": "iiko",
  "posSystemId": "pos-001",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `id` | uuid | Branch identifier |
| `restaurantId` | uuid | Parent restaurant identifier |
| `name` | string | Branch name |
| `externalId` | string | ID in the connected POS system |
| `posSystemName` | string | Connected POS system (e.g., `iiko`, `rkeeper`, `poster`) |
| `posSystemId` | string | POS system instance identifier |
| `updatedAt` | datetime | Last updated timestamp (ISO 8601) |

### 204 No Content

No branch found for the given ID.

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/branches/get-branch/{branchId}",
  "message": "branchId must be a valid UUID",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/branches/get-branch/{branchId}",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/branches/get-branch/3fa85f64-5717-4562-b3fc-2c963f66afa6" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-015"
```
