# Tennis Match Outcome Prediction – Workflow Summary

## 1. Data Collection & Cleaning (`01_data_filtering_cleaning.ipynb`)
- Loaded ATP match dataset (Jeff Sackmann’s `atp_matches_1968-2024`).
- Filtered out grand slams, 1968-2024. NaN's were handled.
- Exported `grand_slams_df.csv` for EDA.

## 2. Feature Engineering & EDA (`02_feature_engineering_eda.ipynb`)
- Created **difference features** (winner – loser) for:
  - `height_diff`, `age_diff`, `rank_diff`, `rank_point_diff`, `seed_diff`,  
    `exp_diff`, `h2h_diff`, `past_wins_diff`, `ace_diff`, `df_diff`,  
    `1stIn_diff`, `1stWon_diff`, `2ndWon_diff`.
- Explored distributions, statistical tests (t-test, Kruskal–Wallis).
- Exported `gdf.csv` for model_data_preparation.


## 3. Model Data Preparation (`03_model_data_preparation.ipynb`)
- Created **mirrored rows**: swapped `player1`/`player2`, inverted diff signs, flipped target.
- Result: balanced dataset (~50% target=1, ~50% target=0) - `Data Doubling`.
- Encoded categorical vars: `surface`, `round` (One-Hot Encoding) and scaled numerics.
- Ensured no data leakage in model.
- Exported `final_df.csv` for model_trainig.


## 4. Model Training (`model_training.ipynb`)
- Train Test Split were done.
- Models tried:
  - Logistic Regression (F1 ≈ **0.7334**)
  - Random Forest (F1 ≈ **0.7230**)
  - AdaBoost (F1 ≈ **0.7357**)
  - XGBoost (F1 ≈ **0.7409**)
- Metrics: `f1` on 5 fold CV.
- Baseline achieved: ~**74% F1** score with XGBoost.

## 6. Next Steps
- Add richer features: recent form, surface-specific stats, rest days, tournament history.
- Hyperparameter tuning for XGBoost / ensembles.

---

## References
1. Jeff Sackmann — [Tennis ATP Match Data](https://github.com/JeffSackmann/tennis_atp)  
2. Dayekh, Hattem — [Predicting Winners of Professional Women’s Tennis Grand Slams (2001–2022)](https://upcommons.upc.edu/server/api/core/bitstreams/857531e2-6593-4325-8e97-02da4879d2c3/content)  
3. Chi, Konstantin, Joakim — [Predicting Tennis Match Results Using Classification Methods](https://lup.lub.lu.se/luur/download?func=downloadFile&recordOId=9121180&fileOId=9121181)