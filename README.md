# Analysis of Promotions and Cannibalization between SKUs

## Project Description

This project focuses on analyzing promotions and identifying the effect of cannibalization between various SKUs. The main objective is to help managers make informed decisions by comparing forecasted sales volumes with historical data and analyzing the relationships between the sales of different SKUs.

## Notebooks

The analysis and results are documented in the following Jupyter notebooks:

1. [Exploratory Data Analysis](eda.ipynb): This notebook contains the analysis of data with plots
2. [Tasks Solutions](tasks_solving.ipynb): This notebook contains the analysis for detecting cannibalization effects between SKUs and similarity of promo

## Data Structure

The project uses three datasets:

1. **Daily_data**: Daily sales data.
   - `SKU`: Product identifier
   - `Warehouse_code`: Store identifier
   - `Date`: Date
   - `Sale_price`: Sale price
   - `Balance`: Stock balance
   - `Qnt_out_sale`: Quantity sold

2. **Products**: Product information.
   - `SKU`: Product identifier
   - `Net_weight`: Weight of the product
   - `Category_id`: Product category
   - `RSL`: Shelf life

3. **Promo**: Promotion information.
   - `Id`: Promotion identifier
   - `Begin_date`: Start date of the promotion
   - `End_date`: End date of the promotion
   - `Period_type_id`: Type of promotion

## Task 1: Finding Similar Promotions

### Description

The company has a system that automatically forecasts product demand during promotions. However, the manager reviews this information in an aggregated form at the "sku-begin_date-end_date" level for adequacy, adjusting or not changing the forecasted demand volumes. To make a decision, the manager wants to see promotions similar to those they are checking and compare the forecasted promotion volume with the aggregated actual sales data for these promotions.

### Solution

1. **Data Loading and Preprocessing**: Daily sales data, product data, and promotion data were loaded and merged.
2. **Data Aggregation**: Sales before, during, and after promotions were aggregated for each SKU.
3. **Similarity Calculation**: For each current promotion, the three most similar promotions from past data were found based on sales quantity, price, and stock balance.
4. **Output Results**: The top 3 most similar promotions for each current promotion were displayed, which can be used to verify the automatic forecasts.

### Answers to Questions

#### If not selecting the top-3 but a non-fixed number of "sku-promotions", based on what information would the decision on the number of options to provide to the user be made?

The decision on the number of options to provide to the user could be based on a similarity threshold rather than a fixed number. For example, instead of always selecting the top-3 similar promotions, the system could present all promotions that have a similarity score above a certain threshold. This approach ensures that only highly relevant promotions are shown, regardless of the exact number, thereby providing more tailored and accurate comparisons.

#### What other methods would you suggest for verifying the automatic forecasting system?

1. **Cross-Validation with Historical Data:** Regularly cross-validate the forecasted demand against actual sales data from past promotions to measure the accuracy of the forecasting model.
2. **Error Analysis:** Implement error metrics such as Mean Absolute Error (MAE), Mean Squared Error (MSE), and Mean Absolute Percentage Error (MAPE) to evaluate the performance of the forecasting system.
3. **A/B Testing:** Conduct A/B tests where one set of promotions uses the forecasted data and another set uses manually adjusted forecasts. Compare the results to understand the effectiveness of the automatic forecasts.
4. **Expert Review:** Periodically involve domain experts to review the forecasts and provide feedback, which can be used to improve the forecasting model.
5. **Anomaly Detection:** Implement anomaly detection techniques to identify and investigate unusual forecast patterns that may indicate model errors.

## Task 2: Analyzing Cannibalization between SKUs

### Description

The goal is to determine whether there is a cannibalization effect among the investigated categories between SKUs and in what cases it may occur. Additionally, it is necessary to propose features for investigating this effect and methods for assessing this effect.

### Solution

1. **Correlation Calculation:** Correlations between the sales of different SKUs within each category were calculated before, during, and after promotions. Significant negative correlations were used to identify the cannibalization effect.
2. **Regression Analysis:** Regression analysis was performed to assess the impact of one SKU's sales on another SKU's sales.
3. **Visualization:** Time series of sales for the top 3 pairs of SKUs with the cannibalization effect were visualized for a clearer analysis.

### Answers to Questions

#### Is there a cannibalization effect among the investigated categories between SKUs, and in what cases can it occur?

Yes, there is a cannibalization effect among the investigated categories between SKUs. Cannibalization can occur when products compete for the same customer segment or serve similar functions. For example, if two SKUs are substitutes or have overlapping features, an increase in sales of one SKU might lead to a decrease in sales of another SKU.

#### What features would you create and select to investigate such an effect?

1. **Average sales before, during, and after promotions**:
   - `avg_sales_before_promo`
   - `avg_sales_during_promo`
   - `avg_sales_after_promo`
2. **Price data**:
   - `price_before_promo`
   - `price_during_promo`
   - `price_after_promo`
3. **Promotion duration**:
   - `promo_duration`
4. **Product category**:
   - `category_id`
5. **Sales volumes by SKU**:
   - `sku_sales`
6. **Periodic sales data (e.g., monthly or weekly sales)**:
   - `monthly_sales`
   - `weekly_sales`

#### How can this effect be assessed if it is present?

1. **Correlation Analysis**:
   - Analyze correlations between the average sales of different SKUs before, during, and after promotions.
   - Use Spearman's rank correlation coefficient to identify significant relationships between categories.
2. **Regression Analysis**:
   - Build regression models to assess the impact of one SKU's sales on another SKU's sales.
   - Use linear regression to determine influence coefficients and significance.
3. **Cannibalization Ratio**:
   - Calculate the cannibalization ratio as the ratio of the decrease in sales in one category to the increase in sales in another category as a result of the promotion.
   - Example: If sales of SKU A decreased by 100 units and sales of SKU B increased by 200 units, the cannibalization ratio would be -0.5.

### Conclusion

**Task 1**: Identifying similar promotions helps managers make more informed decisions by comparing forecasts with historical data.

**Task 2**: Analyzing cannibalization between SKUs helps identify the negative impact of one SKU on another's sales, which can help optimize the product assortment and marketing strategies.