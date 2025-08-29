# Examples

## Instrument Import
```json
{
  "name": "instrument_import",
  "allowedEndpoints": ["POST /v1/instruments/import"],
  "allowedFields": ["instrument_id","type","acquired_at"],
  "disallowedFields": ["patient_name","ssn","dob"],
  "redact": [{ "path": "$.ssn" }, { "path": "$.dob" }]
}
```

## Meeting Scheduler
```json
{
  "name": "meeting_scheduler",
  "allowedEndpoints": ["POST /v1/meetings"],
  "allowedFields": ["title","start_time","end_time"],
  "disallowedFields": ["attendee_emails_private"]
}
```
