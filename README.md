<p align="center">
  <img src="https://raw.githubusercontent.com/coding-dojo-data-science/CodingDojo_Images/main/data-science.jpg">
</p>

# Optimize Outlet Sales by Understanding What Drives Product Revenue

## Analyzing Product and Outlet Characteristics to Predict Item-Level Sales

**Author:** Mohamed Shehada

---

## Business Problem

Retailers carry hundreds of products across multiple outlet types and locations, yet not all products perform equally. Without knowing which product and outlet factors drive sales, inventory decisions, pricing strategies, and outlet expansions are made blindly.

This project identifies the key drivers of item-level outlet sales and delivers a predictive model that allows the retailer to forecast expected revenue for any product-outlet combination — enabling smarter, data-driven business decisions.

---

## Data

**Source:** [Big Mart Sales Data — Kaggle](https://www.kaggle.com/datasets/brijbhushannanda1979/bigmart-sales-data)

The dataset contains sales records for 1,559 products across 10 outlets, including product-level features (weight, fat content, visibility, price, type) and outlet-level features (size, location tier, outlet type, establishment year).

- **Rows:** 8,523
- **Columns:** 12
- **Target variable:** `Item_Outlet_Sales` (sales in dollars)

---

## Methods

- Removed inconsistent labels in `Item_Fat_Content` (e.g. "LF" → "Low Fat") to ensure clean categorical encoding.
- Applied median imputation for `Item_Weight` to avoid bias from outliers.
- Applied constant imputation ("Missing") for `Outlet_Size` to retain rows while making absent information explicit.
- Used `OrdinalEncoder` for ordered features and `OneHotEncoder` for nominal features.
- Wrapped all preprocessing in a `Pipeline` to prevent data leakage.

---

## Results

### Item MRP Is the Strongest Sales Driver

<p align="center">
  <img src="explanatory4.png">
</p>

Among all features, `Item_MRP` (maximum retail price) shows the strongest correlation with sales at **0.57**. Higher-priced products consistently generate more outlet revenue, suggesting that premium pricing and placement decisions have a measurable impact on performance.

---

### Supermarket Type 1 Dominates Outlet Distribution

<p align="center">
  <img src="explanatory3.png">
</p>

`Supermarket Type1` is by far the most frequent outlet type in the dataset. Any inventory or sales strategy targeting this outlet type will have the broadest reach across the retailer's network.

---

## Model

A **Tuned Random Forest Regressor** was selected as the final model after comparing three approaches:

| Model | Train R² | Test R² | Test RMSE |
|---|---|---|---|
| Linear Regression | 0.562 | 0.567 | $1,092 |
| Default Random Forest | 0.938 | 0.558 | $1,104 |
| **Tuned Random Forest** | **0.643** | **0.606** | **$1,042** |

The tuned model explains **~61% of the variation in product sales** and predicts sales within an average error of **$1,042**. RMSE was chosen as the reporting metric because it is expressed in the same unit as sales (dollars), making it directly interpretable for business stakeholders.

The tuned model reduces the overfitting gap from **0.38** (default RF) down to just **0.037**, meaning it generalizes reliably to new, unseen products and outlets.

---

## Recommendations

- **Focus on high-MRP products:** Since item price is the strongest predictor, prioritizing premium product stocking — especially in high-traffic outlets — is likely to drive the most revenue growth.
- **Invest in Supermarket Type 1 outlets:** Given their dominance in the data, optimizing operations and inventory at Type 1 supermarkets will have the highest business impact.
- **Use the model for demand forecasting:** The tuned Random Forest can estimate expected sales for new product-outlet combinations before committing to inventory decisions.

---

## Limitations & Next Steps

- The model explains ~61% of sales variation — the remaining ~39% may be driven by factors not in the dataset (promotions, seasonality, competitor pricing).
- `Outlet_Size` had missing values that were imputed; better outlet-level data collection would improve accuracy.
- Next steps include testing Gradient Boosting or XGBoost and engineering new features such as outlet age from `Outlet_Establishment_Year`.

---

## For Further Information

For any additional questions, please contact: **eng.mdshehada@gmail.com
**
