# Restaurants

The Restaurants resource provides endpoints to retrieve restaurant information and synchronize data with the connected POS system.

## Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | [/api/v1/restaurants/get-restaurant/{restaurantId}](/gateway-api/restaurants/get-restaurant) | Get restaurant details by ID |
| `GET` | [/api/v1/restaurants/get-restaurant-branches/{restaurantId}](/gateway-api/restaurants/get-restaurant-branches) | List branches for a restaurant |
| `POST` | [/api/v1/restaurants/sync-info](/gateway-api/restaurants/sync-info) | Sync restaurant info with the POS system |
