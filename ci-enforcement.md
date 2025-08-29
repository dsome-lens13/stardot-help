# CI & Enforcement

## CI validation
```yaml
name: Validate StarDot Contracts
on: [push, pull_request]
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: "20" }
      - run: npm ci || npm i
      - run: npx ts-node tools/validate-contracts.ts contracts/
```

## Gateway enforcement (Node/Express)
```ts
import express from "express";
import { stardotMiddleware } from "./src/middleware";
const app = express();
app.use(express.json());
app.post("/v1/instruments/import", stardotMiddleware("./contracts/instrument_import.json"), (req,res)=>res.json({ok:true}));
app.listen(3000);
```
