# Orders

The Orders resource provides endpoints to create, retrieve, list, and cancel orders in the connected POS system.

## Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | [/api/v1/orders/create-order](/gateway-api/orders/create-order) | Create a new dine-in order |
| `GET` | [/api/v1/orders/get-order](/gateway-api/orders/get-order) | Get order details by ID |
| `GET` | [/api/v1/orders/get-order-status/{orderId}](/gateway-api/orders/get-order-status) | Check current order status |
| `GET` | [/api/v1/orders/get-order-list](/gateway-api/orders/get-order-list) | List orders for a branch |
| `POST` | [/api/v1/orders/cancel-order](/gateway-api/orders/cancel-order) | Cancel an existing order |

## Order Object

The full order object returned by GET endpoints:

| Field | Type | Description |
|-------|------|-------------|
| `id` | uuid | Birga order identifier |
| `branchId` | uuid | Branch where the order was placed |
| `externalId` | string | Order ID in the connected POS system |
| `sessionId` | integer | POS session identifier |
| `status` | string | Current order status |
| `type` | string | Order type (dine-in, delivery, etc.) |
| `totalItems` | integer | Total number of items |
| `totalPrice` | number | Total order price |
| `tableId` | integer | Table number |
| `tableName` | string | Table name |
| `waiterId` | integer | Assigned waiter ID |
| `waiterName` | string | Assigned waiter name |
| `createdAt` | datetime | Order creation timestamp |
| `updatedAt` | datetime | Last update timestamp |
| `items` | array | Order line items |
