---
id: cs0864
title: "The Making: Optimising Budget through Machine Learning"
company: Foodpanda
primary_category: forecast
sub_category: demand-forecast
year: 2024
source_url: https://medium.com/foodpanda-data/the-making-optimising-budget-through-data-analysis-3ca4d97a6d1a
tags: [demand forecasting]
---

# The Making: Optimising Budget through Machine Learning
**Foodpanda** · 2024 · [source](https://medium.com/foodpanda-data/the-making-optimising-budget-through-data-analysis-3ca4d97a6d1a)

## Problem
Foodpanda needed to model the relationship between marketing spend and Gross Merchandise Value (GMV), recognizing it follows a diminishing-returns (logarithmic) curve rather than a linear one. This is the technical companion to the project-management article "Sculpturing" (cs0855).

## Approach / System design
Evaluate multiple regression techniques to capture the curved spend→GMV relationship. A key finding was that data granularity matters: predicting at daily granularity and then aggregating up beats fitting directly at weekly/monthly levels, preserving detail and keeping error low.

## Key decisions
- Predict at daily granularity, then aggregate, to hold MAPE below ~10%.
- Model selection by elimination:
  - Linear regression couldn't capture diminishing returns.
  - Polynomial regression produced unrealistic downward slopes past the peak.
  - Tree-based models (Decision Tree, Random Forest) gave stepped, low-nuance predictions despite low error.
  - Generalised Additive Model (GAM) selected as final — smooth, interpretable, and aligned with expected business dynamics.

## Stack
Regression family explored: Linear, Polynomial, Multi-Linear, Lasso, Ridge, Elastic Net; Decision Tree and Random Forest; final choice GAM. MAPE used as the accuracy metric.

## Results
GAM achieved MAPE below the 10% threshold while producing smooth, interpretable predictions that balance flexibility and interpretability better than the alternatives.

## Takeaways
For spend-to-GMV curves, the win came from two choices: model at the finest (daily) granularity then aggregate, and pick a GAM that captures diminishing returns smoothly while staying interpretable — preferred over tree models that fit well numerically but produce non-business-like step functions.
