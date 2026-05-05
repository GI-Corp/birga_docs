# Birga Gateway API

Birga — единый интеграционный шлюз, подключающий ваш бизнес к нескольким POS-системам. Один API, одна панель управления, без привязки к конкретному поставщику.

<img src="/img/birga.png" alt="Birga Gateway API" style="max-width: min(820px, 100%); height: auto; display: block;">

## Что такое Birga?

Birga предоставляет унифицированный интеграционный слой для работы с R-Keeper, Poster, IIKO и другими POS-системами через единый согласованный интерфейс. Мы берём на себя протоколы, повторные попытки и маппинг данных, чтобы вы могли сосредоточиться на своём продукте.

### Поддерживаемые POS-системы

- [RKeeper](https://rkeeper.uz/)
- [Poster](https://joinposter.com/)
- [IIKO](https://iikosoftware.uz/)

## Быстрый старт

1. Получите учётные данные у команды Birga
2. [Получите токен доступа](/ru/autorization/get-token)
3. Начните вызывать Gateway API

## Общие заголовки

Все запросы к API требуют следующих заголовков:

| Заголовок | Обязателен | Описание |
|-----------|-----------|----------|
| `Authorization` | Да | `Bearer <access_token>` |
| `X-Request-Id` | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | Да (POST) | `application/json` |

## Аутентификация

Базовый путь: `/api/v1/auth-service`

API использует Bearer JWT токены. Получите токен по учётным данным и передавайте его в заголовке `Authorization` при каждом запросе.

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `POST` | `/api/v1/auth-service/get-token` | Получить токены доступа и обновления |
| `POST` | `/api/v1/auth-service/refresh-token` | Обновить истёкший токен доступа |
| `POST` | `/api/v1/auth-service/validate` | Проверить токен и получить информацию о сессии |
| `POST` | `/api/v1/auth-service/logout` | Завершить текущую сессию |

## Gateway API

Базовый путь: `/api/v1`

### Рестораны

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `GET` | `/api/v1/restaurants/get-restaurant/{restaurantId}` | Получить данные ресторана по ID |
| `GET` | `/api/v1/restaurants/get-restaurant-branches/{restaurantId}` | Список филиалов ресторана (с пагинацией) |
| `POST` | `/api/v1/restaurants/sync-info` | Синхронизировать данные с POS-системой |

### Филиалы

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `GET` | `/api/v1/branches/get-branch/{branchId}` | Получить данные филиала по ID |

### Меню

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `GET` | `/api/v1/menus/get-menu/{branchId}` | Получить меню филиала с категориями и позициями |

### Заказы

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `POST` | `/api/v1/orders/create-order` | Создать новый заказ в зале |
| `GET` | `/api/v1/orders/get-order` | Получить детали заказа по ID |
| `GET` | `/api/v1/orders/get-order-status/{orderId}` | Проверить текущий статус заказа |
| `GET` | `/api/v1/orders/get-order-list` | Список заказов филиала (с пагинацией) |
| `POST` | `/api/v1/orders/cancel-order` | Отменить существующий заказ |

### Доставка

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `POST` | `/api/v1/delivery/create-order` | Создать заказ на доставку |

## Нужна помощь?

- [Changelog](/changelog)
- Контакт: [gicorp.work@gmail.com](mailto:gicorp.work@gmail.com) | Telegram: [@islomcodes](https://t.me/islomcodes)
