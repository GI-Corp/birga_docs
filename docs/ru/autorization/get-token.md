# Получить токен

Аутентифицирует пользователя по логину и паролю, возвращает токен доступа и токен обновления.

## Запрос

**`POST`** `/api/v1/auth-service/get-token`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | string | Да | `application/json` |

### Тело запроса

```json
{
  "username": "ваш_логин",
  "password": "ваш_пароль"
}
```

| Поле | Тип | Обязателен | Описание |
|------|-----|-----------|----------|
| `username` | string | Да | Логин пользователя |
| `password` | string | Да | Пароль пользователя |

## Ответ

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

| Поле | Тип | Описание |
|------|-----|----------|
| `accessToken` | string | JWT токен доступа. Используйте как `Authorization: Bearer <accessToken>` |
| `refreshToken` | string | Токен для получения нового токена доступа по истечении текущего |
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
  "detail": "Неверный логин или пароль.",
  "instance": "/api/v1/auth-service/get-token"
}
```

### 500 Internal Server Error

Сервер столкнулся с непредвиденной ошибкой. Повторите запрос.

## Пример

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/get-token \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-001" \
  -d '{
    "username": "ваш_логин",
    "password": "ваш_пароль"
  }'
```
