# Выход

Завершает текущую сессию и аннулирует токен доступа.

## Запрос

**`POST`** `/api/v1/auth-service/logout`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |

## Ответ

### 200 OK

Сессия успешно завершена.

### 400 Bad Request

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "Bad Request",
  "status": 400,
  "detail": "Недействительный или отсутствующий токен.",
  "instance": "/api/v1/auth-service/logout"
}
```

### 500 Internal Server Error

Сервер столкнулся с непредвиденной ошибкой. Повторите запрос.

## Пример

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/auth-service/logout \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-004"
```
