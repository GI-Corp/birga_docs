# Получить филиал

Возвращает данные конкретного филиала по его ID.

## Запрос

**`GET`** `/api/v1/branches/get-branch/{branchId}`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |

### Параметры пути

| Параметр | Тип | Обязателен | Описание |
|----------|-----|-----------|----------|
| `branchId` | uuid | Да | Идентификатор филиала |

### Параметры запроса

| Параметр | Тип | Обязателен | По умолчанию | Описание |
|----------|-----|-----------|-------------|----------|
| `forceRefresh` | boolean | Нет | `false` | Обойти кэш и получить актуальные данные из POS |

## Ответ

### 200 OK

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "restaurantId": "9b1c3e70-1234-4abc-b3fc-2c963f66afa6",
  "name": "Филиал в центре",
  "externalId": "iiko-branch-001",
  "posSystemName": "iiko",
  "posSystemId": "pos-001",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | uuid | Идентификатор филиала |
| `restaurantId` | uuid | Идентификатор родительского ресторана |
| `name` | string | Название филиала |
| `externalId` | string | ID в подключённой POS-системе |
| `posSystemName` | string | Название POS-системы (например, `iiko`, `rkeeper`, `poster`) |
| `posSystemId` | string | Идентификатор экземпляра POS-системы |
| `updatedAt` | datetime | Время последнего обновления (ISO 8601) |

### 204 No Content

Филиал с указанным ID не найден.

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/branches/get-branch/3fa85f64-5717-4562-b3fc-2c963f66afa6" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-015"
```
