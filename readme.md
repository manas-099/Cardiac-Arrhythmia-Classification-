# Cardiac Arrhythmia Classification Project

## Overview
This project focuses on analyzing the **Cardiac Arrhythmia Dataset** to classify ECG records into 16 classes of arrhythmia. The dataset consists of **452 instances** and **278 features**, including patient demographics, heart rate, QRS intervals, and waveform measurements from multiple ECG leads.

The main objectives are:
- Preprocess and clean the dataset.
- Handle missing values and imbalanced classes.
- Reduce dimensionality using PCA.


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


---





## References

- [Cardiac Arrhythmia Dataset](https://archive.ics.uci.edu/ml/datasets/arrhythmia)

---
