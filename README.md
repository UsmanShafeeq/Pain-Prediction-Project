# 🩺 Pain Prediction Project – Summary

**Author:** Usman Shafeeq  
**Email:** usmanshafeeqit@gmail.com  
**Location:** Rahim Yar Khan, Punjab, Pakistan  

---

## 📊 Dataset Overview
- **Source:** Empatica E4 wearable device  
- **Participants:** 200 subjects  
- **Samples:** 96,000 rows at 4Hz sampling rate  
- **Features:**  
  - Motion: `acc_x`, `acc_y`, `acc_z`  
  - Physiological: `eda`, `bvp`, `hr`, `temp`  
  - Target: `pain_scale` (1–8, self-reported)

**Remarks:** Well-structured dataset, no missing values, suitable for regression and time-series modeling.

---

## 📝 Data Processing
- Converted `person_ID` to numeric codes  
- Filled missing values (forward fill; none existed)  
- Feature engineering:  
  - `movement` = √(acc_x² + acc_y² + acc_z²)  
  - Rolling averages: `hr_mean_5`, `eda_mean_5`, `temp_mean_5`  
- Final features: 11 (raw + movement + rolling averages)  
- Train-test split: 80-20 sequential split  

**Remarks:** Rolling averages help capture temporal patterns and stabilize features.

---

## 🤖 Models Implemented

### 1️⃣ Random Forest Regressor
- 11 input features  
- **Performance:**  
  - MAE: 0.94  
  - RMSE: 1.16  
  - R²: 0.73  
- **Top Features:** BVP, EDA, HR, Temp, Movement  

**Comment:** Works well as a baseline; interpretable feature importance.

### 2️⃣ LSTM (Time-Series Model)
- Architecture: LSTM(64) → Dense(32, ReLU) → Dense(1)  
- Training: 5 epochs, batch size 32, Adam optimizer, MSE loss  
- **Performance:**  
  - MAE: 0.95  
  - RMSE: 1.17  
  - R²: 0.73  

**Comment:** Captures temporal dependencies but slightly slower than RF.

---

## 🎯 Prediction Function
- `predict_and_evaluate()`  
- Input: Single sensor reading (11 features)  
- Output:  
  - Random Forest & LSTM predictions  
  - Pain category: 🟢 Low (1–3), 🟡 Moderate (4–6), 🔴 High (7–8)  
  - Model comparison and better model identification  

**Remarks:** Suitable for real-time pain prediction from wearable devices.

---

## 📊 Key Findings
- RF slightly outperforms LSTM (MAE 0.94 vs 0.95)  
- Both models explain ~73% variance (R² = 0.73)  
- Important features: BVP, EDA, HR, Temp, Movement  
- Predictions accurate within ~1 pain point  

**Comment:** Both models are practical; RF slightly more stable.

---

## 💡 Applications
- Real-time wearable pain monitoring  
- Personalized pain assessment tools  
- Remote patient monitoring  

**Remarks:** Can be integrated into healthcare applications and clinical monitoring systems.

---

## 🚀 Future Improvements
- Hyperparameter tuning for both models  
- Personalized per-patient models using `person_ID`  
- Deeper LSTM/GRU architectures  
- Classification-based pain categories  
- Ensemble approaches combining RF + LSTM  

---

## 📦 Dependencies
- `numpy`, `pandas` – data processing  
- `matplotlib`, `seaborn` – visualization  
- `scikit-learn` – Random Forest, metrics, scaling  
- `tensorflow/keras` – LSTM implementation  

---

## 🎉 Conclusion
- Complete ML pipeline implemented: Data processing ✓, Feature engineering ✓, Random Forest ✓, LSTM ✓, Evaluation ✓, Prediction function ✓  
- Achieved MAE ≈ 0.95 (1–8 scale), R² = 0.73  
- Random Forest slightly better, LSTM captures temporal patterns  
- **Remarks:** Demonstrates real-world pain monitoring with wearable sensors.
