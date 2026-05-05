# Аутентификация

Birga Gateway API использует Bearer JWT токены для аутентификации. Необходимо получить токен доступа до вызова любого эндпоинта Gateway API и передавать его в каждом запросе.

## Как это работает

```
1. POST /api/v1/auth-service/get-token  → получить accessToken + refreshToken
2. Использовать: Authorization: Bearer <accessToken> во всех запросах
3. Когда accessToken истечёт → POST /api/v1/auth-service/refresh-token
4. Для завершения сессии → POST /api/v1/auth-service/logout
```

## Время жизни токенов

| Токен | Поле | Описание |
|-------|------|----------|
| Токен доступа | `accessToken` | Краткосрочный токен для вызовов API |
| Токен обновления | `refreshToken` | Долгосрочный токен для получения нового токена доступа |
| Срок действия (доступ) | `expiresIn` | Секунды до истечения токена доступа |
| Срок действия (обновление) | `refreshExpiresIn` | Секунды до истечения токена обновления |

## Эндпоинты

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `POST` | [/api/v1/auth-service/get-token](/ru/autorization/get-token) | Получить токены доступа и обновления |
| `POST` | [/api/v1/auth-service/refresh-token](/ru/autorization/refresh-token) | Обменять токен обновления на новый токен доступа |
| `POST` | [/api/v1/auth-service/validate](/ru/autorization/create-token) | Проверить токен и получить информацию о сессии |
| `POST` | [/api/v1/auth-service/logout](/ru/autorization/logout) | Завершить текущую сессию |

## Общие заголовки

Каждый запрос к Authentication API должен содержать:

| Заголовок | Обязателен | Описание |
|-----------|-----------|----------|
| `X-Request-Id` | Да | Уникальный идентификатор запроса (макс. 255 символов) |
| `Content-Type` | Да (POST) | `application/json` |

Эндпоинты, требующие активной сессии, также требуют:

| Заголовок | Обязателен | Описание |
|-----------|-----------|----------|
| `Authorization` | Да | `Bearer <access_token>` |
