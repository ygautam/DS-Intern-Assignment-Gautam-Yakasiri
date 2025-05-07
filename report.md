##  Final Report: Predicting Equipment Energy Consumption

###  Data Preprocessing Summary

* Removed invalid humidity values (>100%) and replaced them with column means.
* Dropped rows with missing timestamp features after verification.
* Outliers were handled using IQR-based filtering and visual analysis.
* Data contained 20 days of records with varying timestamps (no time pattern observed).

###  Feature Importance (via Random Forest)

Top predictors of equipment energy usage:

1. `zone5_humidity`
2. `zone8_humidity`
3. `zone1_humidity`
4. `outdoor_humidity`
5. `zone9_humidity`

These features contributed significantly to model accuracy, especially in tree-based models.

###  Top 10 Correlated Features with Equipment Energy Usage

From Pearson correlation:

```
1. zone2_temperature:       0.047
2. zone3_temperature:       0.039
3. zone6_temperature:       0.037
4. zone1_humidity:          0.036
5. zone1_temperature:       0.030
6. zone4_temperature:       0.024
7. zone3_humidity:          0.019
8. zone8_temperature:       0.013
9. zone9_temperature:       0.010
10. visibility_index:       0.004
```

> Insight: Correlation coefficients are low overall, suggesting non-linear dependencies. This aligns with higher feature importance scores seen in ensemble models.

### Random Variables

* `random_variable1` and `random_variable2` had:

  * Low correlation with target
  * Moderate importance in ensemble models

> They can be retained for model variety, but are not essential for linear interpretation.

### High-Impact Zones Identified

* Humidity:

  * Zone 5, Zone 8, and Zone 1 are the most significant humidity contributors.
* Temperature:

  * Zone 2, Zone 3, and Zone 6 have the highest correlation with equipment energy.

> Recommendation: Focus on environmental controls in Zone 5 (humidity) and Zone 2 (temperature) to optimize equipment energy efficiency.

---

### Model Performance Summary

| Model             | MSE       | R² Score |
| ----------------- | --------- | -------- |
| Random Forest     | 17,341.38 | 0.134    |
| Gradient Boosting | 18,351.69 | 0.084    |
| XGBoost           | 18,698.92 | 0.066    |
| SVM               | 20,991.61 | -0.048   |

> Best Model: Random Forest (lowest MSE and highest R²)

---

### Conclusion & Recommendations

* Ensemble models outperform SVM, confirming the dataset’s nonlinear nature.
* Focus on Zone 2/3 temperatures for control strategies.
* Humidity in Zone 5 and Zone 8 emerged as the most impactful features in Random Forest’s nonlinear predictions, even though their linear correlations with energy usage were weak.
* Consider retraining with additional data or engineered features (e.g., interaction terms, time-window aggregations) to improve R².
