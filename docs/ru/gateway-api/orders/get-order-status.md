# Статус заказа

Возвращает текущий статус конкретного заказа.

## Запрос

**`GET`** `/api/v1/orders/get-order-status/{orderId}`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |

### Параметры пути

| Параметр | Тип | Обязателен | Описание |
|----------|-----|-----------|----------|
| `orderId` | string | Да | Идентификатор заказа (макс. 255 символов) |

## Ответ

### 200 OK

Возвращает текущий статус заказа.

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/orders/get-order-status/7c9e6679-7425-40de-944b-e07fc1f90ae7" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-032"
```
