# Синхронизация ресторана

Инициирует синхронизацию данных ресторана между Birga и подключённой POS-системой. Используйте этот эндпоинт, чтобы убедиться, что в Birga актуальная конфигурация ресторана из POS.

## Запрос

**`POST`** `/api/v1/restaurants/sync-info`

### Заголовки

| Заголовок | Тип | Обязателен | Описание |
|-----------|-----|-----------|----------|
| `Authorization` | string | Да | `Bearer <access_token>` |
| `X-Request-Id` | string | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | string | Да | `application/json` |

### Тело запроса

```json
{
  "restaurantId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

| Поле | Тип | Обязателен | Описание |
|------|-----|-----------|----------|
| `restaurantId` | uuid | Да | Ресторан для синхронизации |

## Ответ

### 200 OK

```json
{
  "restaurantId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "isSynced": true,
  "lastSyncTimeStamp": "2024-01-15T10:30:00Z"
}
```

| Поле | Тип | Описание |
|------|-----|----------|
| `restaurantId` | uuid | Ресторан, который был синхронизирован |
| `isSynced` | boolean | `true`, если синхронизация завершилась успешно |
| `lastSyncTimeStamp` | datetime | Время последней успешной синхронизации (ISO 8601) |

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X POST https://api.birga-gateway.uz/api/v1/restaurants/sync-info \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Request-Id: req-012" \
  -d '{
    "restaurantId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }'
```
