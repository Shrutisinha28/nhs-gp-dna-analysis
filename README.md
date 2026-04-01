# NHS GP Appointment DNA Analysis & Predictive Modelling

## Overview
This project investigates the Did Not Attend (DNA) problem across the NHS GP 
services in England, using 30 months of national appointment data 
(July 2023 – December 2025). It quantifies the financial cost of missed 
appointments and builds a machine learning model to predict individual 
no-show risk.

---

## Project Structure

```nhs-gp-dna-analysis/
│
├── data/
│   ├── GP_DNA_Monthly_Dataset_Uncleaned.xlsx   # NHS GP monthly dataset
│   └── KaggleV2-May-2016.csv                  # Kaggle no-show dataset
│
├── notebooks/
│   ├── section1_eda.ipynb                     # Demand, mode, wait, DNA analysis
│   ├── section2_cost_analysis.ipynb           # Cost impact analysis
│   └── section3_modelling.ipynb               # Predictive modelling (InProgress)
│
├── charts/                                   # Exported visualisations
├── requirements.txt
└── README.md
```
---

## Sections

### Section 1 — NHS GP Service Context & EDA
An exploratory analysis of 30 months of NHS GP appointment data covering
demand growth, consultation mode shifts, waiting time distribution,
and DNA rate trends.

**Key Findings:**
- 940M+ appointments analysed across 30 months (Jul 2023 – Dec 2025)
- Demand grew 11.4%, from 28.6M to 31.8M appointments per month
- Average DNA rate of 4.5%, stable but generating 1.43M missed appointments monthly
- PCN DNA rate (7.91%) is nearly double the GP rate (4.4%)
- Appointments booked 22+ days in advance averaged 10.6% of all bookings

**Findings & Insights:**
- Demand is growing faster than the registered patient base (11.4% vs 2.2%), 
  the system is under increasing pressure independent of population growth
- F2F appointments declining (68.2% → 61.8%) while video/online grew 472.5%, 
  a structural shift in how care is delivered
- Same-day appointments now account for 45.8% of all bookings, 
  suggesting increasing urgency-driven demand
- High-risk wait (22+ days) grew from 8.9% to 9.7%, 
  a small but growing pool of appointments vulnerable to no-show
- PCN DNA rate is consistently and structurally higher than GP, 
  not a temporary anomaly but a systemic difference requiring targeted intervention

**Charts produced:**
- Monthly appointment volume with trend line
- Appointments per working day
- Consultation mode breakdown (F2F, telephone, video)
- Waiting time distribution
- GP vs PCN DNA rate dumbbell chart

---

### Section 2 — Cost Impact Analysis
Estimates the financial burden of missed GP appointments using a £30 
unit cost per appointment (NHS England National Schedule of NHS Costs 
2022-23).

**Key Findings:**
- Total estimated DNA cost: £1.29 billion over 30 months
- PCN is 1.8x more expensive per 1,000 appointments than GP (£2,372 vs £1,319)
- High-risk wait appointments (22+ days) account for £139.7M (10.9%) of total DNA cost
- A 10% reduction in high-risk DNAs would recover ~£14M over the period

**Findings & Insights:**
- At an average of £42.9M per month, DNA cost is not a marginal inefficiency, 
  it is a structural drain on NHS resources at billion-pound scale
- PCN generates disproportionate waste despite being only ~3% of total volume, 
  scaling PCN services without addressing its DNA rate will amplify costs
- High-risk wait appointments contribute to DNA cost roughly in proportion to 
  their size (10.6% of appointments → 10.9% of cost), confirming they are a 
  targetable and addressable category
- Long booking lead times create an intervention window, reminders, 
  confirmation calls, or predictive flagging could recover meaningful cost
- Even a modest 10% reduction in preventable DNAs would save ~£5.6M annually

**Charts produced:**
- Monthly DNA cost bar chart with trend line
- Cumulative DNA cost line chart
- GP vs PCN cost per 1,000 appointments dumbbell chart
- Routine vs high-risk DNA cost stacked bar chart

---

### Section 3 — Predictive Modelling (InProgress)
Builds and compares classification models to predict individual 
Appointment no-show risk using the Kaggle Medical Appointment 
No-Show dataset (110,527 appointments).

**Models built:**
- Logistic Regression (baseline)
- Random Forest (improved model)

**Key Features:**
- Days between booking and appointment
- SMS reminder received
- Patient age
- Medical conditions (hypertension, diabetes, alcoholism)
- Gender, scholarship status

**Model Performance:**

| Model | Accuracy | No-show Recall | No-show F1 |
|---|---|---|---|
| Logistic Regression | 55.2% | 56% | 0.42 |
| Random Forest | 65.7% | 24% | 0.28 |

**Findings & Insights:**
- Age and waiting days are by far the strongest predictors of no-show,  
  accounting for 53.9% and 35.3% of feature importance respectively
- SMS reminders, despite being a widely used intervention, ranked 4th in 
  importance, suggesting reminders alone are insufficient for high-risk patients
- Logistic Regression achieves better no-show recall (56%) than Random Forest (24%) 
  despite lower overall accuracy, for the NHS use case, catching more no-shows 
  matters more than overall accuracy
- The model serves as a proof of concept, demonstrating that patient-level 
  features can predict no-show risk, and that a similar model deployed on NHS 
  data could help target interventions toward the £139.7M high-risk cost pool 
  identified in Section 2
- Key intervention trigger: patients with long booking lead times and no SMS 
  confirmation are the highest-risk profile for non-attendance

## Connecting the Datasets
The NHS GP dataset (Sections 1–2) operates at national aggregate level and 
establishes the scale and cost of the problem. The Kaggle dataset (Section 3) 
operates at individual appointment level and demonstrates that the problem is 
predictable. Together they form a complete analytical narrative, from 
identifying the problem, quantifying its cost, to building a tool that could 
prevent it.

---

## Datasets

| Dataset | Source | Rows | Description |
|---|---|---|---|
| GP DNA Monthly | NHS England | 30 rows | Aggregated monthly GP appointment data |
| No-Show Appointments | Kaggle | 110,527 rows | Individual patient appointment records |

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python 3 | Core language |
| pandas | Data manipulation |
| numpy | Numerical operations |
| matplotlib | Data visualisation |
| scikit-learn | Machine learning models |
| openpyxl | Excel file handling |

---

## How to Run

1. Clone the repository
```bash
git clone https://github.com/yourusername/nhs-gp-dna-analysis.git
cd nhs-gp-dna-analysis
```

2. Install dependencies
```bash
pip install -r requirements.txt
```

3. Add datasets to the `/data` folder

4. Run notebooks in order
```
section1_eda.ipynb → section2_cost_analysis.ipynb → section3_modelling.ipynb
```

---

## Requirements
```
pandas
numpy
matplotlib
scikit-learn
openpyxl
```

---

## Author
Built as a data analytics portfolio project demonstrating end-to-end 
analysis — from raw NHS data through cost modelling to predictive 
machine learning.

---

## Data Sources
- NHS England GP Appointment Publication — December 2025
- Kaggle Medical Appointment No-Show Dataset
  (Joniarroba, 2016) — https://www.kaggle.com/datasets/joniarroba/noshowappointments
- NHS England National Schedule of NHS Costs 2022-23 (£30 unit cost)
