# Cardiac Arrhythmia Classification Project

## Overview
This project focuses on analyzing and modeling the **Cardiac Arrhythmia Dataset** to classify ECG records into 16 classes of arrhythmia. The dataset consists of **452 instances** and **278 features**, including patient demographics, heart rate, QRS intervals, and waveform measurements from multiple ECG leads.

The main objectives are:
- Preprocess and clean the dataset.
- Handle missing values and imbalanced classes.
- Reduce dimensionality using PCA.
- Build machine learning pipelines with multiple classifiers.
- Evaluate model performance using accuracy, precision, recall, and F1 scores.

---

## Dataset
- **Source:** Cardiac Arrhythmia Database, donated by H. Altay Guvenir, Bilkent University.
- **Attributes:** 278 (206 numeric, the rest nominal).
- **Instances:** 452
- **Class distribution:** 16 classes ranging from Normal to different arrhythmias and unclassified conditions.

### Notable Features
- Demographics: `Age`, `Sex`, `Height`, `Weight`
- ECG intervals: `QRS_Dur`, `P-R_Int`, `Q-T_Int`, `T_Int`, `P_Int`
- Waveform amplitudes and angles across leads: `DI`, `DII`, `DIII`, `V1-V6`, `AVR`, `AVL`, `AVF`
- Class label: `V6279` (16 arrhythmia categories)

---

## Preprocessing
1. **Missing Values**  
   - Replaced `?` with `NaN` and checked for nulls.

2. **Feature Engineering**
   - Separated numeric and categorical columns.
   - Removed class column from feature set.
   - No encoding was required for `Sex` as it is already 0/1.

3. **Dimensionality Reduction**
   - Applied **PCA** to numeric features (~95% variance retention).
   - Reduced 278 features to a smaller number for better model performance.

4. **Handling Imbalanced Classes**
   - Oversampled minority classes using **RandomOverSampler** from `imblearn`.

5. **Normalization / Scaling**
   - StandardScaler applied to numeric columns via `ColumnTransformer` in the pipeline.

---

## Models and Pipelines
The following machine learning models were trained using a pipeline:

| Model | Description |
|-------|-------------|
| KNN | k-Nearest Neighbors Classifier |
| Logistic Regression | Logistic Regression (`solver='saga'`) |
| Decision Tree | Decision Tree Classifier (`max_depth=5`) |
| Linear SVC | Linear Support Vector Classifier |
| Kernel SVC | SVC with sigmoid kernel |
| Random Forest | Random Forest Classifier (`n_estimators=200, max_depth=10`) |

- All models were trained **after PCA and oversampling**.
- Pipelines included preprocessing, PCA, and the classifier.

---

## Results
| Model | Train Accuracy | Test Accuracy |
|-------|----------------|---------------|
| KNN | 0.814 | 0.022 |
| Logistic Regression | 0.492 | 0.022 |
| Decision Tree | 0.026 | 0.000 |
| Linear SVC | 0.650 | 0.015 |
| Kernel SVC | 0.863 | 0.044 |
| Random Forest | 0.176 | 0.007 |

**Observations:**
- The models show **very low test accuracy**, indicating that the dataset is challenging due to:
  - Extreme class imbalance (e.g., class 1 has 245 instances, class 7/8 have only 2–3 instances).
  - High dimensionality of waveform features.
- Kernel SVC and KNN performed slightly better than others on the test set but still **require improvement**.
- Oversampling and PCA help, but further **feature engineering or model tuning** is needed.

---

## Future Improvements
1. **Advanced Feature Engineering**
   - Aggregated waveform features (e.g., average amplitude per lead, QRS area, HRV).
   - Domain-specific features from ECG signals.

2. **Cross-Validation & Weighted Metrics**
   - Use weighted precision, recall, and F1-score for imbalanced classes.

3. **Hyperparameter Tuning**
   - GridSearchCV or RandomizedSearchCV for optimal model parameters.

4. **Ensemble Methods**
   - Try XGBoost, LightGBM, or stacked ensembles.

---

## Notes
- PCA and scaling were applied **after oversampling** to avoid data leakage.
- Categorical encoding was not required beyond `Sex` as it was already numeric.
- All experiments were done using **Python 3.12**, `scikit-learn`, `imblearn`, `pandas`, and `matplotlib`.

---

## References

- [Cardiac Arrhythmia Dataset](https://archive.ics.uci.edu/ml/datasets/arrhythmia)

---
