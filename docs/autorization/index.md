# Authentication

The Birga Gateway API uses Bearer JWT tokens for authentication. You must obtain an access token before calling any Gateway API endpoint, and include it in every request.

## How It Works

```
1. POST /api/v1/auth-service/get-token  → receive accessToken + refreshToken
2. Use: Authorization: Bearer <accessToken> on all requests
3. When accessToken expires → POST /api/v1/auth-service/refresh-token
4. To end the session → POST /api/v1/auth-service/logout
```

## Token Lifetime

| Token | Field | Description |
|-------|-------|-------------|
| Access token | `accessToken` | Short-lived token for API calls |
| Refresh token | `refreshToken` | Long-lived token to obtain a new access token |
| Expiry (access) | `expiresIn` | Seconds until access token expires |
| Expiry (refresh) | `refreshExpiresIn` | Seconds until refresh token expires |

## Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | [/api/v1/auth-service/get-token](/autorization/get-token) | Obtain access and refresh tokens |
| `POST` | [/api/v1/auth-service/refresh-token](/autorization/refresh-token) | Exchange refresh token for a new access token |
| `POST` | [/api/v1/auth-service/validate](/autorization/create-token) | Validate a token and retrieve session info |
| `POST` | [/api/v1/auth-service/logout](/autorization/logout) | Revoke the current session |

## Common Headers

Every request to the Authentication API must include:

| Header | Required | Description |
|--------|----------|-------------|
| `X-Request-Id` | Yes | Unique request identifier (max 255 characters) |
| `Content-Type` | Yes (POST) | `application/json` |

Endpoints that require an active session also need:

| Header | Required | Description |
|--------|----------|-------------|
| `Authorization` | Yes | `Bearer <access_token>` |
