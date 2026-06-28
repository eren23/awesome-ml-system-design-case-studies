# ML System Design Case Studies

A categorized, de-duplicated catalog of real-world ML & AI system design case studies — company
engineering write-ups of how production ML systems are actually built.

## Stats

- **2079** case studies · **340** companies · **16** categories · spanning **2003–2026**

## Browse

- **[INDEX.md](INDEX.md)** — everything, grouped by category (newest first)
- **[RECENT.md](RECENT.md)** — most recently added + counts by year
- **[categories/](categories/)** — one page per category
- **[notes/](notes/)** — structured deep-dive notes on selected studies (problem · system design · key decisions · stack · results · takeaways), growing over time
- **[data/case_studies.csv](data/case_studies.csv)** — the raw data (filter/query however you like)

## Example entries

| Title | Company | Category | Year |
|---|---|---|---|
| [Artwork Personalization at Netflix](https://netflixtechblog.com/artwork-personalization-c589f074ad76) | Netflix | rec / personalization | 2017 |
| [A primer on machine learning for fraud detection](https://stripe.com/guides/primer-on-machine-learning-for-fraud-protection) | Stripe | fraud / risk-scoring | 2021 |
| [A scalable LLM approach to enhancing chatbot knowledge with UGC](https://careersatdoordash.com/blog/doordash-llm-chatbot-knowledge-with-ugc/) | DoorDash | genai / chatbots | 2025 |

…and ~2,000 more in [INDEX.md](INDEX.md).

## Categories

16 top-level categories (see **[TAXONOMY.md](TAXONOMY.md)** for sub-categories + tags): Recommendation &
Personalization · Search/Ranking/Retrieval · Ads & Bidding · Fraud/Risk/Trust & Safety · Forecasting &
ETA/Demand · Computer Vision · NLP & Information Extraction · Generative AI / LLM Apps · Speech & Audio ·
Anomaly Detection · Optimization & Operations · Content Moderation · Graph & Network ML · Reinforcement
Learning · MLOps / Platform / Infra.

## Data model

`data/case_studies.csv` — one row per study:

`id, title, company, industry, primary_category, sub_category, tags, year, source_url, origin_source, date_added, summary_oneliner`

Dedup key = normalized source URL, or normalized company + title.

## Credits

Aggregated and de-duplicated from:
[Evidently AI's ML system design database](https://www.evidentlyai.com/ml-system-design) ·
[mallahyari/ml-practical-usecases](https://github.com/mallahyari/ml-practical-usecases) ·
[eugeneyan/applied-ml](https://github.com/eugeneyan/applied-ml) (taxonomy basis) ·
[Engineer1999/A-Curated-List-of-ML-System-Design-Case-Studies](https://github.com/Engineer1999/A-Curated-List-of-ML-System-Design-Case-Studies) ·
[Chip Huyen's case studies](https://huyenchip.com/machine-learning-systems-design/case-studies.html) ·
and company engineering blogs. All credit for the underlying write-ups belongs to their authors.

## License

[MIT](LICENSE) for the catalog data. Linked articles remain © their respective owners.
