# Получить меню

Возвращает полное меню филиала, включая категории, позиции и группы модификаторов. Данные берутся из подключённой POS-системы.

## Запрос

**`GET`** `/api/v1/menus/get-menu/{branchId}`

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
| `menuId` | string | Нет | — | Фильтр по конкретному ID меню (макс. 255 символов) |
| `itemIdsList` | string[] | Нет | — | Фильтр по конкретным ID позиций |
| `forceRefresh` | boolean | Нет | `false` | Обойти кэш и получить актуальные данные из POS |

## Ответ

### 200 OK

```json
{
  "branchId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "menuId": "menu-001",
  "isActive": true,
  "lastModified": "2024-01-15T10:30:00Z",
  "categories": [
    {
      "id": "cat-001",
      "name": "Закуски",
      "description": "Салаты и закуски",
      "isActive": true,
      "items": [
        {
          "id": "item-001",
          "name": "Салат Цезарь",
          "description": "Классический Цезарь с гренками",
          "price": 12.50,
          "imageUrl": "https://cdn.example.com/caesar.jpg",
          "isActive": true,
          "modifiers": [
            {
              "id": "mod-001",
              "name": "Дополнительная заправка",
              "price": 1.00,
              "isRequired": false,
              "minSelect": 0,
              "maxSelect": 1
            }
          ]
        }
      ]
    }
  ]
}
```

**Схема ответа:**

| Поле | Тип | Описание |
|------|-----|----------|
| `branchId` | uuid | Идентификатор филиала |
| `menuId` | string | Идентификатор меню в POS-системе |
| `isActive` | boolean | Активно ли меню в данный момент |
| `lastModified` | datetime | Время последнего изменения (ISO 8601) |
| `categories` | array | Список категорий меню |

**Объект категории:**

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | string | Идентификатор категории |
| `name` | string | Название категории |
| `description` | string | Описание категории |
| `isActive` | boolean | Активна ли категория |
| `items` | array | Список позиций в категории |

**Объект позиции:**

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | string | Идентификатор позиции |
| `name` | string | Название позиции |
| `description` | string | Описание позиции |
| `price` | number | Цена позиции |
| `imageUrl` | string | URL изображения |
| `isActive` | boolean | Доступна ли позиция |
| `modifiers` | array | Список модификаторов |

**Объект модификатора:**

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | string | Идентификатор модификатора |
| `name` | string | Название модификатора |
| `price` | number | Дополнительная стоимость |
| `isRequired` | boolean | Обязателен ли выбор |
| `minSelect` | integer | Минимальное количество выборов |
| `maxSelect` | integer | Максимальное количество выборов |

### 204 No Content

Меню для указанного филиала не найдено.

### 400 Bad Request / 500 Internal Server Error

Стандартный формат ошибки. См. [Gateway API](/ru/gateway-api/index).

## Пример

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/menus/get-menu/3fa85f64-5717-4562-b3fc-2c963f66afa6" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-020"
```
