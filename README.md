# Getting Started

StarDot is a **JSON contract layer** that governs how LLMs/agents call your APIs.

## Why it matters
- **Rules** → endpoint allow/deny, required fields, retries, time windows  
- **Compliance** → PHI/PII redaction, blocked fields, audit trails  
- **Determinism** → stop on low-confidence, cap steps/tokens  
- **Observability** → metrics, logs, traces per agent request

## Quick start (Node/Express)
```ts
import express from "express";
import { stardotMiddleware } from "./src/middleware";

const app = express();
app.use(express.json());

app.post("/v1/instruments/import",
  stardotMiddleware("./contracts/instrument_import.json"),
  (req, res) => res.json({ ok: true })
);

app.listen(3000, () => console.log("StarDot demo on :3000"));
```

## Contract (example)
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
