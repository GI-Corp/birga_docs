# Get Token

Authenticates a user with username and password and returns an access token and refresh token.

## Request

**`POST`** `/api/v1/auth-service/get-token`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |
| `Content-Type` | string | Yes | `application/json` |

### Request Body

```json
{
  "username": "your_username",
  "password": "your_password"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `username` | string | Yes | Account username |
| `password` | string | Yes | Account password |

## Response

### 200 OK

```json
{
  "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "dGhpcyBpcyBhIHJlZnJlc2ggdG9rZW4...",
  "tokenType": "Bearer",
  "expiresIn": 3600,
  "refreshExpiresIn": 86400,
  "scope": "openid"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `accessToken` | string | JWT access token. Use as `Authorization: Bearer <accessToken>` |
| `refreshToken` | string | Token used to obtain a new access token when the current one expires |
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
  "detail": "Invalid username or password.",
  "instance": "/api/v1/auth-service/get-token"
}
```

### 500 Internal Server Error

The server encountered an unexpected error. Retry the request.

## Example

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/get-token \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-001" \
  -d '{
    "username": "your_username",
    "password": "your_password"
  }'
```
