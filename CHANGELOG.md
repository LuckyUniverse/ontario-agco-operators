# Changelog

All notable changes to the Ontario AGCO-Licensed Online Casino Operators dataset are documented here.

This dataset follows quarterly updates with material out-of-band updates whenever an operator joins or leaves the iGaming Ontario register.

The dataset is maintained by [CasinoGPT.ai](https://casinogpt.ai) and released under [CC BY 4.0](LICENSE).

---

## 2026-04-07 — Initial public release

- **48 active operators** exported from the CasinoGPT internal database
- **22-column schema** covering operator name, parent company, regulator, payment methods, withdrawal speed, deposit minimums, support channels, games count, primary game provider, sportsbook availability, loyalty programme, mobile experience, and a citation link to the full review at [casinogpt.ai](https://casinogpt.ai)
- Released as both **CSV** (`data/operators.csv`) and **JSON** (`data/operators.json`)
- Licensed under [CC BY 4.0](LICENSE) — free to use with attribution
- Schema documented in [`schema.md`](schema.md)
- Data sourced from the AGCO operator registry, the iGaming Ontario operator listing, and each operator's own public-facing website. Cross-referenced and verified.
- `MasterCard` / `Mastercard` payment-method variants normalised to `Mastercard`
- Payment methods sorted alphabetically within each operator row for stable diffs
