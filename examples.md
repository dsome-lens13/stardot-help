# Examples

## Instrument import
```json
{
  "name": "instrument_import",
  "allowed_endpoints": ["POST /v1/instruments/import"],
  "allowed_fields": ["instrument_id","type","acquired_at"],
  "disallowed_fields": ["patient_name","ssn","dob"],
  "confidence_threshold": 0.9,
  "redact": ["ssn","dob"],
  "stop_conditions": ["low_confidence","invalid_field"]
}
```
