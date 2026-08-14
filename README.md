# Brazilian E-Commerce Delivery Delay Prediction

## Overview

This repository contains a complete Machine Learning project developed using the Brazilian E-Commerce (Olist) dataset. The objective of this project is to predict whether an order will be delivered late based on information available before delivery occurs.

Delivery delay prediction is a critical business problem in e-commerce logistics. Accurate predictions help companies proactively manage delivery risks, improve customer satisfaction, optimize resource allocation, and enhance courier performance monitoring.

The project follows an end-to-end machine learning workflow, including data auditing, preprocessing, feature engineering, exploratory data analysis (EDA), model development, evaluation, and business insight generation.

---

## Business Problem

Late deliveries directly impact customer experience and operational efficiency. Customers expect reliable delivery estimates, and businesses need visibility into potential delays before they happen.

This project builds a binary classification model capable of identifying high-risk deliveries in advance, allowing logistics teams to take preventive actions and improve overall service quality.

### Business Value

* Improve delivery reliability.
* Reduce customer complaints.
* Optimize logistics resource allocation.
* Monitor courier performance.
* Support data-driven operational decisions.
* Improve delivery expectation management.

---

## Project Objective

Predict whether an order will be delivered late.

### Target Definition

```python
is_late = 1 if actual_delivery_days > expected_delivery_days else 0
```

Where:

* **1** → Late Delivery
* **0** → On-Time Delivery

---

## Dataset

The project uses the Brazilian E-Commerce Public Dataset by Olist.

The dataset contains information about:

* Orders
* Customers
* Products
* Sellers
* Couriers
* Delivery performance
* Revenue
* Ratings
* Marketing channels

---

## Features Used

To prevent data leakage, only features available before delivery were used during training.

### Selected Features

* Courier
* Expected Delivery Days
* Weather Conditions
* Season
* Customer Area
* Product Category
* Order Month
* Order Hour

### Excluded Features

The following variables were intentionally excluded because they directly reveal delivery outcomes:

* Actual Delivery Days
* Delivery Status

---

## Machine Learning Pipeline

### Data Preparation

The shared preprocessing phase included:

* Missing value analysis
* Duplicate detection
* Data cleaning
* Data type correction
* Feature engineering
* Outlier inspection
* Exploratory Data Analysis (EDA)

### Class Imbalance Handling

The delivery delay target was highly imbalanced, with the majority of orders being delivered on time.

To address this challenge:

* Baseline performance was established using a Dummy Classifier.
* Class weighting strategies were evaluated.
* Multiple machine learning algorithms were compared.
* Model selection considered both predictive performance and business usefulness.

---

## Models Evaluated

The following classification models were trained and evaluated:

1. Dummy Classifier (Majority Class Baseline)
2. Logistic Regression
3. Decision Tree
4. Random Forest
5. K-Nearest Neighbors (KNN)
6. Support Vector Machine (RBF Kernel)
7. Neural Network (MLP Classifier)

---

## Evaluation Metrics

Models were evaluated using:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

Additional evaluation included:

* Confusion Matrix
* Feature Importance Analysis
* Courier Delay Analysis

---

## Model Performance Comparison

| Model               | Accuracy | Precision |     Recall |   F1 Score |    ROC-AUC | Tuned | Selected |
| ------------------- | -------: | --------: | ---------: | ---------: | ---------: | :---: | :------: |
| Dummy Classifier    |   0.9356 |    0.0000 |     0.0000 |     0.0000 |     0.5000 |   No  |    No    |
| Random Forest       |   0.9343 |    0.3320 |     0.0202 |     0.0381 | **0.7060** |  Yes  |   Yes    |
| Decision Tree       |   0.8932 |    0.1757 |     0.1786 |     0.1771 |     0.5605 |   No  |    No    |
| Logistic Regression |   0.6757 |    0.1093 | **0.5650** |     0.1832 |     0.6739 |   No  |    No    |
| KNN                 |   0.7281 |    0.0935 |     0.3709 |     0.1494 |     0.5854 |   No  |    No    |
| RBF SVC             |   0.7142 |    0.0713 |     0.2915 |     0.1123 |     0.5203 |   No  |    No    |
| Neural Network      |   0.7652 |    0.1242 |     0.4370 | **0.1934** |     0.6710 |   No  |    No    |

---

## Model Selection

### Selected Model: Random Forest

Although several models achieved higher Recall and F1 scores, the Random Forest model achieved the highest ROC-AUC score (**0.706**), indicating the strongest ability to distinguish between delayed and on-time deliveries across classification thresholds.

Hyperparameter tuning further improved its predictive capability, making it the most reliable model for ranking delivery risk.

