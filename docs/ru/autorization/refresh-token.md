# Обновить токен

Обменивает действующий токен обновления на новую пару токенов доступа и обновления. Используйте этот эндпоинт, когда токен доступа истёк.

## Запрос

**`POST`** `/api/v1/auth-service/refresh-token`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | string | Да | `application/json` |

### Тело запроса

```json
{
  "refreshToken": "dGhpcyBpcyBhIHJlZnJlc2ggdG9rZW4..."
}
```

| Поле | Тип | Обязателен | Описание |
|------|-----|-----------|----------|
| `refreshToken` | string | Да | Токен обновления, полученный от `/get-token` или предыдущего вызова `/refresh-token` |

## Ответ

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

| Поле | Тип | Описание |
|------|-----|----------|
| `accessToken` | string | Новый JWT токен доступа |
| `refreshToken` | string | Новый токен обновления (предыдущий аннулируется) |
| `tokenType` | string | Тип токена, всегда `Bearer` |
| `expiresIn` | integer | Время жизни токена доступа в секундах |
| `refreshExpiresIn` | integer | Время жизни токена обновления в секундах |
| `scope` | string | Область применения токена |

### 400 Bad Request

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "Bad Request",
  "status": 400,
  "detail": "Недействительный или истёкший токен обновления.",
  "instance": "/api/v1/auth-service/refresh-token"
}
```

### 500 Internal Server Error

Сервер столкнулся с непредвиденной ошибкой. Повторите запрос.

## Пример

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/refresh-token \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-002" \
  -d '{
    "refreshToken": "dGhpcyBpcyBhIHJlZnJlc2ggdG9rZW4..."
  }'
```
