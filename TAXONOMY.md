# Taxonomy

Two-tier scheme + cross-cutting tags. Combines `eugeneyan/applied-ml`'s technique categories with
Evidently/mallahyari industry tags. Every case study gets exactly **one** `primary_category` (Tier 1),
**one** `sub_category` (Tier 2), and any number of cross-cutting `tags`.

## Tier 1 — primary capability / use case (16)

| key | name | typical sub-categories (Tier 2) |
|---|---|---|
| `rec` | Recommendation & Personalization | candidate-generation, ranking, embeddings, cold-start, sequential-transformer, multi-task, feed-ranking, notifications, personalization |
| `search` | Search, Ranking & Retrieval | query-understanding, retrieval, learning-to-rank, semantic-search, autocomplete, relevance-eval |
| `ads` | Ads & Bidding | ctr-prediction, bidding, targeting, budget-pacing, attribution, auction |
| `fraud` | Fraud, Risk & Trust/Safety | payment-fraud, account-takeover, risk-scoring, aml, abuse-detection, identity |
| `forecast` | Forecasting & ETA / Demand | demand-forecast, eta-prediction, supply-demand, inventory, capacity, time-series |
| `cv` | Computer Vision | image-classification, object-detection, ocr, visual-search, segmentation, video, vlm, embeddings |
| `nlp` | NLP & Information Extraction | classification, ner, entity-resolution, translation, summarization, sentiment, parsing, information-extraction |
| `genai` | Generative AI / LLM Apps | rag, agents, copilots, chatbots, fine-tuning, prompt-eng, eval, inference-opt, structured-output, summarization, llm |
| `audio` | Speech & Audio | asr, tts, speaker-id, audio-classification, music |
| `anomaly` | Anomaly Detection & Monitoring | outlier-detection, drift-detection, alerting, root-cause, observability |
| `optim` | Optimization & Operations | routing, pricing, matching, dispatch, logistics, allocation, bin-packing |
| `moderation` | Content Moderation & Spam | spam, toxicity, nsfw, policy-enforcement, integrity |
| `graph` | Graph & Network ML | gnn, link-prediction, community-detection, knowledge-graph, fraud-rings |
| `rl` | Reinforcement Learning | bandits, policy-optimization, rlhf, sequential-decision, simulation, uplift-modeling |
| `data` | Data & Feature Engineering | data-quality, data-pipeline, data-discovery, feature-store, labeling |
| `mlops` | MLOps / Platform / Infra | serving, platform, experimentation, model-mgmt, training-infra, efficiency, monitoring-infra, explainability, security, payments, practices, ethics, team, failures, applied-ml, data-pipeline |

## Cross-cutting tags (any number)

- **industry:** `delivery`, `mobility`, `fintech`, `media-streaming`, `e-commerce`, `social`,
  `healthcare`, `b2b-saas`, `gaming`, `travel`, `adtech`, `edtech`, `enterprise`, `dev-tools`
- **technique:** `two-tower`, `gnn`, `transformer`, `diffusion`, `distillation`, `embeddings`,
  `xgboost`, `deep-learning`, `bandits`, `llm`, `rag`, `vector-db`, `feature-store`
- **meta:** `has-architecture-diagram`, `large-scale`, `real-time`, `batch`, `cost-optimization`,
  `latency-critical`, `interview-favorite`

## Notes
- If a study spans two Tier-1 areas, pick the one that drives the system's hardest design decision and
  add the secondary area as a tag (e.g. primary `genai`, tag `search` for a RAG-over-search system).
- Keep `sub_category` from the suggested list where possible; introduce a new one only when nothing fits,
  and add it to this file in the same change.
