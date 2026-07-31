---
name: crypto-price
description: "Check live crypto prices from the CryptoBoss API (multi-source USD feeds). Read-only; returns current price, 24h change, and source exchange for each requested coin."
runx:
  tags:
    - crypto
    - prices
    - read-only
  version: 0.1.0
links:
  api: https://cryptoboss.space/api/price
  spec: https://runx.ai/spec
license: MIT
---

# crypto-price

Read-only skill that fetches live USD prices for one or more cryptocurrencies
from the CryptoBoss multi-source price API.

## When to use

Use this skill when an agent needs:

- the current USD price of a coin (BTC, ETH, SOL, ...);
- the 24h percentage change;
- which exchange the feed came from.

Do not use this skill for anything that writes, trades, signs, or spends.

## Inputs

- `coins` (required): comma-separated list of coin IDs as used by the API
  (e.g. `bitcoin,ethereum`). Unknown IDs return empty entries.

## Procedure

1. Build the URL:

   ```
   https://cryptoboss.space/api/price?coins=<coins>
   ```

2. GET the URL with an HTTP client. No auth, no API key required.

3. Parse the JSON response:

   ```json
   {
     "source": "multi-source",
     "coins": "bitcoin,ethereum",
     "vs": "usd",
     "prices": {
       "bitcoin": { "usd": 64334.9, "usd_24h_change": ..., "source": "kraken" }
     }
   }
   ```

## Output

Return one line per coin:

```
bitcoin: $64334.90 (24h: +x.x%, source: kraken)
```

## Safety rules

- Read-only: never mutate, sign, send, or act on the returned data.
- Do not use the price as financial advice or a trading signal.

## Success criteria

- Response HTTP 200 and `prices` contains an entry for every requested coin
  that exists in the API.
- Output lists price, 24h change, and source exchange.
