# Purchase Order JSON Schema

This schema defines the structured output for purchase order extraction.

| Key | Type | Description | Handling of Absent Fields |
| :--- | :--- | :--- | :--- |
| `buyer` | string | Company issuing PO. | `""` |
| `supplier` | string | Vendor receiving PO. | `""` |
| `po_number` | string | PO identifier. | `""` |
| `date` | string (YYYY-MM-DD) | Issue date. | `""` |
| `delivery_date` | string (YYYY-MM-DD) or null | Delivery date. | `null` |
| `currency` | string | Currency code. | `""` |
| `total` | float | Total amount. | `0.0` |
| `items` | array | List of items. | `[]` |

### items Object:
- `item_name` (string)
- `quantity` (number)
- `unit_price` (float)
