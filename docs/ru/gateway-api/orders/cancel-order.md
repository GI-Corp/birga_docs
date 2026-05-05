# Отменить заказ

Отменяет существующий заказ в подключённой POS-системе.

## Запрос

**`POST`** `/api/v1/orders/cancel-order`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | string | Да | `application/json` |

### Тело запроса

```json
{}
```

> Тело запроса в настоящее время пустое. По вопросам параметров отмены заказа обратитесь в [поддержку](mailto:gicorp.work@gmail.com).

## Ответ

### 200 OK

Заказ успешно отменён.

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/orders/cancel-order \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-034" \
  -d '{}'
```
