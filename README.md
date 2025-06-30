# Machine Learning for Magnetic Order Classification

## Team
Ahmed Fahmy, Murod Mirzhalilov, Brandon Abrego, Sayok Chakravarty  
🔗 [GitHub Repository](https://github.com/AhmedFahmy177/MachineLearningMagneticOrderClassification/tree/main)

---

## 📌 Project Overview

As the demand for scalable, accurate, and cost-effective materials discovery grows, data-driven approaches have become essential to accelerating scientific breakthroughs. Magnetism plays a central role in a wide range of advanced technologies, including spintronic devices, magnetic memory storage, and emerging quantum information systems. However, traditional techniques—such as neutron scattering and DFT calculations—are often resource-intensive or computationally prohibitive, limiting their scalability.

This project develops a machine learning framework to predict the magnetic ordering of materials based on structural, chemical, electronic, and thermodynamic descriptors. Our strategy is two-fold:

1. **Materials Project Classifier:** We train ML models using the Materials Project (MP) database (~150,000 entries) to classify materials into magnetic ordering types. Although useful, MP labels are biased toward ferromagnetism due to limitations in DFT.

2. **MAGNDATA Classifier:** To correct this bias, we build a separate classifier using the experimentally validated MAGNDATA database (~2,100 commensurate magnetic structures) to predict the **propagation vector**, which encodes magnetic structure information. This classifier is then used to revise incorrect MP magnetic labels.

---

## 👥 Stakeholders

- Materials scientists  
- Spintronics and quantum technology developers  
- Experimental condensed matter physicists  
- Computational materials researchers  

---

## 📈 Key Performance Indicators (KPIs)

- **Accuracy:** Significant improvement over baseline (stratified dummy classifier) and the benchmark paper: *Merker et al., iScience, 2022*.
- **Throughput:** Faster predictions compared to time-consuming DFT calculations.
- **Bias Correction:** Number of mislabelled FM materials in MP reclassified via MAGNDATA predictions.

---

## 🧠 Approach

### 🔧 Feature Engineering

- Features include numerical and categorical descriptors covering structural, compositional, electronic, and thermodynamic properties.
- Dimensionality reduction via Random Forest importance, correlation analysis, and PCA.
- Categorical variables such as chemical composition were one-hot encoded at the element level.
- Final MP dataset contained ~100,000 cleaned entries.
- MAGNDATA materials used the same descriptors imported from the Materials Project.

### 📊 Training, Validation & Testing

- **Materials Project:**
  - 60% training, 20% validation, 20% testing.
  - Models: Random Forest, XGBoost, LightGBM, SVM, Logistic Regression, kNN, Decision Tree, Naive Bayes.
  - Metrics: Accuracy and F1-macro.
  - 4-fold cross-validation and GridSearchCV used for tuning.

- **MAGNDATA:**
  - 67.5% training, 22.5% validation, 10% testing.
  - Models: Random Forest, XGBoost.
  - 6-fold cross-validation.
  - Used to predict propagation vectors on MP data.

### 🔄 Subset Merging

- FM and FiM merged to reflect common literature practice.
- Magnetic element subset defined by presence of transition metals, lanthanides, or actinides.
- Enables fair benchmarking against Merker et al. (2022).

---

## 🧪 Results

- **MP Classifier:**
  - XGBoost: 89% accuracy (vs. 45% baseline), LightGBM: 67% F1-macro and 86% accuracy.
  - SMOTE improved minority class performance.
  - SHAP analysis confirmed feature contributions.
  - Models perform significantly faster than DFT.

- **MAGNDATA Classifier:**
  - Random Forest achieved 94% accuracy in predicting propagation vectors.
  - Applied to MP database, 12,609 FM-labelled materials predicted to have **non-zero propagation vectors**, suggesting likely AFM/FiM behavior → **partial correction of FM bias in MP**.

---

## 🔮 Future Work

- Incorporating features to predict noncollinear magnetic structures.
- Developing neural network models to better capture complex structure-property relationships.

---

## 📂 Repository Structure

- `data/`: Cleaned and processed datasets  
- `models/`: Trained models and configuration  
- `notebooks/`: Jupyter notebooks for training, evaluation, and visualization  
- `scripts/`: Utility scripts for data preprocessing and model inference  
- `results/`: Summary tables, plots, and benchmark comparisons  
