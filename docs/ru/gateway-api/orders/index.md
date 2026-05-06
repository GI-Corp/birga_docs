# Заказы

Ресурс Заказы предоставляет эндпоинты для создания, получения, листинга и отмены заказов в подключённой POS-системе.

## Эндпоинты

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `POST` | [/api/v1/orders/create-order](/ru/gateway-api/orders/create-order) | Создать новый заказ в зале |
| `GET` | [/api/v1/orders/get-order](/ru/gateway-api/orders/get-order) | Получить детали заказа по ID |
| `GET` | [/api/v1/orders/get-order-status/{orderId}](/ru/gateway-api/orders/get-order-status) | Проверить текущий статус заказа |
| `GET` | [/api/v1/orders/get-order-list](/ru/gateway-api/orders/get-order-list) | Список заказов филиала |
| `POST` | [/api/v1/orders/cancel-order](/ru/gateway-api/orders/cancel-order) | Отменить существующий заказ |

## Объект заказа

Полный объект заказа, возвращаемый GET-эндпоинтами:

| Поле | Тип | Описание |
|------|-----|----------|
| `id` | uuid | Идентификатор заказа в Birga |
| `branchId` | uuid | Филиал, в котором создан заказ |
| `externalId` | string | ID заказа в POS-системе |
| `sessionId` | integer | Идентификатор сессии POS |
| `status` | string | Текущий статус заказа |
| `type` | string | Тип заказа (в зале, доставка и т.д.) |
| `totalItems` | integer | Общее количество позиций |
| `totalPrice` | number | Итоговая сумма заказа |
| `tableId` | integer | Номер стола |
| `tableName` | string | Название стола |
| `waiterId` | integer | ID назначенного официанта |
| `waiterName` | string | Имя назначенного официанта |
| `createdAt` | datetime | Время создания заказа |
| `updatedAt` | datetime | Время последнего обновления |
| `items` | array | Позиции заказа |
