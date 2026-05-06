# Рестораны

Ресурс Рестораны предоставляет эндпоинты для получения информации о ресторанах и синхронизации данных с подключённой POS-системой.

## Эндпоинты

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `GET` | [/api/v1/restaurants/get-restaurant/{restaurantId}](/ru/gateway-api/restaurants/get-restaurant) | Получить данные ресторана по ID |
| `GET` | [/api/v1/restaurants/get-restaurant-branches/{restaurantId}](/ru/gateway-api/restaurants/get-restaurant-branches) | Список филиалов ресторана |
| `POST` | [/api/v1/restaurants/sync-info](/ru/gateway-api/restaurants/sync-info) | Синхронизировать данные с POS-системой |
