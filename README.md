# Brazilian E-Commerce Machine Learning Capstone

## Overview
This repository contains the Machine Learning Capstone project predicting business outcomes for a Brazilian E-Commerce dataset (Olist). The project follows a strict machine learning pipeline including data auditing, preprocessing, feature engineering, exploratory data analysis (EDA), and machine learning model training.

## Folder Structure
- `data/` : Contains the raw dataset and the final `clean_orders.csv` after the shared preprocessing phase.
- `notebook/` : Contains the Jupyter Notebooks for analysis and model training.
- `model/` : Contains the final serialized `.pkl` file of the best tuned machine learning model.
- `visuals/` : Contains exported PNGs of key EDA and evaluation charts.
- `reports/` : Contains the final `model_comparison.csv` summarizing the performance of the 4 tested algorithms.

## Shared Phase (Completed)
1. **Data Audit:** Analyzed missing values, hidden nulls, and exact duplicates.
2. **Data Cleaning:** Standardized text, fixed data types, and enforced null handling rules.
3. **Feature Engineering:** Calculated net revenue, delivery delays, pricing gaps, and customer age groups.
4. **EDA:** Target distributions and correlation analysis.

## Individual Phase (Pending)
*Each team member will branch out to choose ONE of the following 5 models:*
1. Return Prediction (Classification)
2. Delivery Delay Prediction (Classification)
3. Customer Rating Prediction (Regression)
4. Customer Segmentation (Clustering)
5. Revenue Prediction (Regression)

## Instructions
To run this project, start with the Jupyter notebook located in the `notebook/` folder. Ensure all dependencies are installed before executing the cells.
