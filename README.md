# CLTV Prediction using BG-NBD and Gamma-Gamma Model

## Project Description

FLO aims to define a roadmap for its sales and marketing activities. To enable medium- and long-term strategic planning, the company needs to estimate the potential future value that existing customers will bring to the business. This project involves using BG-NBD and Gamma-Gamma models to predict Customer Lifetime Value (CLTV).

## Dataset Description

This dataset consists of past shopping behaviors of customers who made their last purchases in 2020-2021 as OmniChannel shoppers (both online and offline). The dataset includes the following variables:

### Variables:
- **master_id**: Unique customer ID.
- **order_channel**: Shopping channel (Android, iOS, Desktop, Mobile, Offline).
- **last_order_channel**: The channel used for the last purchase.
- **first_order_date**: Date of the customer's first purchase.
- **last_order_date**: Date of the customer's last purchase.
- **last_order_date_online**: Date of the last online purchase.
- **last_order_date_offline**: Date of the last offline purchase.
- **order_num_total_ever_online**: Total number of online purchases.
- **order_num_total_ever_offline**: Total number of offline purchases.
- **customer_value_total_ever_offline**: Total spending in offline purchases.
- **customer_value_total_ever_online**: Total spending in online purchases.
- **interested_in_categories_12**: List of categories the customer shopped in the last 12 months.

## Project Tasks

### Task 1: Data Preparation
1. Read the **flo_data_20K.csv** file and create a copy of the dataframe.
2. Define **outlier_thresholds** and **replace_with_thresholds** functions to handle outliers.
   - Since frequency values must be integers for CLTV calculations, round the upper and lower limits.
3. Detect and replace outliers in the following columns:
   - `order_num_total_ever_online`
   - `order_num_total_ever_offline`
   - `customer_value_total_ever_offline`
   - `customer_value_total_ever_online`
4. Create new variables for each customer's **total number of purchases** and **total spending** across both online and offline platforms.
5. Convert date-related columns to datetime format.

### Task 2: Building the CLTV Data Structure
1. Define the analysis date as **2 days after the last recorded purchase date**.
2. Create a new CLTV dataframe containing the following:
   - `customer_id`
   - `recency_cltv_weekly`: Recency in weeks (last purchase date - first purchase date)
   - `T_weekly`: Customer's tenure in weeks (analysis date - first purchase date)
   - `frequency`: Total number of purchases
   - `monetary_cltv_avg`: Average value per purchase

### Task 3: Modeling BG-NBD and Gamma-Gamma for CLTV Calculation
1. **Fit the BG/NBD model**:
   - Predict expected purchases for the next **3 months** (`exp_sales_3_month`).
   - Predict expected purchases for the next **6 months** (`exp_sales_6_month`).
2. **Fit the Gamma-Gamma model** to estimate the expected average value per transaction (`exp_average_value`).
3. Calculate **6-month CLTV** and store it in the dataframe (`cltv`).
   - Standardize CLTV values to create a new variable `scaled_cltv`.
   - Observe the top **20 customers** based on CLTV values.

### Task 4: Segmenting Customers Based on CLTV
1. Segment all customers into **4 groups** based on **6-month standardized CLTV** and assign segment names to the dataset (`cltv_segment`).
2. Select **two segments** and provide **6-month action recommendations** to management.

### Task 5: Function Implementation
- Convert the entire process into a reusable function to automate CLTV prediction.

## Conclusion
This project provides a systematic approach to predicting **Customer Lifetime Value (CLTV)** using BG-NBD and Gamma-Gamma models. By segmenting customers based on their future value, FLO can optimize its sales and marketing strategies, improving customer retention and maximizing revenue.

