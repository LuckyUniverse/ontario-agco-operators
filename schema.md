# Schema — Ontario AGCO-Licensed Online Casino Operators

This document defines every column in [`data/operators.csv`](data/operators.csv) and the matching property in [`data/operators.json`](data/operators.json).

The dataset is maintained by [CasinoGPT.ai](https://casinogpt.ai) and is released under [CC BY 4.0](LICENSE).

---

## Columns

| # | Column | Type | Required | Source | Notes |
|---|---|---|---|---|---|
| 1 | `name` | string | ✅ | Operator's own site / iGaming Ontario | Trade name as shown to Ontario players (e.g. "bet365", "Jackpot City") |
| 2 | `slug` | string | ✅ | CasinoGPT-internal canonical | URL-safe lowercase identifier. Stable across updates. Used to derive `casinogpt_review_url` |
| 3 | `parent_company` | string \| null | — | AGCO operator registry | Top-level corporate parent (e.g. "Apollo Entertainment Limited", "Hillside (International Sports) ENC") |
| 4 | `registered_company` | string \| null | — | AGCO operator registry | The legal entity actually licensed in Ontario. Often a regional subsidiary |
| 5 | `licence_issuer` | string | ✅ | AGCO | Always "Alcohol and Gaming Commission of Ontario (AGCO)" — included for downstream clarity |
| 6 | `regulator` | string | ✅ | AGCO + iGaming Ontario | Always "AGCO / iGaming Ontario" |
| 7 | `jurisdiction` | string | ✅ | AGCO | Always "Ontario, Canada" |
| 8 | `ontario_launch_year` | integer \| null | — | iGaming Ontario | Year the operator was first registered with iGaming Ontario. Null where not yet captured |
| 9 | `min_age` | integer | ✅ | AGCO regulation | Always `19` per Ontario law |
| 10 | `currency` | string | ✅ | Operator site | Always `"CAD"` (Canadian Dollars) — operators must accept CAD to be eligible for AGCO licensure |
| 11 | `payment_methods` | string[] | ✅ | Operator site | Array of accepted deposit/withdrawal methods. CSV serialises as semicolon-separated. Normalised vocabulary (e.g. "Mastercard" not "MasterCard"). Sorted alphabetically |
| 12 | `withdrawal_speed` | string \| null | — | Operator site | Free-text description of typical payout time (e.g. "1-4 hours (Interac)", "1-3 business days") |
| 13 | `min_deposit` | string \| null | — | Operator site | Stated minimum deposit, including currency symbol (e.g. "$10") |
| 14 | `min_withdrawal` | string \| null | — | Operator site | Stated minimum withdrawal, including currency symbol |
| 15 | `support_channels` | string \| null | — | Operator site | Free-text description of customer-support availability (e.g. "24/7 live chat, email") |
| 16 | `games_count` | string \| null | — | Operator site | Approximate number of games (e.g. "2,000+", "550+"). String to preserve "+" suffixes |
| 17 | `primary_game_provider` | string \| null | — | Operator site | Dominant game-software provider (e.g. "Microgaming", "Evolution Gaming"), or "Multiple providers" |
| 18 | `has_sportsbook` | boolean | ✅ | Operator site | `true` if the operator offers an integrated sports betting product alongside the casino |
| 19 | `loyalty_program` | string \| null | — | Operator site | Name of the operator's VIP / loyalty programme. Null if none |
| 20 | `mobile_experience` | string \| null | — | Operator site | Free-text description of mobile offering ("Dedicated iOS and Android apps", "Mobile-optimized browser", etc.) |
| 21 | `casinogpt_review_url` | string | ✅ | Derived | Link to the full annotated review on [casinogpt.ai](https://casinogpt.ai). Always `https://casinogpt.ai/casinos/ontario/{slug}` |
| 22 | `last_updated` | string (ISO date) | ✅ | CasinoGPT-internal | Date of the most recent verification, in `YYYY-MM-DD` format |

---

## Data quality notes

- All free-text fields (`withdrawal_speed`, `support_channels`, `games_count`, `loyalty_program`, `mobile_experience`) are kept as strings rather than parsed/normalised because the original phrasing carries information that machine-friendly schemas would lose. If you need normalised data, build it on top of this dataset.
- `payment_methods` IS normalised. `MasterCard` and `Mastercard` were merged in March 2026; same for any future case variants we encounter.
- `parent_company` and `registered_company` are sometimes the same (when the licensed entity is itself the top-level company). Both columns are kept for downstream clarity.
- `ontario_launch_year` is null for older entries because iGaming Ontario's launch wave (April 2022) didn't always publish per-operator launch dates. We backfill this column over time.
- `last_updated` is a verification date — the row was confirmed correct on that day. It is **not** a "data created at" timestamp.

---

## Versioning

The dataset is versioned by the `last_updated` field on each row and by the [`CHANGELOG.md`](CHANGELOG.md) at the repository level. We do not currently tag releases — `main` always reflects the latest verified state.

If you need a frozen snapshot for a published paper or article, use a Git commit hash:

```bash
curl -O https://raw.githubusercontent.com/LuckyUniverse/ontario-agco-operators/{commit-hash}/data/operators.csv
```

---

## Questions or corrections?

[Open an issue](https://github.com/LuckyUniverse/ontario-agco-operators/issues) with a citation to a public source. We'll verify and update.

For broader questions about the Ontario regulated iGaming market, ask the [CasinoGPT chat interface](https://casinogpt.ai) — it's queryable in natural language against this same dataset (plus the proprietary annotations that aren't published here).
