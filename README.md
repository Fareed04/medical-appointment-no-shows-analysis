# 🏥 Medical Appointment No-Shows: Predictive Analysis for Healthcare Operations

This project analyzes patient absenteeism in the Brazilian healthcare system and builds a **cost-sensitive predictive model** to reduce wasted clinical capacity caused by missed appointments.

Using **110,000+ medical records**, the analysis moves from exploratory insights to a decision-oriented machine learning model that prioritizes **operational impact over raw accuracy**.

**Data Source:** Kaggle – Medical Appointment No Shows  
https://www.kaggle.com/datasets/joniarroba/noshowappointments

---

## 🎯 Business Problem

Missed medical appointments create a **double operational loss**:
- Idle clinician time and underutilized facilities  
- Longer patient wait times and scheduling inefficiencies  

With approximately **1 in 5 appointments missed**, even small improvements in attendance prediction can unlock significant efficiency gains.

This project asks:
- *Who is most likely to miss an appointment?*
- *Why do they miss?*
- *How can prediction support better scheduling decisions?*

---

## 📊 Phase 1: Exploratory Data Analysis

The exploratory phase focused on identifying **behavioral and operational drivers** of no-shows.

---

### 1️⃣ Baseline Absenteeism Rate

The dataset shows a **20.2% no-show rate**, meaning roughly **one out of every five appointments** is missed.

![Ratio of Shows to No-Shows](images/ratio_of_shows_to_no-shows.png)

This establishes a strong baseline opportunity for intervention.

---

### 2️⃣ Demographic Risk Patterns (Age vs Gender)

- **Age is a strong predictor** of attendance behavior  
- Patients aged **19–35** exhibit the highest no-show rates  
- **Gender has no meaningful effect** on absenteeism

![Probability of Missing Appointment by Age and Gender](images/Probability_of_Missing_an_Appointment_by_Age_and_Gender.png)

This indicates that intervention strategies should focus on **life-stage behavior**, not gender-based assumptions.

---

### 3️⃣ The SMS Reminder Paradox

Patients who received SMS reminders were **more likely** to miss appointments.

![No-Show Rate by SMS Status](images/No-Show_Rate_by_SMS_Status.png)

Further investigation revealed the root cause:
- SMS reminders are disproportionately sent for appointments with **long scheduling lead times**
- **Waiting time friction**, not reminder absence, drives absenteeism

This reframes SMS from a “solution” to a **proxy indicator of scheduling risk**.

---

### 4️⃣ Geographic Concentration of No-Shows

- **Jardim Camburi** has the highest *absolute* number of no-shows  
- Several smaller neighborhoods show higher *percentage-based* risk

![Top 10 Neighbourhoods with the Most No-Shows](images/Top_10_Neighbourhoods_with_the_Most_No-Shows.png)

This enables two intervention paths:
- High-volume targeting
- High-risk precision targeting

---

## ⚙️ Phase 2: Feature Engineering & Preprocessing

To support predictive modeling, the dataset was transformed into an analysis-ready format:

- **Waiting Time Engineering**  
  Converted appointment timestamps into a `waiting_days` feature capturing lead time friction

- **Categorical Encoding**  
  One-Hot Encoded `Neighbourhood` (80+ unique values) to preserve geographic signal

- **Feature Scaling**  
  Standardized numerical features such as `Age` and `waiting_days` to stabilize model learning

---

## 🤖 Phase 3: Machine Learning with Operational Constraints

### The Core Challenge: Class Imbalance

The target variable is heavily imbalanced:
- ~80% Show
- ~20% No-Show

---

### Baseline Model: Accuracy Without Usefulness

A standard Logistic Regression achieved **80% accuracy** but only **1% recall** for no-shows.

This model effectively predicts “Show” for everyone, making it **operationally useless**.

---

### Final Model: Cost-Sensitive Logistic Regression

Using `class_weight='balanced'`, the model was optimized to **prioritize identifying no-shows**, accepting lower accuracy in exchange for actionable recall.

| Metric | Baseline Model | Balanced Model |
|------|---------------|----------------|
| Accuracy | 80% | 57% |
| No-Show Recall | 1% | **86%** |
| No-Show Precision | 42% | 30% |

**Key Result:**  
The final model correctly identifies **86% of missed appointments**, enabling proactive intervention rather than passive reporting.

---

## 🔍 Model Interpretation: What Drives No-Shows

Model coefficients were analyzed to ensure interpretability:

- **Increased No-Show Risk**
  - Long waiting times
  - Certain neighborhoods
  - Alcoholism indicator

- **Increased Attendance Likelihood**
  - Same-day appointments (strongest effect)
  - Short lead times

This confirms that **scheduling design**, not patient reminders alone, is the dominant driver of absenteeism.

---

## 💡 Operational Recommendations

Based on the analysis:

1. **Risk-Based Outreach**  
   Prioritize manual confirmation for patients aged **19–35** with **waiting times > 10 days**

2. **Geographic Pilots**  
   Test same-day confirmation workflows in **Jardim Camburi**

3. **Controlled Overbooking**  
   Use high-recall predictions to safely overbook **10–15%** of high-risk appointment slots

These actions directly convert prediction into **capacity recovery and efficiency gains**.

---

## 🛠️ Technical Stack

- Pandas, NumPy  
- Matplotlib, Seaborn  
- Scikit-Learn  
- Jupyter Notebook  

---

## 📬 Contact

**Fareed Ologundudu**  
LinkedIn: https://www.linkedin.com/in/fareed-ologundudu-129506249/  
GitHub: https://github.com/Fareed04