# Список заказов

Возвращает постраничный список заказов филиала с возможностью фильтрации только по активным заказам.

## Запрос

**`GET`** `/api/v1/orders/get-order-list`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |

### Параметры запроса

| Параметр | Тип | Обязателен | По умолчанию | Описание |
|----------|-----|-----------|-------------|----------|
| `BranchId` | uuid | Да | — | Филиал, заказы которого нужно получить |
| `OnlyActive` | boolean | Да | — | `true` — только активные/открытые заказы; `false` — все заказы |
| `PageNumber` | integer | Нет | — | Номер страницы |
| `PageSize` | integer | Нет | — | Количество записей на странице |

## Ответ

### 200 OK

```json
{
  "totalCount": 42,
  "data": [
    {
      "id": "7c9e6679-7425-40de-944b-e07fc1f90ae7",
      "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "status": "InProgress",
      "totalItems": 3,
      "totalPrice": 37.50,
      "createdAt": "2024-01-15T10:00:00Z"
    }
  ]
}
```

| Поле | Тип | Описание |
|------|-----|----------|
| `totalCount` | integer | Общее количество заказов по запросу |
| `data` | array | Массив объектов заказов на текущей странице |

Полное описание объекта заказа — в разделе [Заказы](/ru/gateway-api/orders/index).

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/orders/get-order-list?BranchId=3fa85f64-5717-4562-b3fc-2c963f66afa6&OnlyActive=true&PageNumber=1&PageSize=20" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-033"
```
