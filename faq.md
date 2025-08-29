# FAQ

**Is StarDot a replacement for OpenAPI?**  
No. It complements OpenAPI by adding agent behavior contracts.

**Do I need a gateway?**  
You can start with the dry-run API; enforcement at gateway recommended.

**How do I keep logs clean of PHI?**  
Use `redact[]` rules.

**What if an agent cannot meet rules?**  
Use `stopConditions` and escalate safely.
