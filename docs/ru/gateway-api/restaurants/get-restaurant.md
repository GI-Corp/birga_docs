# Получить ресторан

Возвращает данные конкретного ресторана по его ID.

## Запрос

**`GET`** `/api/v1/restaurants/get-restaurant/{restaurantId}`

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
| `forceRefresh` | boolean | Нет | `false` | Обойти кэш и получить актуальные данные из POS |

## Ответ

### 200 OK

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "restaurantId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "name": "Мой Ресторан",
  "externalId": "iiko-org-123",
  "posSystemName": "iiko",
  "posSystemId": "pos-001",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | uuid | Идентификатор Birga |
| `restaurantId` | uuid | Идентификатор родительского ресторана |
| `name` | string | Название ресторана |
| `externalId` | string | ID в подключённой POS-системе |
| `posSystemName` | string | Название POS-системы (например, `iiko`, `rkeeper`, `poster`) |
| `posSystemId` | string | Идентификатор экземпляра POS-системы |
| `updatedAt` | datetime | Время последнего обновления (ISO 8601) |

### 204 No Content

Ресторан с указанным ID не найден.

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/restaurants/get-restaurant/{restaurantId}",
  "message": "restaurantId должен быть валидным UUID",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/restaurants/get-restaurant/{restaurantId}",
  "message": "Внутренняя ошибка сервера",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Пример

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/restaurants/get-restaurant/3fa85f64-5717-4562-b3fc-2c963f66afa6" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-010"
```
