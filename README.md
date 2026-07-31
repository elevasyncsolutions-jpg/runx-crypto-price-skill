# runx-crypto-price-skill

A [runx](https://runx.ai) skill: check live crypto prices from the
[CryptoBoss](https://cryptoboss.space) multi-source API.

A skill is a portable `SKILL.md` contract that a human can understand and an
agent can run under governed authority. This one is read-only: it fetches USD
prices, 24h change, and the source exchange for any coin the API supports.

## Usage

```bash
npm i -g @runxhq/cli
runx run crypto-price --input '{"coins": "bitcoin,ethereum"}'
```

Or browse it from the runx catalog at <https://runx.ai/x>.

## What the skill does

1. GET `https://cryptoboss.space/api/price?coins=<coins>`
2. Parse `prices.<coin>.usd`, `usd_24h_change`, and `source`
3. Return one line per coin

## Why runx

- **Explicit skill**: the contract is a single reviewable `SKILL.md`.
- **Bounded authority**: read-only surface, no keys, no writes.
- **Receipts**: every run leaves a signed receipt proving what happened.

## License

MIT
