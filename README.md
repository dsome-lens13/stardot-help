# Getting Started

**StarDot** is a **JSON contract layer** that governs how LLMs/agents call your APIs:
- Deterministic inputs/outputs
- Guardrails for auth, privacy, rate limits
- Redaction by default
- Traceable, observable calls

Core principles: **Access, Predictability, Safety, Efficiency, Trust**.

---

## Quick Start (5 minutes)

### 1) Write a contract
```json
{
  "name": "instrument_import",
  "version": "1.0.0",
  "description": "Safe import for lab instruments",
  "allowedEndpoints": ["POST /v1/instruments/import"],
  "allowedFields": ["instrument_id", "type", "acquired_at"],
  "disallowedFields": ["patient_name", "ssn", "dob"],
  "redact": [{ "path": "$.ssn" }, { "path": "$.dob" }],
  "confidenceThreshold": 0.9,
  "stopConditions": ["low_confidence", "invalid_field"],
  "observability": { "metrics": ["call_count","error_rate"], "trace": true },
  "businessRules": {
    "maxRetries": 2,
    "businessHours": { "start": "09:00", "end": "17:00", "timezone": "America/New_York" }
  }
}
```

### 2) Validate
```bash
curl -s https://api.stardot.ai/contracts/validate \
  -H "content-type: application/json" \
  -d @contracts/instrument_import.json | jq
```

### 3) Dry-run enforcement
```bash
curl -s https://api.stardot.ai/contracts/enforce \
  -H "content-type: application/json" \
  -d '{ "contract": { "..." }, "request": { "method": "POST", "path": "/v1/instruments/import", "confidence": 0.86, "body": { "instrument_id": "X-42", "type": "hematology", "ssn": "123-45-6789" } } }' | jq
```

### 4) Decide
- `allowed: true` → proceed
- `allowed: false, decision: "stopped"` → fix the request or relax rules intentionally
