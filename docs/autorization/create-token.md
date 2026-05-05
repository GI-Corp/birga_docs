# Validate Token

Validates an access token and returns information about the associated client, user, and roles.

## Request

**`POST`** `/api/v1/auth-service/validate`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |
| `Content-Type` | string | Yes | `application/json` |

### Request Body

```json
{
  "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `token` | string | Yes | The access token to validate |

## Response

### 200 OK

```json
{
  "isValid": true,
  "expiresAt": "2024-01-15T11:30:00Z",
  "errorMessage": null
}
```

| Field | Type | Description |
|-------|------|-------------|
| `isValid` | boolean | `true` if the token is valid and not expired |
| `expiresAt` | datetime | Token expiration timestamp (ISO 8601) |
| `errorMessage` | string | Error description if `isValid` is `false`, otherwise `null` |

**Invalid token response:**

```json
{
  "isValid": false,
  "expiresAt": null,
  "errorMessage": "Token has expired."
}
```

### 400 Bad Request

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "Bad Request",
  "status": 400,
  "detail": "Token is required.",
  "instance": "/api/v1/auth-service/validate"
}
```

### 500 Internal Server Error

The server encountered an unexpected error. Retry the request.

## Example

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/validate \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-003" \
  -d '{
    "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..."
  }'
```
