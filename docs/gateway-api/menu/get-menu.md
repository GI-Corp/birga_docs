# Get Menu

Returns the full menu for a branch, including categories, items, and modifier groups. Data is sourced from the connected POS system.

## Request

**`GET`** `/api/v1/menus/get-menu/{branchId}`

### Headers

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `Authorization` | string | Yes | `Bearer <access_token>` |
| `X-Request-Id` | string | Yes | Unique request identifier (max 255 chars) |

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `branchId` | uuid | Yes | Branch identifier |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `menuId` | string | No | — | Filter by specific menu ID (max 255 chars) |
| `itemIdsList` | string[] | No | — | Filter by specific item IDs |
| `forceRefresh` | boolean | No | `false` | Bypass cache and fetch latest data from POS |

## Response

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
      "name": "Starters",
      "description": "Appetizers and starters",
      "isActive": true,
      "items": [
        {
          "id": "item-001",
          "name": "Caesar Salad",
          "description": "Classic Caesar with croutons",
          "price": 12.50,
          "imageUrl": "https://cdn.example.com/caesar.jpg",
          "isActive": true,
          "modifiers": [
            {
              "id": "mod-001",
              "name": "Extra dressing",
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

**Response schema:**

| Field | Type | Description |
|-------|------|-------------|
| `branchId` | uuid | Branch identifier |
| `menuId` | string | Menu identifier in the POS system |
| `isActive` | boolean | Whether the menu is currently active |
| `lastModified` | datetime | Last modification timestamp (ISO 8601) |
| `categories` | array | List of menu categories |

**Category object:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Category identifier |
| `name` | string | Category name |
| `description` | string | Category description |
| `isActive` | boolean | Whether the category is active |
| `items` | array | List of menu items in this category |

**Item object:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Item identifier |
| `name` | string | Item name |
| `description` | string | Item description |
| `price` | number | Item price |
| `imageUrl` | string | Image URL |
| `isActive` | boolean | Whether the item is available |
| `modifiers` | array | List of modifier groups for this item |

**Modifier object:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Modifier identifier |
| `name` | string | Modifier name |
| `price` | number | Additional price for this modifier |
| `isRequired` | boolean | Whether this modifier must be selected |
| `minSelect` | integer | Minimum number of selections |
| `maxSelect` | integer | Maximum number of selections |

### 204 No Content

No menu found for the given branch ID.

### 400 Bad Request

```json
{
  "code": "INVALID_PARAMETER",
  "path": "/api/v1/menus/get-menu/{branchId}",
  "message": "branchId must be a valid UUID",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### 500 Internal Server Error

```json
{
  "code": "INTERNAL_ERROR",
  "path": "/api/v1/menus/get-menu/{branchId}",
  "message": "Internal server error",
  "details": [],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Example

```bash
curl -X GET "https://api.birga-gateway.uz/api/v1/menus/get-menu/3fa85f64-5717-4562-b3fc-2c963f66afa6?forceRefresh=false" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "X-Request-Id: req-020"
```
