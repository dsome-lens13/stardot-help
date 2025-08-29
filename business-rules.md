# Business Rules & Stop Conditions

## Business rules
```json
"businessRules": {
  "maxRetries": 2,
  "businessHours": { "start": "09:00", "end": "17:00", "timezone": "America/New_York" }
}
```

## Stop conditions
- low_confidence
- invalid_field
- outside_business_hours
- max_retries_exceeded
- forbidden_endpoint
