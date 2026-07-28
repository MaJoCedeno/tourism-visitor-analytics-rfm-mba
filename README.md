# Tourism Visitor Analytics — Market Basket, Recommender System & RFM Segmentation

A consulting-style analytics project for Portugal's National Tourism Board Organization (NTBO), analyzing TripAdvisor review data to understand visitor behavior patterns and how they shifted before vs. after COVID-19, benchmarked against Portugal's main tourism competitor countries. Built for the Data Science for Marketing course at Nova IMS.

## Business Problem

Tourism was hit hard by COVID-19. The Portuguese NTBO needed to understand: who visits Portugal's top attractions, what they visit together, how similar visitors and attractions cluster, and how visitor value and behavior changed pre- vs. post-pandemic — benchmarked against competing European destinations.

## Data

- **92,120 TripAdvisor reviews** (Jan 2019–Aug 2021, English-language) covering **100 top European attractions**, plus a supplementary holidays dataset for seasonal pattern analysis.
- Fields included attraction ranking/rating, visit and review dates, user location, trip type, user contribution history, and review text.
- Significant data cleaning required: inconsistent country/ISO codes, malformed user location strings (split into city/country), outlier user-contribution values, and ambiguous attraction ID mappings resolved through text-matching against review content.

## My Contribution

I led data cleaning and preparation (location parsing, outlier treatment, ID resolution), the Market Basket Analysis, and the RFM segmentation (before/after COVID comparison), as part of a team project. Teammates led the item-based recommender system and the holiday-seasonality analysis.

## Approach

1. **Data Cleaning** — filtered to Portugal and competitor-country attractions, resolved malformed country codes (e.g., correcting Croatia/Poland ISO mismatches), split combined location strings into city/country, mapped ambiguous attraction IDs back to named attractions via text search, removed duplicate reviews while preserving legitimate repeat visits.
2. **Missing Values** — imputed missing visit dates using the median gap between visit and review dates (calculated from complete records), rather than dropping incomplete records.
3. **Market Basket Analysis** — applied the Apriori algorithm to attraction co-visitation patterns (5% minimum support), generating association rules ranked by support, confidence, and lift, separately for Portugal-only attractions and Portugal-vs-competitor-country patterns.
4. **Recommender System** — built an item-based collaborative filtering model using a customer-item interaction matrix and cosine similarity, both at the attraction level and the country level.
5. **RFM Segmentation** — calculated Recency, Frequency, and a rating-based Monetary proxy per visitor, computed independently for pre-COVID and post-COVID periods, then segmented visitors into Platinum/Gold/Silver/Bronze tiers to compare value distribution shifts across the pandemic.
6. **Seasonality Analysis** — cross-referenced visit patterns against international holidays (Christmas, Easter) to identify seasonal demand patterns.

## Key Findings

- **Market Basket Analysis** surfaced strong co-visitation patterns: Park and National Palace of Pena + Quinta da Regaleira (both in Sintra) showed a lift of **1.71**, and Mosteiro dos Jerónimos + Torre de Belém (both in Lisbon) formed the strongest single association rule in the dataset — both intuitive from geography, but useful to confirm quantitatively for bundling/marketing recommendations.
- **Recommender System** — the top attraction similar to Torre de Belém was correctly identified as Mosteiro dos Jerónimos, followed by other major landmark attractions (Park and National Palace of Pena, Sagrada Familia, Alhambra), validating the model against real-world tourist geography.
- **RFM Segmentation** — comparing pre- and post-COVID visitor tiers revealed shifts in visitor loyalty/frequency distribution, informing recommendations on which visitor segments the NTBO should prioritize for post-pandemic recovery marketing.

## Tools

Python (pandas, NumPy, mlxtend for Apriori/association rules, scikit-learn for similarity matrices), matplotlib/seaborn for visualization (including treemaps and network graphs), Google Colab.

## What I'd Improve

- Extend the recommender system with a hybrid approach (combining item similarity with user-level RFM segment) to personalize recommendations per visitor tier, not just per attraction.
- Formal significance testing on the pre/post-COVID RFM segment shifts, rather than descriptive comparison alone.
- Incorporate review sentiment (text analysis) as an additional signal, since review text was collected but not yet analyzed for sentiment in this iteration.
