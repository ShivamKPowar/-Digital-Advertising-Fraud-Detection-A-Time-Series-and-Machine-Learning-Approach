# 🚨 **Digital Advertising Fraud Detection — A Time-Series & Machine Learning Approach**

---

## 🔍 **Introduction**
This assignment project presents an **end-to-end data analysis and machine learning solution** for detecting **Invalid Traffic (IVT)**, commonly known as **mobile ad fraud**.

The analysis focuses on **six mobile applications** —  
✅ **3 apps with consistently valid traffic**  
⚠️ **3 apps flagged as fraudulent (IVT) at different time points**

Using **time-series ad traffic logs** and **derived fraud-detection ratios**, we explore the **behavioral signature of fraudulent apps**.

A **Decision Tree Classifier** and **XGBoost model** are used to:
- Detect IVT
- Identify key fraud metrics and thresholds
- Explain **_why_** some apps were flagged earlier vs later

---

## 🏢 **Business Problem**
The real-world challenge is **not just detecting fraud**, but answering:

> 🔎 **What traffic pattern indicates fraud?**  
> ⏱️ **When does a valid app suddenly become fraudulent?** (the **“Sudden Attack Pattern”**)  
> 📊 **Which exact traffic signals trigger IVT classification?**

---

## 🎯 **Objective**
The primary goals of the analysis are:

1️⃣ **Feature Identification**  
   Find which traffic metrics and ratios best separate IVT from non-IVT.

2️⃣ **Change-Point Detection**  
   Identify the **exact hour/day an app first turns fraudulent**.

3️⃣ **Model Interpretability**  
   Build an **explainable ML model** (Decision Tree/XGBoost) showing **which thresholds → IVT flag**.

---

## 📂 **Dataset**
The dataset contains **hourly & daily aggregated ad traffic logs** for **six apps** over a **5-day period**.

| Column | Description |
|--------|-------------|
| **Date Or Hour** | Timestamp for aggregation |
| **unique_idfas** | Count of unique device IDs |
| **unique_ips** | IP count |
| **unique_uas** | User-Agent string count |
| **total_requests** | Total ad requests |
| **requests_per_idfa** | `total_requests / unique_idfas` |
| **impressions** | Total served ads |
| **impressions_per_idfa** | `impressions / unique_idfas` |
| **idfa_ip_ratio** | `unique_idfas / unique_ips` |
| **idfa_ua_ratio** | `unique_idfas / unique_uas` |
| **IVT** | Label: 0 ✅ valid / 1 ❌ invalid |

---

## 📊 **Exploratory Data Analysis (EDA)**

### 1️⃣ Feature Distribution Comparison
📌 **Fraud shows abnormal ratio spikes**

![Feature Distribution](http://github.com/ShivamKPowar/-Digital-Advertising-Fraud-Detection-A-Time-Series-and-Machine-Learning-Approach/blob/main/Feature%20Distribution%20Comparison.png)

**Key Signals of IVT:**
- **idfa_ua_ratio** → too many devices share same UA → **device spoofing**
- **requests_per_idfa** → abnormally high requests per device → **bot automation**
- **idfa_ip_ratio** → many devices behind same IP → **proxy/datacenter traffic**

---

### 2️⃣ Temporal Pattern — “IVT Emergence”
![Temporal Analysis](https://github.com/ShivamKPowar/-Digital-Advertising-Fraud-Detection-A-Time-Series-and-Machine-Learning-Approach/blob/main/Temporal%20Analysis%20by%20App.png)

**Patterns Observed:**
| Pattern | Behavior |
|---------|----------|
| ✅ **Valid Apps** | Metrics stay stable & organic |
| ⚠️ **IVT Early Apps** | Start fraudulent from hour 1 |
| 💣 **IVT Later Apps** | Clean at first → sudden spike attack |

---

## 🌳 **Decision Tree Model**
![Decision Tree](https://github.com/ShivamKPowar/-Digital-Advertising-Fraud-Detection-A-Time-Series-and-Machine-Learning-Approach/blob/main/Decision%20Tree.png)

### ✅ **Conclusions**
✔️ **Top features driving IVT detection:**
- **unique_uas** → UA diversity
- **requests_per_idfa** → bot burst rate
- **idfa_ip_ratio** → proxy traffic pattern

✔️ **Performance**
- **Accuracy:** 0.95
- **IVT Recall:** 0.92 (low false negatives)
- **IVT Precision:** 0.99 (almost no false positives)

---

## ⚡ XGBoost Model
![XGBoost](https://github.com/ShivamKPowar/-Digital-Advertising-Fraud-Detection-A-Time-Series-and-Machine-Learning-Approach/blob/main/XGBoost%20Tree.png)

### 🔥 Feature Importance (IVT Signature)
| Rank | Feature | Importance |
|-------|----------|------------|
| 🥇 **unique_uas** | 0.56 |
| 🥈 **requests_per_idfa** | 0.17 |
| 🥉 **idfa_ua_ratio** | Significant |
| 4️⃣ **idfa_ip_ratio** | Key anomaly indicator |

📌 **Raw metrics like impressions have near-zero importance** → ratios are the real fraud indicators.

### 📈 Model Performance
- **Accuracy:** 0.95
- **Precision (IVT):** 0.96 ✅
- **Recall (IVT):** 0.93 ✅
- **F1 Score:** 0.95 ✔️ stable across both classes

---

## 🧠 **Conclusion & Insights**
✅ IVT can be **detected reliably using derived ratios**  
✅ Fraudulent apps trigger **sharp spikes before being flagged**  
✅ XGBoost + Decision Tree provide **both accuracy & interpretability**

⚠️ **Apps marked IVT earlier had high fraudulent ratios from the start**  
⏳ **Apps marked later showed a sudden attack (change-point event)**

---

## 🛠️ **Tech Stack**
| Category | Tools |
|----------|-------|
| Data & EDA | **Python, pandas, numpy, seaborn, matplotlib** |
| ML Models | **scikit-learn (DecisionTreeClassifier), XGBoost** |
| Notebook | **Jupyter** |
| Visualization | **Decision Tree Plot, Feature Importance Plot** |
| Version Control | **GitHub** |

---

---

💡 *Feel free to ⭐ the repo if you find it useful!*
