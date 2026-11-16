# 🏦 Loan Status Predictor

A machine learning project that predicts whether a loan application will be **approved or rejected** based on applicant details, using a **Support Vector Machine (SVM)** classifier.

---

## 📁 Project Structure

```
loan prediction/
├── Loan Prediction.csv          # Dataset
├── Loan_Status_Prediction.ipynb # ML model (training & evaluation)
├── index.html                   # Frontend UI (standalone, no server needed)
└── README.md
```

---

## 📊 Dataset

- **Source:** `Loan Prediction.csv`
- **Rows:** 614 | **Columns:** 13
- **Target:** `Loan_Status` (Y = Approved, N = Rejected)

| Feature | Description |
|---|---|
| Gender | Male / Female |
| Married | Yes / No |
| Dependents | 0, 1, 2, 3+ |
| Education | Graduate / Not Graduate |
| Self_Employed | Yes / No |
| ApplicantIncome | Monthly income of applicant |
| CoapplicantIncome | Monthly income of co-applicant |
| LoanAmount | Loan amount in thousands |
| Loan_Amount_Term | Term in months |
| Credit_History | 1 = good, 0 = bad |
| Property_Area | Rural / Semiurban / Urban |

---

## 🤖 Model

- **Algorithm:** Support Vector Machine (SVM) with linear kernel
- **Library:** `scikit-learn`
- **Train/Test Split:** 90% / 10% (stratified)
- **Training Accuracy:** ~79.9%
- **Test Accuracy:** ~83.3%

### Preprocessing Steps
1. Dropped rows with missing values
2. Label encoded categorical columns (Gender, Married, Education, Self_Employed, Property_Area)
3. Replaced `3+` dependents with `4`

---

## 🖥️ Frontend

`index.html` is a **standalone** frontend — just open it in any browser, no server required.

### Prediction Logic (Frontend)
Since the model lives in the `.ipynb` file, the frontend uses rule-based logic derived from dataset patterns:

**Hard Reject (any one condition triggers rejection):**
- Bad credit history
- Zero total income
- Monthly EMI > 50% of income
- Loan amount > 6× annual income

**Soft Score (used when no hard rejects):**
- Score ≥ 3 → Approved
- Factors: credit history, debt ratio, education, marital status, property area, employment type, dependents

---

## 🚀 How to Run

### View Frontend
Just double-click `index.html` — opens directly in your browser.

### Run the Notebook
```bash
pip install numpy pandas seaborn scikit-learn jupyter
jupyter notebook Loan_Status_Prediction.ipynb
```

### To Connect Frontend to Real Model (Optional)
1. Export the trained model from the notebook:
```python
import pickle
pickle.dump(classifier, open('model.pkl', 'wb'))
```
2. Create a Flask backend (`app.py`) that loads `model.pkl` and exposes a `/predict` endpoint
3. Update `index.html` to POST form data to that endpoint

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| ML Model | Python, scikit-learn (SVM) |
| Data Processing | pandas, numpy |
| Visualization | seaborn, matplotlib |
| Frontend | HTML, CSS, JavaScript (vanilla) |

---

## 📈 Results

| Split | Accuracy |
|---|---|
| Training | 79.86% |
| Test | 83.33% |
