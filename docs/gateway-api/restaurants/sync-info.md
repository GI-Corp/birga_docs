# Sync Restaurant Info

Triggers a synchronization of restaurant data between Birga and the connected POS system. Use this endpoint to ensure Birga has the latest restaurant configuration from the POS.

## Request

**`POST`** `/api/v1/restaurants/sync-info`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |
| `Content-Type` | string | Yes | `application/json` |

### Request Body

```json
{
  "restaurantId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `restaurantId` | uuid | Yes | Restaurant to synchronize |

## Response

### 200 OK

```json
{
  "restaurantId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "isSynced": true,
  "lastSyncTimeStamp": "2024-01-15T10:30:00Z"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `restaurantId` | uuid | Restaurant that was synchronized |
| `isSynced` | boolean | `true` if synchronization completed successfully |
| `lastSyncTimeStamp` | datetime | Timestamp of the last successful sync (ISO 8601) |

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/restaurants/sync-info",
  "message": "restaurantId is required",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/restaurants/sync-info",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/restaurants/sync-info \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-012" \
  -d '{
    "restaurantId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }'
```