For this reason, Random Forest was selected as the final production model and saved as:

```text
model/rf_best_pipeline.pkl
```

---

## Confusion Matrix Analysis

### Random Forest Results

|                | Predicted On-Time | Predicted Late |
| -------------- | ----------------: | -------------: |
| Actual On-Time |            25,428 |             14 |
| Actual Late    |             1,782 |             55 |

### Interpretation

* Correctly identified 25,428 on-time deliveries.
* Correctly detected 55 delayed deliveries.
* Generated very few false alarms.
* Missed a substantial number of delayed deliveries due to severe class imbalance.

This behavior explains the model's high accuracy but relatively low recall.

---

## Feature Importance

Feature importance analysis was performed using the final Random Forest model.

The visualization is available in:

```text
visuals/03.Top_15_Feature_Importances.png
```

The most influential predictors were derived from delivery expectations, seasonal patterns, customer location characteristics, and courier-related information.

---

## Business Insights

### 1. Delivery Delay Is a Highly Imbalanced Problem

The Dummy Classifier achieved 93.56% accuracy while completely failing to identify delayed orders.

This demonstrates that accuracy alone is misleading and that additional metrics such as Recall, F1 Score, and ROC-AUC are necessary for model evaluation.

### 2. Courier Performance Significantly Impacts Delivery Outcomes

Courier-level analysis revealed noticeable differences in delivery performance, indicating that carrier selection is an important operational factor influencing delays.

### 3. Geographic Areas Exhibit Different Delay Risks

Certain delivery regions consistently showed higher delay frequencies, suggesting that infrastructure, distance, or operational constraints contribute to delivery performance.

### 4. Seasonal Effects Influence Delivery Reliability

Periods with elevated order volume exhibited increased delay rates, highlighting the impact of demand surges on logistics operations.

### 5. Delivery Expectations Are Strong Predictors

Expected delivery duration emerged as one of the strongest indicators of eventual delivery performance, making it a valuable feature for proactive risk monitoring.

---

## Visualizations

The project includes the following visual analyses:

### Model Evaluation

* Confusion Matrix
* ROC Curve
* Top 15 Feature Importances

### Business Analytics

* Net Revenue Analysis
* Top Areas by Revenue
* Average Quantity by Discount
* Average Net Revenue by Discount
* Marketing Source Performance
* Courier Performance
* Top vs Bottom Performing Segments
* Customer Rating Distribution
* Delivery Delay vs Rating
* Total Net Revenue by Age Group
* Orders Over Time
* Correlation Heatmap
* Net Revenue by State

---

## Repository Structure

```text
.
├── data
│   ├── clean_orders.csv
│   └── raw_orders.csv
│
├── model
│   ├── .gitkeep
│   └── rf_best_pipeline.pkl
│
├── notebook
│   ├── brazilian_ecom_preprocessing.ipynb
│   └── Capstone_Model2_Analysis.ipynb
│
├── reports
│   ├── .gitkeep
│   └── model_comparison.csv
│
├── visuals
│   ├── 01.Confusion_Matrix.png
│   ├── 02.ROC_Curve.png
│   ├── 03.Top_15_Feature_Importances.png
│   ├── 04.Net_revenue.png
│   ├── 05.Top10_Areas_Revenue.png
│   ├── 06.Average_Quantity_By_Discount.png
│   ├── 07.Average_net_revenue_discount.png
│   ├── 08.Marketing_sources_performance.png
│   ├── 09.Courier_Performance.png
│   ├── 10.Top5_Vs_Bottom5.png
│   ├── 11.Rating_Dist.png
│   ├── 12.Delivery_Delay_Vs_Rating.png
│   ├── 13_TTL_Net_Revenue_Age.png
│   ├── 14.Orders_Over_Time.png
│   ├── 15.Correlation_Heatmap.png
│   └── 16_Net_Rev_State.png
│
├── AI_Project.pdf
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-Learn
* Matplotlib
* Seaborn
* Jupyter Notebook

---

## Future Improvements

* Apply SMOTE and advanced resampling techniques.
* Experiment with XGBoost, LightGBM, and CatBoost.
* Optimize classification thresholds for business objectives.
* Deploy the model through a REST API.
* Implement automated model monitoring and retraining.

---

## Conclusion

This project successfully developed a machine learning pipeline for predicting delivery delays in Brazilian e-commerce operations. After comparing multiple classification algorithms, a tuned Random Forest model was selected as the final solution due to its superior ROC-AUC performance and ability to distinguish delayed orders from on-time deliveries.

The resulting insights can help logistics teams proactively manage delivery risks, improve courier selection strategies, and enhance customer satisfaction through more reliable delivery planning.
