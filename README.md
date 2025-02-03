# ChicagoCrimes

# **Chicago Crime Prediction using Machine Learning**
This project analyzes crime patterns in Chicago (2010-2022) and predicts the likelihood of an arrest based on crime characteristics. The dataset is sourced from the [Chicago Data Portal](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2) and processed using **Databricks on Google Cloud Platform (GCP)**. We implemented multiple machine learning models and optimized performance by deploying the models on **1 to 4 worker nodes**.

This is the databricks notebook link - https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/3623708202541795/487412892863449/2377989951854267/latest.html

## **Project Overview**
### **Objective**
- Predict whether an arrest will occur based on crime type, district, location, and other factors.
- Analyze crime trends across different locations and time periods.
- Optimize execution time and model performance by scaling worker nodes in **Databricks on GCP**.

### **Dataset Details**
- **Time Range:** 2010 - 2024
- **Records:** 4,636,386
- **Features:** 22 columns, including:
  - **Categorical Features:** Primary Type, Description, Location Description
  - **Numerical Features:** District, Hour of Day, Day of Week
  - **Boolean Features:** Domestic (True/False), Arrest (True/False)

## **Data Preprocessing**
### **1. Data Cleaning**
- Null values were imputed for missing **Latitude, Longitude, Ward, Community Area, District, and X Coordinate**.
- Missing **Location Description** values were replaced with “Other”.
- Removed duplicate records.

### **2. Feature Engineering**
- Extracted **time-related features**: Date, Month, Day of Week, Hour of Day.
- Created **"DayOrNight" classification** (Day: 6 AM - 6 PM, Night: 6 PM - 6 AM).

### **3. ETL Pipeline**
- Data was **extracted as CSV** and stored in **Amazon S3**.
- **Databricks on GCP** was used for running machine learning models on multiple worker nodes.

## **Exploratory Data Analysis**
- **22.3% of crimes resulted in an arrest** between 2010-2024.
- Most crimes occurred at **night** and in **specific districts**.
- Overall crime rates **declined** over the years.

## **Machine Learning Models**
### **1. XGBoost (Best Performing Model)**
- **Why XGBoost?** It efficiently handles large datasets with high accuracy.
- **Data Split:** 70% training, 30% testing.
- **Accuracy Results for sampled data:**
  - **2018-2024:** **89.79%**
  - **2014-2024:** 88.43%
  - **2010-2024:** 87.92%
- **Impact of Worker Nodes:** 
  - Increased worker nodes **reduced execution time** significantly.

### **2. Decision Tree Classifier**
- **Accuracy Results:**
  - **2018-2022:** **87.47%**
  - **2014-2022:** 85.12%
  - **2010-2022:** 84.37%
- **Observation:** More worker nodes led to **faster training time**.

### **3. Random Forest**
- **Accuracy Results:**
  - **2018-2022:** 85.98%
  - **2014-2022:** **86.14%**
  - **2010-2022:** 84.92%
- **Key Insight:** More robust than a single decision tree but slightly slower.

### **4. Naïve Bayes**
- **Accuracy Results:**
  - **2018-2022:** **88.90%**
  - **2014-2022:** 87.01%
  - **2010-2022:** 85.73%
- **Advantage:** Computationally efficient for large datasets.

## **Deployment on Google Cloud Platform (GCP)**
We deployed our **ML pipeline on Databricks (GCP)** and ran experiments using **1 to 4 worker nodes** to analyze performance:

| Worker Nodes | Execution Time | Model Accuracy (XGBoost) |
|-------------|----------------|--------------------------|
| 1 Node      | **Longest** (High latency) | **89.79%** |
| 2 Nodes     | Moderate Improvement | **89.79%** |
| 3 Nodes     | **Significant Improvement** | **89.79%** |
| 4 Nodes     | **Best Performance (Lowest Execution Time)** | **89.79%** |

### **Key Findings**
- **Execution time decreased as worker nodes increased.**
- **Accuracy remained consistent**, meaning additional worker nodes mainly improved processing efficiency.
- **Scaling beyond 4 nodes might not provide additional performance gains** but could be explored for larger datasets.

## **Performance Insights**
- **XGBoost had the best accuracy (~90%)** across different datasets.
- **More worker nodes led to reduced execution time.**
- **Increasing dataset size slightly reduced accuracy** due to class imbalance.

## **Technologies Used**
- **Databricks on GCP** (for ML pipeline and scaling experiments)
- **Amazon S3** (data storage)
- **Python (Pandas, NumPy, Scikit-Learn, XGBoost)**
- **Matplotlib & Seaborn** (for visualization)

## **Conclusion**
- **Scaling worker nodes significantly reduced execution time.**
- **XGBoost was the best model**, providing the highest accuracy.
- **Future improvements:** Explore **deep learning models** and **real-time crime prediction**.

