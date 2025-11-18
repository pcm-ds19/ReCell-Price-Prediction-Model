# ReCell Price Prediction – Predictive Modeling Project

Predicting used device prices for a refurbished smartphone and tablet startup using Linear Regression and detailed exploratory data analysis.

---

## 1. Project Overview

This project builds a Linear Regression model to predict the normalized used price of phones and tablets in the refurbished device market.

The work was done as part of the Predictive Modeling module in the PGP-DSBA program (Great Lakes Institute of Management & Texas McCombs). The goal is to help a startup, ReCell, design a data-driven dynamic pricing strategy for used and refurbished devices.

The analysis covers:
- Exploratory Data Analysis (EDA)
- Data preprocessing and feature engineering
- Linear Regression model building
- Assumption checks for Linear Regression
- Model performance evaluation
- Actionable business recommendations for pricing and positioning

All details are documented in the accompanying business report PDF and notebook.

---

## 2. Business Problem

The used and refurbished mobile device market is growing rapidly, with customers looking for affordable yet reliable alternatives to new phones and tablets. ReCell wants to:

1. Predict the normalized used price of each device.
2. Understand which features significantly influence resale value.
3. Use these insights to set competitive, profitable, and transparent prices.

Business questions addressed include:
- How do device specifications (RAM, camera, screen size, battery) impact used prices?
- How much does the original (new) price influence the resale price?
- How do age and usage days affect value depreciation?
- Which features should ReCell highlight in marketing and pricing strategies? :contentReference[oaicite:0]{index=0}

---

## 3. Dataset

The dataset contains information on used/refurbished phones and tablets collected in 2021.

- Rows: 3,454 devices  
- Original columns: 15  
- Post-encoding columns: 50 (after one-hot encoding categorical features) :contentReference[oaicite:1]{index=1}  

**Key variables:**
- `brand_name` – Device brand (Apple, Samsung, Xiaomi, etc.)
- `os` – Operating system (Android, iOS, Others)
- `screen_size` – Screen size in inches
- `4g`, `5g` – Network capability flags
- `main_camera_mp`, `selfie_camera_mp` – Camera resolutions
- `int_memory`, `ram` – Storage and RAM in GB
- `battery` – Battery capacity in mAh
- `weight` – Weight in grams
- `release_year` – Year model was released
- `days_used` – Number of days the device has been used
- `normalized_new_price` – Normalized price of the new device (euros)
- `normalized_used_price` – Normalized price of the used device (target variable) :contentReference[oaicite:2]{index=2}  

---

## 4. Approach

### 4.1 Exploratory Data Analysis (EDA)

EDA was performed to understand distributions, relationships, and key drivers of price.

Examples of analyses:
- Distribution of `normalized_used_price` (right-skewed; most devices are in lower price ranges).
- Market share by operating system (Android dominates, followed by iOS).
- Variation of RAM, battery, screen size, and camera resolutions across brands.
- Relationship between price and:
  - Days used
  - Brand
  - Screen size
  - RAM and internal memory
  - New device price
  - Battery and weight :contentReference[oaicite:3]{index=3}  

### 4.2 Data Preprocessing

Steps:
- Duplicate check: No duplicate rows found.
- Missing values:
  - Present in camera, memory, battery, and weight columns.
  - Treated using median imputation for numeric features.
- Outlier handling:
  - Outliers detected using IQR for numeric columns.
  - Extreme values capped to reasonable bounds where appropriate.
- Feature engineering:
  - `device_age = 2021 - release_year` created to capture age directly.
- Encoding:
  - Categorical variables (`brand_name`, `os`, `4g`, `5g`) converted using one-hot encoding.
  - One level dropped from each to avoid dummy variable trap/multicollinearity. :contentReference[oaicite:4]{index=4}  

### 4.3 Model Building – Linear Regression

- Target: `normalized_used_price`
- Technique: Ordinary Least Squares (OLS) Linear Regression
- Train–test split: 80% train, 20% test
- Implementation:
  - Model trained on preprocessed and encoded features.
  - Coefficients interpreted to understand feature impact on used price. :contentReference[oaicite:5]{index=5}  

### 4.4 Assumption Checks

To validate the Linear Regression model, the following assumptions were checked:

- Normality of residuals:
  - Tested using Shapiro–Wilk.
  - Residuals deviate from perfect normality but are acceptable for practical use.
- Homoscedasticity:
  - Residuals vs predicted plot shows mild heteroscedasticity.
- Multicollinearity:
  - VIF analysis revealed high multicollinearity between `release_year`, `device_age`, and some brand dummies.
- Linearity:
  - Strong linear relationships observed for key predictors such as screen size, cameras, RAM, and `normalized_new_price`. :contentReference[oaicite:6]{index=6}  

---

## 5. Model Performance

The Linear Regression model achieved the following performance:

- Train R²: 0.847  
- Test R²: 0.836  
- MAE (Mean Absolute Error): 0.1844  
- MSE (Mean Squared Error): 0.0533  
- RMSE (Root Mean Squared Error): 0.2309 :contentReference[oaicite:7]{index=7}  

Interpretation:
- The model explains about 84% of the variance in the normalized used price.
- Errors are relatively small compared to the normalized price range, indicating good predictive performance on unseen data.

---

## 6. Key Drivers and Insights

Important features impacting used device prices:

- `normalized_new_price`  
  Strongest positive driver. Higher original price leads to higher used price.

- `device_age`  
  Negative impact. Older devices lose value more quickly.

- `screen_size`  
  Larger screens are associated with higher prices, up to a point.

- `main_camera_mp` and `selfie_camera_mp`  
  Higher megapixels increase price; rear camera has slightly more influence than selfie camera.

- `ram` and `int_memory`  
  Devices with more RAM and internal memory command higher prices.

- Battery capacity and weight  
  Larger batteries tend to increase weight; battery capacity shows a small negative relationship with normalized price, possibly reflecting trade-offs in design or market segment.

Business implications:
- Premium, recent devices retain more value and can be positioned as “high value retention” models.
- Specifications like RAM, storage, cameras, and screen size should be central to pricing and marketing.
- Age and days used are crucial for dynamic discounting strategies.

---

## 7. Business Recommendations

From the analysis and model results, the following recommendations are made for ReCell:

1. Dynamic pricing:
   - Use the model to set baseline prices based on key features and age.
   - Apply dynamic adjustments for brand, condition, and market demand.

2. Feature-based positioning:
   - Highlight RAM, storage, large screens, and camera quality in product listings.
   - Position 5G-enabled and recent models as “future-ready” and price them accordingly.

3. Segmentation:
   - Entertainment segment: Large screen, high storage, good battery.
   - Performance segment: High RAM, fast processors, 5G support.
   - Budget segment: Balanced specifications with strong value for money.

4. Inventory and marketing:
   - Discount older, low-spec models more aggressively to reduce inventory.
   - Promote high-spec devices with clear value messages around performance and longevity. :contentReference[oaicite:8]{index=8}  

---






