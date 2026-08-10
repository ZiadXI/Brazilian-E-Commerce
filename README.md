# E-Commerce Machine Learning Capstone

This repository contains the code and models for our E-Commerce Machine Learning Capstone project.

## The Shared Phase (Team Foundation)
Before splitting into individual models, the team must complete the **Shared Phase**. This ensures everyone is working from the same high-quality, preprocessed dataset (`clean_orders.csv`).

### Step 1: Load & Preserve
* **Goal:** Import the data safely.
* **Tasks:** 
  * Read `raw_orders.csv` from the `data/` folder.
  * Preserve a raw copy of the dataframe.
  * Check `.shape`, `.head()`, and `.tail()`.
  * Set a global random seed for reproducibility.

### Step 2: Data Audit
* **Goal:** Understand data quality issues.
* **Tasks:**
  * Run `.info()` and `.describe()` for all columns.
  * Calculate missing value counts and percentages.
  * Check for exact row duplicates and duplicate `Order_ID`s.
  * Identify hidden nulls (e.g., `'NA'`, `'N/A'`, `'Null'`, `'-'`, or blanks).

### Step 3: Data Preprocessing (Cleaning & Encoding)
* **Goal:** Fix the issues identified in the audit.
* **Tasks:**
  * Clean column names to `snake_case`.
  * Fix data types (convert dates to `datetime`, numerics to `numeric`, categoricals to `category`).
  * Standardize text labels (e.g., unify casing, merge `Online/online` -> `Online`).
  * Standardize binary/category labels (Yes/No, gender, branch).
  * Validate business rules (prices > 0, qty > 0, discount scale 0-100 vs 0-1).
  * **Important Null Rules:**
    * Return fields (Returned=No) -> keep null (not an error).
    * Rating null -> keep null (no review).
    * Campaign null -> fill with `'No Campaign'`.

### Step 4: Feature Engineering
* **Goal:** Create derived features to improve model performance.
* **Tasks:**
  * **Revenue:** Calculate `gross_revenue`, `discount_amount`, and `net_revenue`.
  * **Delivery:** Calculate `delivery_delay` and binary `is_late`.
  * **Pricing:** Calculate `price_gap` against competitors and binary `is_pricier`.
  * **Time:** Extract `order_month`, `order_weekday`, `order_hour`, and binary `is_weekend`.
  * **Customer:** Bin ages into `age_group` (U18, 18-25, 26-35, 36-45, 46-55, 55+).
  * **Stock:** Create `low_stock_flag`.

### Step 5: Shared EDA (Exploratory Data Analysis)
* **Goal:** Understand overall business trends before modeling.
* **Tasks:**
  * Check unique values and numeric quartiles.
  * Plot Correlation heatmap for numeric features.
  * Plot Orders over time (line chart).
  * Plot Revenue by category, channel, and area.

### 💾 Export
Once Step 5 is complete, the team will export this unified dataframe as **`data/clean_orders.csv`**. 

Every team member will then load `clean_orders.csv` into their individual Jupyter Notebooks to begin their unique model (Steps 6-10: Target Definition, Split, Encode, Train, Tune, Evaluate).
