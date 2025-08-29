# Contracts (JSON)

A **StarDot contract** is a versioned JSON/YAML document that governs how an agent may call your API.

## Minimal schema
- `name` (string, required)
- `allowedEndpoints` (array, required)
- `allowedFields` / `disallowedFields`
- `redact[]`
- `confidenceThreshold`
- `stopConditions[]`
- `businessRules`
- `observability`

## Example
```json
{
  "name": "meeting_scheduler",
  "allowedEndpoints": ["POST /v1/meetings"],
  "allowedFields": ["title","start_time","end_time"],
  "disallowedFields": ["ssn"],
  "redact": [{ "path": "$.ssn" }],
  "confidenceThreshold": 0.9,
  "stopConditions": ["low_confidence"]
}
```
