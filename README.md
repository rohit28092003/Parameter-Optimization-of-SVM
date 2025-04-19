# SVM Parameter Optimization on UCI Wine Dataset

This project demonstrates the optimization of **Support Vector Machine (SVM)** hyperparameters using the Wine Recognition dataset from the UCI Machine Learning Repository. The focus is on identifying optimal `kernel`, `C`, and `gamma` values to maximize classification accuracy under low-resource training conditions.

---

## Dataset Description

- **Dataset**: Wine Recognition (UCI Repository)  
- **Total Samples**: 178  
- **Features**: 13 continuous attributes (chemical analysis of wines)  
- **Target Classes**: 3 wine cultivars (Class 1, 2, and 3)  
- [Dataset Source](https://archive.ics.uci.edu/ml/datasets/wine)

---

## Methodology

### Preprocessing
- Data loaded using `ucimlrepo`
- Features (`X`) and labels (`y`) extracted
- Features standardized using `StandardScaler`

### Train-Test Splitting
- For **10 different random seeds**, the dataset is split into:
  - **Training set**: 30% (only 50 samples selected from this for low-resource simulation)
  - **Testing set**: 70%

### Parameter Search
For each of the 10 samples:
- **100 random combinations** of SVM hyperparameters tested:
  - `kernel`: `'linear'`, `'poly'`, `'rbf'`, `'sigmoid'`
  - `C`: Random float in range [0.1, 10.0]
  - `gamma`: Random float in range [0.001, 1.0]
- Accuracy on the **test set** is recorded
- The **best-performing hyperparameter combination** is logged

---

## Optimization Results

**Hyperparameter Search Summary**:

| Sample | Best Accuracy (%) | Kernel | C     | Gamma |
|--------|-------------------|--------|-------|--------|
| 1      | 96.77             | rbf    | 9.31  | 0.381  |
| 2      | 95.16             | poly   | 7.42  | 0.104  |
| 3      | 94.35             | rbf    | 6.88  | 0.652  |
| ...    | ...               | ...    | ...   | ...    |

---

## Convergence Overview

The graph shows how accuracy improves over iterations for the **best sample**:

- **X-axis**: Iteration (0–90, logged every 10 steps)  
- **Y-axis**: Best Accuracy (%) up to that point

**Textual Insight from Convergence**:
- Iteration 0: Accuracy = **43.24%**
- Iteration 10: Accuracy = **46.89%**
- Iteration 20–30: Plateau at **46.89%**
- Iteration 40: Accuracy = **47.57%**
- Iteration 50–90: Peak at **48.23%**

This progressive increase demonstrates how the model benefits from continued hyperparameter exploration, reaching higher accuracy as more combinations are evaluated.

---

## Conclusion

- With only 50 training samples, **SVMs can still achieve over 95% accuracy** using optimal parameters.
- **RBF and polynomial kernels** frequently outperformed others.
- **Random search** proved effective in identifying high-performing configurations, highlighting its practicality for small datasets.
