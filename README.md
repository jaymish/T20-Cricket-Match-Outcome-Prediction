# 🏏 T20 Cricket Match Outcome Prediction Using Machine Learning

This project predicts the outcome of T20 cricket matches using only **pre‑match metadata** from the Cricsheet T20 dataset. The goal is to determine whether **Team 1** will win a match *before the match begins*, using engineered features that capture team strength, recent form, rivalry, toss impact, and home advantage. The repository includes a complete data processing pipeline, leakage‑free feature engineering, multiple machine learning models, and a full evaluation framework.

---

## 📁 Repository Structure

T20-Cricket-Match-Outcome-Prediction/  
├── data/                         — Raw Cricsheet match files + venue mapping  
├── notebooks/  
│   ├── T20_Data_Processing.ipynb — Parsing, cleaning, preprocessing  
│   ├── Feature_Engineering.ipynb — Chronological feature creation  
│   ├── Model_Training.ipynb      — ML models + evaluation  
│   └── EDA.ipynb                 — Exploratory analysis  
├── results/                      — Model outputs, tables, plots  
├── requirements.txt              — Python dependencies  
└── README.md                     — Project documentation  

---

## 📘 Dataset

This project uses the **Cricsheet T20 (male)** dataset, which contains structured match‑level metadata such as:

- Teams  
- Venue and city  
- Toss winner and toss decision  
- Match date and season  
- Match winner (used to create the target variable)

Only **pre‑match information** is used to avoid data leakage.  
A separate venue‑to‑country mapping file is used to compute **home advantage**.

---

## 🧹 Preprocessing Pipeline

The preprocessing notebook performs:

- Parsing all match files into a unified DataFrame  
- Cleaning missing or inconsistent metadata  
- Standardizing team names  
- Creating the binary target variable `team1_win`  
- Merging venue → country mapping  
- One‑hot encoding categorical variables  
- Chronological sorting to ensure leakage‑free feature creation  

---

## 🧠 Feature Engineering

All features are computed **chronologically**, meaning only past matches are used to generate features for each match.

### Contextual Features
- Toss winner  
- Toss decision  
- Home advantage  

### Performance Features
- Team strength (historical win rate)  
- Recent form (last 5 matches)  
- Season strength  

### Rivalry Features
- Overall head‑to‑head  
- Weighted head‑to‑head (recent matches weighted more)  
- Venue‑specific head‑to‑head  

### Relative Features
- `strength_diff`  
- `recent_form_diff`  
- `season_strength_diff`  

These features capture competitive dynamics between the two teams.

---

## 🤖 Machine Learning Models

The following models were trained and evaluated:

- Logistic Regression  
- K‑Nearest Neighbors  
- Support Vector Machine  
- Decision Tree  
- Random Forest  
- XGBoost  
- Deep MLP (128‑64‑32)  
- AdaBoost  

Each model was evaluated using:

- Accuracy  
- Precision  
- Recall  
- F1 Score  

---

## 📊 Results Summary

Logistic Regression achieved the highest F1 score, followed closely by XGBoost and the Deep MLP.

Tree‑based models (Random Forest, AdaBoost) performed moderately well, while KNN struggled due to high‑dimensional one‑hot encoded inputs.

A full results table is available in the `Model_Training.ipynb` notebook.

---

## 🧩 Why Logistic Regression Performs Best

The engineered features (strength differences, form differences, rivalry metrics, home advantage) are largely **linear and additive**, making Logistic Regression a natural fit.

More complex models capture nonlinear interactions but do not significantly outperform the simpler baseline because the dataset’s predictive structure is already well‑captured by linear relationships.

---

## 🚀 Future Improvements

- Add a soft voting ensemble combining LR + XGBoost + MLP  
- Add SHAP values for model interpretability  
- Extend to women’s T20 or ODI formats  
- Deploy as a web app (Streamlit or FastAPI)  

---

## 📦 Installation

```bash
git clone https://github.com/jaymish/T20-Cricket-Match-Outcome-Prediction
cd T20-Cricket-Match-Outcome-Prediction
pip install -r requirements.txt
```

## ▶️ Running the Project

Open the notebooks in the following order:

1. `T20_Data_Processing.ipynb`
2. `Feature_Engineering.ipynb`
3. `Model_Training.ipynb`

---

## 📜 License

This project uses the open Cricsheet dataset.  
All code is released under the MIT License.

---

## 👤 Author

**Jaymish Patel**  
Machine Learning Project — Saint Peter’s University





