<img width="256" height="256" alt="image" src="https://github.com/user-attachments/assets/780a24a5-6776-43b4-aaaf-2390a1a4f422" />

# 🧭 VentPath LOS

**Predicting ICU Length of Stay Using Clinical and Treatment Signals**

---

## 📌 Overview

VentPath LOS is a predictive modeling tool designed to estimate **ICU length of stay (LOS)** in mechanically ventilated patients using clinical, laboratory, and treatment-related variables.

The model leverages machine learning techniques to capture **nonlinear relationships and interactions**, particularly around treatment intensity and sedation patterns.

This tool is intended for:
- Risk stratification  
- Operational planning  
- Retrospective analysis  

**It is not intended for bedside clinical decision-making or causal inference.**

---

## 🧠 Model Summary

- **Model Type:** Gradient Boosting Regressor  
- **Target:** ICU Length of Stay (log-transformed)  
- **Population:** Mechanically ventilated patients  
- **Transformation:** `log1p(ICU LOS)` → predictions converted back using `expm1()`

---

## 📊 Performance

| Metric | ICU LOS |
|------|--------|
| R² | ~0.51 |
| MAE | ~3.1 days |
| RMSE | ~5.1 days |

**Key Insight:**
- ICU LOS is moderately predictable using clinical variables  
- Hospital LOS shows lower predictability due to non-clinical factors  

---

## 🔑 Key Predictors

Top contributing features (permutation importance):

- **Fentanyl exposure (dominant predictor)**
- Dexmedetomidine use
- Electrolytes (phosphate, potassium, calcium)
- Deterioration index
- Propofol use

**Notably:**
- Paralytic exposure contributes minimally to prediction
- Suggests paralytics act more as markers than drivers

---

## ⚙️ Features Used

### Treatment Variables
- Total fentanyl exposure (mcg)
- Propofol, midazolam, dexmedetomidine, morphine
- Paralytic exposure (derived)

### Clinical Variables
- Age
- BMI
- Deterioration index

### Laboratory Values
- Sodium
- Potassium
- Phosphate
- Magnesium
- Calcium

### Comorbidities
- COPD, CKD, ESRD
- Liver disease
- OSA/OHS
- Neuromuscular disorders
- Tobacco use

---

## 🔄 Derived Variables

The model dynamically derives:

- `total_paralytic_days`  
- `any_paralytic`  

From raw inputs:
- succinylcholine_days  
- vecuronium_days  
- rocuronium_days  
- cisatracurium_days  

---

## 🚀 Streamlit App

The model is deployed as a Streamlit application:

### Run locally:
```bash
streamlit run icu_los_streamlit_app.py
```

### Features:
- Interactive patient input
- Real-time ICU LOS prediction
- Risk stratification (low / moderate / high)
- Scenario analysis (fentanyl dose impact)

---

## 📈 Interpretation

Predictions represent:

> Expected ICU length of stay given observed clinical and treatment patterns

They should be interpreted as:
- **Relative risk estimates**
- Not precise duration predictions
- Not causal effects

---

## ⚠️ Limitations

- Retrospective dataset  
- Includes treatment-course variables (not early prediction)  
- Does not capture:
  - Discharge logistics  
  - Social determinants  
  - System-level factors  

---

## 🔬 Key Findings

- Fentanyl exposure is the **dominant predictor of ICU LOS**
- Evidence of **nonlinear escalation in ventilatory burden**
- Paralytics do not fully mediate fentanyl’s effect
- ICU LOS is substantially more predictable than hospital LOS

---

## 🧭 Future Directions

- Prospective validation  
- Early-phase prediction models  
- Integration with EHR systems  
- Real-time clinical decision support  

---

## 📄 License

For research and educational use only.
