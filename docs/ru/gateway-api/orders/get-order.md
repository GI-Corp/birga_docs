# Получить заказ

Возвращает полные данные конкретного заказа, включая позиции, стоимость и статус.

## Запрос

**`GET`** `/api/v1/orders/get-order`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |

### Параметры запроса

| Параметр | Тип | Обязателен | Описание |
|----------|-----|-----------|----------|
| `BranchId` | uuid | Да | Идентификатор филиала |
| `OrderId` | uuid | Да | Идентификатор заказа |
| `ExternalId` | string | Нет | ID заказа в POS-системе (макс. 255 символов) |
| `SessionId` | string | Нет | Идентификатор сессии POS (макс. 255 символов) |
| `Guid` | string | Нет | Альтернативный уникальный идентификатор (макс. 255 символов) |
| `forceRefresh` | boolean | Нет | Обойти кэш — по умолчанию `false` |

## Ответ

### 200 OK

```json
{
  "id": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
  "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "externalId": "iiko-order-8821",
  "sessionId": 112,
  "status": "InProgress",
  "type": "DineIn",
  "totalItems": 3,
  "totalPrice": 37.50,
  "tableId": 5,
  "tableName": "Стол 5",
  "waiterId": 42,
  "waiterName": "Иван",
  "creatorId": 1,
  "creatorName": "Администратор",
  "createdAt": "2024-01-15T10:00:00Z",
  "updatedAt": "2024-01-15T10:15:00Z",
  "items": []
}
```

Полное описание полей — в разделе [Заказы](/ru/gateway-api/orders/index).

### 204 No Content

Заказ по указанным параметрам не найден.

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/orders/get-order?BranchId=3fa85f64-5717-4562-b3fc-2c963f66afa6&OrderId=7c9e6679-7425-40de-944b-e07fc1f90ae7" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-031"
```
