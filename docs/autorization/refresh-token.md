# Refresh Token

Exchanges a valid refresh token for a new access token and refresh token pair. Use this endpoint when the access token has expired.

## Request

**`POST`** `/api/v1/auth-service/refresh-token`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |
| `Content-Type` | string | Yes | `application/json` |

### Request Body

```json
{
  "refreshToken": "dGhpcyBpcyBhIHJlZnJlc2ggdG9rZW4..."
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `refreshToken` | string | Yes | Refresh token previously issued by `/get-token` or a prior `/refresh-token` call |

## Response

### 200 OK

```json
{
  "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "bmV3UmVmcmVzaFRva2Vu...",
  "tokenType": "Bearer",
  "expiresIn": 3600,
  "refreshExpiresIn": 86400,
  "scope": "openid"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `accessToken` | string | New JWT access token |
| `refreshToken` | string | New refresh token (the previous one is invalidated) |
| `tokenType` | string | Token type, always `Bearer` |
| `expiresIn` | integer | Access token lifetime in seconds |
| `refreshExpiresIn` | integer | Refresh token lifetime in seconds |
| `scope` | string | Token scope |

### 400 Bad Request

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "Bad Request",
  "status": 400,
  "detail": "Invalid or expired refresh token.",
  "instance": "/api/v1/auth-service/refresh-token"
}
```

### 500 Internal Server Error

The server encountered an unexpected error. Retry the request.

## Example

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/refresh-token \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-002" \
  -d '{
    "refreshToken": "dGhpcyBpcyBhIHJlZnJlc2ggdG9rZW4..."
  }'
```
