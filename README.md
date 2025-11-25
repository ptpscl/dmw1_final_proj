# Multivariate Process Monitoring Project

This repository contains a sequence of Jupyter notebooks that document the development of a multivariate statistical process monitoring (MSPM) system, likely applied to a complex industrial dataset such as the Tennessee Eastman Process (TEP). The project follows a standard data science and quality control workflow, moving from initial data understanding to the implementation and evaluation of advanced modeling techniques.

## Project Structure

The project is divided into three distinct phases, each represented by a notebook:

### 1. `0EDA.ipynb` (Exploratory Data Analysis)

This notebook is dedicated to the initial understanding and preparation of the raw process data.

* **Purpose:** To explore the structure, quality, and statistical properties of the multivariate time-series data. This phase is crucial for establishing the "normal" operating condition baseline.
* **Key Activities:**
    * Loading and initial inspection of the dataset (e.g., checking data types, missing values).
    * Statistical summarization of variables (mean, variance, distribution).
    * Time-series visualization of key process variables and manipulated variables to identify trends, cycles, and regime shifts.
    * Analysis of temporal properties, such as **autocorrelation** and **stationarity**, which determine the need for dynamic modeling methods.
    * Separating the data into **Normal Operation** (for model training) and **Faulty** conditions (for testing).

---

### 2. `01CONTROL_CHARTS.ipynb` (Multivariate Control Charts)

This notebook implements the foundational MSPM technique: **Principal Component Analysis (PCA)**, and uses it to construct control charts for fault detection.

* **Purpose:** To train a static PCA model on the normal data, establish control limits, and evaluate its performance in detecting various fault types.
* **Key Activities:**
    * **Data Standardization:** Applying scaling to ensure all variables contribute equally to the PCA model.
    * **PCA Model Training:** Determining the optimal number of principal components (PCs) to retain the maximum amount of "normal" variation (the signal) while isolating the noise.
    * **Control Limit Calculation:** Calculating the **Hotelling's $T^2$** and **Squared Prediction Error (SPE or $Q$)** statistics and setting control limits (usually at 95% or 99% confidence). 
    * **Fault Detection Evaluation:** Applying the model to the faulty datasets to measure metrics like **Detection Rate (DR)** and **False Alarm Rate (FAR)**, particularly focusing on the use of the Q statistic for fault detection.

---

### 3. `02MODELING.ipynb` (Dynamic and Advanced Modeling)

This notebook advances the process monitoring framework by incorporating dynamic and more sophisticated techniques to improve fault detection, diagnosis, and prognosis.

* **Purpose:** To capture the time-dependent nature (process memory) of the industrial system, which static PCA often misses, and to apply state-of-the-art methods for better performance on difficult faults.
* **Key Activities:**
    * **Dynamic Data Embedding (Takens-PCA):** Applying time-lagged data structures (e.g., Takens embedding) to turn static models into dynamic ones.
    * **Implementation of Dynamic Models:** Training and evaluating models such as:
        * **Dynamic PCA (DPCA)** or **Enhanced PCA (ENH-PCA)**.
        * **Canonical Variate Analysis (CVA)** or **Canonical Variate Dynamic Analysis (CVDA)**.
    * **Prognosis and Diagnosis:** Utilizing contribution plots and advanced statistics (like the **D-index** in CVDA) to not only detect a fault but also to **diagnose** which variables are the primary cause and to perform **prognosis** by tracking the fault's state trajectory.

    * **Performance Comparison:** Summarizing the detection rates and time-to-detection across all static and dynamic methods for various fault scenarios (e.g., comparing PCA vs. DPCA vs. CVA performance).
