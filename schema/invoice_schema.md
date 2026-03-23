# Invoice JSON Schema

This schema defines the structured output for invoice extraction.

| Key | Type | Description | Handling of Absent Fields |
| :--- | :--- | :--- | :--- |
| `vendor` | string | Full legal name of the vendor. | `""` |
| `invoice_number` | string | Unique identifier. | `""` |
| `date` | string (YYYY-MM-DD) | Issue date. | `""` |
| `due_date` | string (YYYY-MM-DD) or null | Due date. | `null` |
| `currency` | string (ISO 4217) | 3-letter code. | `""` |
| `subtotal` | float | Amount before tax. | `0.0` |
| `tax` | float or null | Tax amount. | `null` |
| `total` | float | Final total. | `0.0` |
| `line_items` | array | List of items. | `[]` |

### line_items Object:
- `description` (string)
- `quantity` (number)
- `unit_price` (float)
