# Проверить токен

Проверяет токен доступа и возвращает информацию о связанном клиенте, пользователе и ролях.

## Запрос

**`POST`** `/api/v1/auth-service/validate`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | string | Да | `application/json` |

### Тело запроса

```json
{
  "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

| Поле | Тип | Обязателен | Описание |
|------|-----|-----------|----------|
| `token` | string | Да | Токен доступа для проверки |

## Ответ

### 200 OK

```json
{
  "isValid": true,
  "expiresAt": "2024-01-15T11:30:00Z",
  "errorMessage": null
}
```

| Поле | Тип | Описание |
|------|-----|----------|
| `isValid` | boolean | `true`, если токен действителен и не истёк |
| `expiresAt` | datetime | Время истечения токена (ISO 8601) |
| `errorMessage` | string | Описание ошибки, если `isValid` равен `false`, иначе `null` |

**Ответ для недействительного токена:**

```json
{
  "isValid": false,
  "expiresAt": null,
  "errorMessage": "Срок действия токена истёк."
}
```

### 400 Bad Request

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "Bad Request",
  "status": 400,
  "detail": "Поле token обязательно.",
  "instance": "/api/v1/auth-service/validate"
}
```

### 500 Internal Server Error

Сервер столкнулся с непредвиденной ошибкой. Повторите запрос.

## Пример

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/validate \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-003" \
  -d '{
    "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..."
  }'
```
