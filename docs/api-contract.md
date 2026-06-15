# SnackFlow API Specification v1.0

This document defines the strict data contracts between the Frontend (Client) and Backend (Server). All payloads must strictly match these keys and data types.

---

## 1. Menu Item Object
Used for rendering the digital menu for customers, managing inventory in the Admin panel, and updating the "86" switch in the Manager view.

### Data Schema (JSON)
```json
{
  "id": "prod_dosa_001",
  "name": "Masala Dosa",
  "price": 80,
  "category": "South Indian",
  "station": "Dosa Station",
  "icon": "dosa-icon-svg",
  "isAvailable": true
}

| Field Name  | Data Type | Description                                                      |
| :---        | :---      | :---                                                             |
| id          | String    | Unique product identifier prefix (e.g., prod_).                  |
| name        | String    | Display name of the item on the menu.                            |
| price       | Number    | Cost of the dish in INR.                                         |
| category    | String    | Tab grouping for customer UI navigation.                         |
| station     | String    | Assigned physical kitchen station for automatic routing.         |
| icon        | String    | String key matching the frontend SVG/Lucide library.             |
| isAvailable | Boolean   | Inventory status flag (managed by Manager/Owner).                |




## 2. Order

{
  "orderId": "A12",
  "timestamp": "2026-06-15T12:30:00.000Z",
  "paymentMode": "online", 
  "isPaid": true,
  "assemblyStatus": "waiting",
  "items": [
    {
      "productId": "prod_dosa_001",
      "name": "Masala Dosa",
      "quantity": 2
    },
    {
      "productId": "prod_beverage_002",
      "name": "Coke",
      "quantity": 1
    }
  ],
  "totalAmount": 190,
  "customerSessionId": "sess_987654321"
}


| Field Name        | Data Type    | Description                                                     |
| :---              | :---         | :---                                                            |
| orderId           | String       | Auto-generated sequential tracking ID (e.g., A12, A13).         |
| timestamp         | String (ISO) | ISO standard date-time string of when the order was placed.     |
| paymentMode       | String       | Explicitly limited to "online" or "cash".                       |
| isPaid            | Boolean      | Payment verification state. true for online; toggled for cash.  |
| assemblyStatus    | String       | Progress indicator restricted to "waiting", "ready", etc.       |
| items             | Array        | List of objects containing productId, name, and quantity.       |
| totalAmount       | Number       | Gross checkout value in INR.                                    |
| customerSessionId | String       | Unique device marker stored in browser localStorage.            |