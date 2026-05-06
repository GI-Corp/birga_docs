# Создать заказ на доставку

Создаёт новый заказ на доставку в подключённой POS-системе.

## Запрос

**`POST`** `/api/v1/delivery/create-order`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | string | Да | `application/json` |

### Тело запроса

```json
{
  "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderId": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
  "comment": "Оставить у двери",
  "items": [
    {
      "itemId": "item-001",
      "quantity": 2,
      "modifiers": [
        {
          "modifierId": "mod-001",
          "quantity": 1
        }
      ]
    }
  ]
}
```

| Поле | Тип | Обязателен | Описание |
|------|-----|-----------|----------|
| `branchId` | uuid | Да | Филиал, выполняющий доставку |
| `orderId` | uuid | Да | Ваш уникальный идентификатор заказа |
| `comment` | string | Нет | Инструкции по доставке (макс. 255 символов) |
| `items` | array | Нет | Список позиций заказа |

**Объект позиции:**

| Поле | Тип | Обязателен | Описание |
|------|-----|-----------|----------|
| `itemId` | string | Да | Идентификатор позиции меню из POS |
| `quantity` | integer | Да | Количество единиц |
| `modifiers` | array | Нет | Выбранные модификаторы |

**Объект модификатора:**

| Поле | Тип | Обязателен | Описание |
|------|-----|-----------|----------|
| `modifierId` | string | Да | Идентификатор модификатора из POS |
| `quantity` | integer | Да | Количество единиц модификатора |

## Ответ

### 200 OK

```json
{
  "id": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
  "externalId": "iiko-delivery-5541",
  "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "sessionId": 88,
  "status": "New"
}
```

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | uuid | Идентификатор заказа в Birga |
| `externalId` | string | ID заказа в POS-системе |
| `branchId` | uuid | Филиал, обрабатывающий доставку |
| `sessionId` | integer | Идентификатор сессии POS |
| `status` | string | Начальный статус заказа |

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/delivery/create-order \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-040" \
  -d '{
    "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderId": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
    "comment": "Оставить у двери",
    "items": [{ "itemId": "item-001", "quantity": 1 }]
  }'
```
