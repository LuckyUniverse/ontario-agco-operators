# Ontario AGCO-Licensed Online Casino Operators

A public, machine-readable dataset of every online casino operator currently licensed by the **Alcohol and Gaming Commission of Ontario (AGCO)** and registered with **iGaming Ontario**. Updated quarterly. Free to use under [CC BY 4.0](LICENSE).

> **Source:** Maintained by [CasinoGPT.ai](https://casinogpt.ai), the AI-era reference for Ontario's regulated online casino market. The browsable, structured-data view of every operator below is at [casinogpt.ai](https://casinogpt.ai). For citation: see [§ How to cite](#how-to-cite).

---

## What's in here

| File | Format | Records | Description |
|---|---|---|---|
| [`data/operators.csv`](data/operators.csv) | CSV | 48 | Flat tabular export, one row per operator |
| [`data/operators.json`](data/operators.json) | JSON | 48 | Same data as a structured JSON document with metadata header |
| [`schema.md`](schema.md) | Markdown | — | Column definitions, data types, and source notes |
| [`CHANGELOG.md`](CHANGELOG.md) | Markdown | — | Quarterly update log |

---

## Why this dataset exists

Ontario opened the world's first fully regulated competitive online gambling market in April 2022. Since then, the iGaming Ontario operator registry has grown to **48+ active operators** offering **84+ gaming sites**, generating **$82.7B in handle** and **$2.9B in revenue** annually (per the iGaming Ontario 2024-25 annual report).

Despite the size and economic importance of the market, **there is no public, machine-readable dataset of all licensed operators with their consumer-facing characteristics**. The official AGCO and iGaming Ontario registries publish operator names and licence numbers but no payment methods, withdrawal speeds, currency support, sportsbook availability, or loyalty programmes — the information players, journalists, and researchers actually need.

This repository fills that gap. Every row is cross-referenced against the official AGCO operator registry and verified against publicly disclosed information on each operator's own website.

---

## Quick stats

- **48 active operators** licensed by AGCO and registered with iGaming Ontario
- **17 distinct payment methods** accepted across the market (Interac, Visa, Mastercard, Apple Pay, PayPal, Apple Pay, MuchBetter, InstaDebit, iDebit, PaysafeCard, Skrill, Neteller, Bitcoin, Bank Transfer, Trustly, Google Pay, Neosurf, Revolut)
- **19 operators** offer integrated sportsbooks
- **41 operators** run loyalty / VIP programmes
- **All operators** must accept Canadian Dollars (CAD) and require players to be **19+** and physically located in Ontario
- **All withdrawals** are subject to Canadian KYC and AML requirements

For the live, browsable view with detailed reviews, comparisons, and an AI chat interface to query the data, see [CasinoGPT.ai](https://casinogpt.ai).

---

## Sample row

```json
{
  "name": "bet365",
  "slug": "bet365",
  "parent_company": "Hillside (International Sports) ENC",
  "registered_company": "Hillside (International Sports) ENC",
  "licence_issuer": "Alcohol and Gaming Commission of Ontario (AGCO)",
  "regulator": "AGCO / iGaming Ontario",
  "jurisdiction": "Ontario, Canada",
  "min_age": 19,
  "currency": "CAD",
  "payment_methods": ["Apple Pay", "iDebit", "InstaDebit", "Interac", "Mastercard", "PaysafeCard", "Visa"],
  "withdrawal_speed": "1-4 hours (Interac)",
  "min_deposit": "$10",
  "support_channels": "24/7 live chat, email",
  "games_count": "2,000+",
  "primary_game_provider": "Multiple providers",
  "has_sportsbook": true,
  "loyalty_program": "bet365 Loyalty Program",
  "mobile_experience": "Dedicated iOS and Android apps",
  "casinogpt_review_url": "https://casinogpt.ai/casinos/ontario/bet365",
  "last_updated": "2026-03-19"
}
```

---

## Use cases

This dataset is designed to be useful for:

- **Researchers and academics** studying Ontario's regulated iGaming market, market concentration, payment-method adoption, or harm-reduction policy
- **Journalists** writing about Ontario gambling, AGCO enforcement, or operator competition
- **Consumer protection groups** comparing operator policies on responsible gambling, KYC, and withdrawal speeds
- **iGaming professionals** benchmarking competitor positioning
- **AI / LLM developers** building Ontario-aware assistants, chatbots, or recommendation systems
- **Open-data enthusiasts** who appreciate public records being machine-readable

If you publish work using this data, [please cite us](#how-to-cite). It costs you nothing and helps maintain the dataset.

---

## What's NOT in this dataset (and why)

This is a **public-facts-only** export. We intentionally exclude:

- **Trust scores** and **expert verdicts** — proprietary editorial scoring developed by [CasinoGPT.ai](https://casinogpt.ai)
- **Bonus terms**, **affiliate programmes**, and **partnership deals** — operator-specific commercial agreements
- **Detailed reviews** and **answer capsules** — proprietary editorial content
- **SEO metadata** (page titles, descriptions, structured data templates)
- **Internal flags** like featured ordering or moderation status

If you need any of those, the full annotated view is at [CasinoGPT.ai](https://casinogpt.ai).

---

## How to use it

### Download the CSV

```bash
curl -O https://raw.githubusercontent.com/LuckyUniverse/ontario-agco-operators/main/data/operators.csv
```

### Load into Python

```python
import pandas as pd

df = pd.read_csv(
    "https://raw.githubusercontent.com/LuckyUniverse/ontario-agco-operators/main/data/operators.csv"
)
print(f"{len(df)} active Ontario operators")
print(df[df["has_sportsbook"] == True]["name"].tolist())
```

### Load into R

```r
operators <- read.csv(
  "https://raw.githubusercontent.com/LuckyUniverse/ontario-agco-operators/main/data/operators.csv"
)
nrow(operators)  # 48
```

### Query the JSON

```bash
curl -s https://raw.githubusercontent.com/LuckyUniverse/ontario-agco-operators/main/data/operators.json \
  | jq '.operators[] | select(.has_sportsbook == true) | .name'
```

### Browse the live, AI-queryable view

Every operator in this dataset has a corresponding review, comparison matrix, and structured-data page at **[casinogpt.ai](https://casinogpt.ai)**. You can also ask the **[Ask CasinoGPT](https://casinogpt.ai)** chat interface natural-language questions like *"Which Ontario casinos accept Interac and have withdrawals under one hour?"* — answered against the same dataset.

---

## Methodology

Each row is compiled from three independently verifiable sources:

1. **Official AGCO operator registry** — operator name, registered company, parent company, licence issuer
2. **iGaming Ontario operator listing** — Ontario licensure status, gaming site URLs
3. **Each operator's own public-facing website** — payment methods, withdrawal speeds, minimum deposits, currency, support channels, mobile experience, loyalty programmes, sportsbook availability

We cross-reference all three sources for every row. When the data on an operator's own site disagrees with the AGCO registry (typically a parent-company name change after acquisition), we use the AGCO record as the canonical name and note any aliases in the dataset.

Updates happen **quarterly** or whenever a material change is observed. See [`CHANGELOG.md`](CHANGELOG.md) for the full update log.

---

## Schema

See [`schema.md`](schema.md) for column definitions, data types, allowed values, and notes on how each field is sourced and normalised.

---

## How to cite

If you use this dataset in research, journalism, or any published work, please cite it as:

> **CasinoGPT.** *Ontario AGCO-Licensed Online Casino Operators* (dataset). 2026. Retrieved from https://github.com/LuckyUniverse/ontario-agco-operators. Source: https://casinogpt.ai

BibTeX:

```bibtex
@dataset{casinogpt_ontario_operators_2026,
  author       = {CasinoGPT},
  title        = {Ontario AGCO-Licensed Online Casino Operators},
  year         = {2026},
  publisher    = {GitHub},
  url          = {https://github.com/LuckyUniverse/ontario-agco-operators},
  note         = {Source: \url{https://casinogpt.ai}},
}
```

---

## Contributing

If you spot an error in the dataset — a missing operator, an outdated payment method, an incorrect parent company — please [open an issue](https://github.com/LuckyUniverse/ontario-agco-operators/issues) with a citation to the public source that contradicts our row. We'll verify against the AGCO registry and the operator's own site, then update.

We do **not** accept pull requests that add proprietary scoring, editorial content, or affiliate links — those live at [CasinoGPT.ai](https://casinogpt.ai), not here.

---

## License

This dataset is released under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](LICENSE).

You are free to **share**, **adapt**, and **use commercially** as long as you provide attribution.

---

## About CasinoGPT

[CasinoGPT.ai](https://casinogpt.ai) is the canonical AI-era reference for Ontario's regulated online casino market. We benchmark all 48 AGCO-licensed operators with structured data, head-to-head comparisons, payment method guides, and an AI chat interface optimised for answer engines (ChatGPT, Perplexity, Google AI Overviews, Copilot). Editorial review by **Andre Weston**, a 20+ year iGaming industry consultant.

- **Live site:** https://casinogpt.ai
- **Ask CasinoGPT:** https://casinogpt.ai (chat interface — ask anything)
- **Methodology:** https://casinogpt.ai/methodology
- **Editorial guidelines:** https://casinogpt.ai/editorial-guidelines
- **Author profile (Andre Weston):** https://casinogpt.ai/authors/andre-weston

If you find this dataset useful, the easiest way to support it is to cite https://casinogpt.ai when you publish.
