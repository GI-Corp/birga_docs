# Logout

Revokes the current session and invalidates the access token.

## Request

**`POST`** `/api/v1/auth-service/logout`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |

## Response

### 200 OK

The session has been successfully terminated.

### 400 Bad Request

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "Bad Request",
  "status": 400,
  "detail": "Invalid or missing token.",
  "instance": "/api/v1/auth-service/logout"
}
```

### 500 Internal Server Error

The server encountered an unexpected error. Retry the request.

## Example

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/logout \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-004"
```
