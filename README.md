![Project Banner](assets/banner.png)

# 🧬 Silicon Lottery AI Analyzer: Ryzen 7000 Series Optimization

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Library](https://img.shields.io/badge/Library-XGBoost%20%7C%20Pandas%20%7C%20Scikit--Learn-orange)
![Hardware](https://img.shields.io/badge/Hardware-AMD%20Ryzen%207000%20(Zen4)-red)
![Status](https://img.shields.io/badge/Status-Stable-green)

## 🚀 Overview

This project implements a **Machine Learning-driven approach** to optimize AMD Ryzen 7000 series (Zen 4) processors. By analyzing hardware telemetry logs using **XGBoost**, the system predicts thermal behavior, detects "Clock Stretching" anomalies, and calculates the optimal per-core Undervolting (Curve Optimizer) values.

The goal is to move beyond trial-and-error overclocking and use **Data Science** to find the absolute "Sweet Spot" between performance, thermals, and stability.

---

## 🎯 Key Features

* **Silicon Quality Assessment:** Automatically classifies cores as *Golden*, *Silver*, or *Bronze* based on voltage/frequency curves.
* **Thermal Simulation:** Predicts CPU temperature under various PPT (Power) limits using Gradient Boosting Regressors.
* **Clock Stretching Detection:** Compares *Effective Clock* vs. *Perf Clock* to identify voltage starvation and instability under load.
* **Automated Tuning Recipe:** Generates a precise BIOS configuration table (PBO, Curve Optimizer, PPT Limits) tailored to the specific silicon lottery of the chip.

---

## 🛠️ Methodology

### 1. Data Collection
Telemetry data is collected via **HWiNFO64** under various load scenarios (Prime95, Cinebench, Gaming, Idle).
* *Metrics:* Core VIDs, Effective Clocks, Power Draw (PPT), Temperatures, Fan RPM.

### 2. Machine Learning Model (XGBoost)
We train a regression model to understand the relationship between:
`Input: [PPT Limit, Curve Optimizer Offset, Fan Speed]`
`Output: [Expected Temperature, Expected Effective Clock]`

### 3. Optimization Logic
The script iterates through potential BIOS settings to maximize frequency while adhering to thermal constraints (e.g., <90°C) and voltage stability thresholds.

---

## 📊 Results (Example: Ryzen 5 7600X)

| Metric | Stock Settings | AI Optimized (Golden Tune) | Improvement |
| :--- | :--- | :--- | :--- |
| **Max Boost Clock** | 5.35 GHz | **5.55 GHz** | 🔺 +200 MHz |
| **Cinebench Temp** | 95.0°C (Throttled) | **86.0°C** | ❄️ -9°C |
| **Idle Stability** | Standard | **Enhanced (MCR/GDM Tuned)** | ✅ No Stutters |
| **Power Draw** | Uncapped (~110W) | **95W (Sweet Spot)** | 🔋 More Efficient |

---

## ⚙️ How to Use

1.  **Collect Data:** Log your CPU metrics using HWiNFO to a CSV file.
2.  **Install Requirements:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run Analysis:**
    Open `notebooks/03_Optimizer_and_Solver.ipynb` and load your CSV file.
4.  **Apply BIOS Settings:**
    Use the generated "Recipe" to configure PBO and Curve Optimizer in BIOS.

---

## ⚠️ Disclaimer
*Overclocking and Undervolting involve modifying hardware parameters that may void warranties or cause instability. This tool provides data-driven recommendations, but final application is at the user's risk.*

---

## 👨‍💻 Author
**Emrah Gökpınar** - *Data Science & Hardware Enthusiast*
