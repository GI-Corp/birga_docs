# Филиалы ресторана

Возвращает постраничный список филиалов конкретного ресторана.

## Запрос

**`GET`** `/api/v1/restaurants/get-restaurant-branches/{restaurantId}`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |

### Параметры пути

| Параметр | Тип | Обязателен | Описание |
|----------|-----|-----------|----------|
| `restaurantId` | uuid | Да | Идентификатор ресторана |

### Параметры запроса

| Параметр | Тип | Обязателен | По умолчанию | Описание |
|----------|-----|-----------|-------------|----------|
| `PageNum` | integer | Да | — | Номер страницы (1–100000) |
| `PageSize` | integer | Да | — | Количество записей на странице (1–500) |
| `forceRefresh` | boolean | Нет | `false` | Обойти кэш и получить актуальные данные из POS |

## Ответ

### 200 OK

```json
{
  "totalCount": 3,
  "data": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "restaurantId": "9b1c3e70-1234-4abc-b3fc-2c963f66afa6",
      "name": "Главный филиал",
      "externalId": "iiko-branch-001",
      "posSystemName": "iiko",
      "posSystemId": "pos-001",
      "updatedAt": "2024-01-15T10:30:00Z"
    }
  ]
}
```

| Поле | Тип | Описание |
|------|-----|----------|
| `totalCount` | integer | Общее количество филиалов по всем страницам |
| `data` | array | Массив объектов филиалов на текущей странице |

**Объект филиала:**

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | uuid | Идентификатор филиала |
| `restaurantId` | uuid | Идентификатор родительского ресторана |
| `name` | string | Название филиала |
| `externalId` | string | ID в подключённой POS-системе |
| `posSystemName` | string | Название POS-системы |
| `posSystemId` | string | Идентификатор экземпляра POS-системы |
| `updatedAt` | datetime | Время последнего обновления (ISO 8601) |

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/restaurants/get-restaurant-branches/9b1c3e70-1234-4abc-b3fc-2c963f66afa6?PageNum=1&PageSize=20" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-011"
```
