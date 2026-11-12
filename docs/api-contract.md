# API contract

**Owner:** API, quality & cloud · **Status:** DRAFT. Matches the current mock; agree changes with backend + frontend before building.

## GET /health
`200` → `{ "status": "healthy" }`

## POST /calculate

### Request
```json
{
  "spending": [
    { "category": "Travel", "amount": 25.00 },
    { "category": "Food", "amount": 40.00 }
  ]
}
```

| Field | Type | Rules (current) | To decide |
|---|---|---|---|
| `spending` | array | at least 1 item | max items? |
| `category` | string | non-empty | restrict to allowed list (Travel, Food, Utilities, …)? subcategory? |
| `amount` | number (GBP) | ≥ 0 | upper limit? decimal places? |
| — | — | — | `customerId`, `month` (`YYYY-MM`)? reject unknown fields? |

### Response `200` (Sprint 1 mock)
```json
{
  "status": "success",
  "totalCarbonKg": 0,
  "breakdown": [ { "category": "Travel", "amount": 25.0, "carbonKg": 0 } ],
  "recommendations": []
}
```

### Status codes
| Code | When |
|---|---|
| 200 | Valid request |
| 422 | Validation failed (FastAPI default; body lists the invalid fields) |
| 500 | Unexpected error: generic message only, never a stack trace |
