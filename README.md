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
│   └── section3_modelling.ipynb               # Predictive modelling
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
- Demand grew 11.4% — from 28.6M to 31.8M appointments per month
- Average DNA rate of 4.5% — stable but generating 1.43M missed appointments monthly
- PCN DNA rate (7.91%) is nearly double the GP rate (4.4%)
- Appointments booked 22+ days in advance averaged 10.6% of all bookings

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

**Charts produced:**
- Monthly DNA cost bar chart with trend line
- Cumulative DNA cost line chart
- GP vs PCN cost per 1,000 appointments dumbbell chart
- Routine vs high-risk DNA cost stacked bar chart

---

### Section 3 — Predictive Modelling
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
