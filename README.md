# Fertilizer Sales Report

### Interactive Dashboard:https://app.powerbi.com/groups/me/reports/af838d31-bc1e-42e9-b99d-de05cdd4ccef?ctid=df8679cd-a80e-45d8-99ac-c83ed7ff95a0&pbi_source=linkShare&bookmarkGuid=b827a80b-eaf5-42be-99a0-6cb365364293

### Description
The Fertilizer Sales Report provides a comprehensive overview of fertilizer sales across the United States. It offers valuable insights into sales trends, product performance, and regional distribution, enabling data-driven decisions to optimize sales strategies and improve business performance.

### Situation
The sales team faced challenges in tracking and analyzing fertilizer sales data across multiple regions. The unstructured data hindered the ability to:
- Monitor sales trends and identify growth opportunities.
- Analyze product performance and customer preferences.
- Optimize inventory management and distribution strategies.
- Make data-driven decisions to improve sales and marketing efforts.

### Task
As the data analyst for this project, my task was to consolidate and analyze fertilizer sales data across multiple regions. By creating an interactive Power BI dashboard, I aimed to:
- **Visualize sales trends and patterns**: Identify seasonal variations, growth trends, and potential sales opportunities.
- **Analyze product performance**: Determine the best-selling products and identify areas for product optimization.
- **Track sales by region**: Analyze regional performance and identify underperforming regions.
- **Support informed decision-making**: Provide actionable insights to optimize sales strategies, inventory management, and marketing efforts.

### Action

#### Data Cleaning and Preparation
- **Data Validation**: Checked for missing values, outliers, and inconsistencies in the data.
- **Data Cleaning**: Removed duplicates, corrected errors, and handled missing data appropriately.
- **Data Transformation**: Reshaped and restructured the data to align with the desired analysis, including categorizing products and standardizing units of measurement.

#### Data Modeling
- **Data Structure**: Designed a star schema data model to organize data efficiently, with a fact table containing sales data and dimension tables for product category, region, time period, and customer information.

#### Data Analysis and Visualization
- **Exploratory Data Analysis (EDA)**: Utilized EDA techniques to understand data distribution, identify trends, and uncover potential insights.
- **Time Series Analysis**: Analyzed sales trends over time to identify seasonal patterns, growth rates, and anomalies.
- **Product Performance Analysis**: Evaluated the sales performance of different product categories to identify best-sellers and underperforming products.
- **Geographical Analysis**: Analyzed sales performance by region to identify high-performing and low-performing areas.
- **Data Visualization**: Created interactive visualizations, such as line charts, bar charts, and maps, to communicate insights effectively.

## Main Dashboard
The main dashboard provides an in-depth view of sales behaviour, showcasing trends over time, product performance, and regional distribution by state.

![Screenshot_13-11-2024_232141_](https://github.com/user-attachments/assets/453aab2e-f9a9-4083-a9c4-deb425461740)

## Key Takeaways After Analysis

### Sales Trends
- **Seasonal Fluctuations**: The data reveals distinct seasonal patterns, with peak sales occurring in March and May, aligning with agricultural cycles.
- **Year-over-Year Comparison**: Comparative analysis provides insights into market trends, economic factors, and the impact of specific marketing or promotional strategies.

### Product Performance
- **Top-Selling Products**: Urea-based fertilizers, such as Granular Urea and Prilled Urea, dominate the market, indicating strong demand for nitrogen-based fertilizers.
- **Product Segmentation**: A deeper analysis of product-wise sales can identify opportunities for product diversification and targeted marketing campaigns.

### Regional Performance
- **Market Dominance**: California accounts for a significant portion of total sales, highlighting its importance as a key market.
- **Regional Variations**: Understanding regional sales patterns can help tailor marketing and distribution strategies to specific market needs.

### Pareto Analysis
The Pareto chart visually represents each product category's sales contribution and cumulative percentage.
- **Dominant Product Category**: Urea leads, contributing 21% of total sales.
- **Cumulative Sales**: By the time we reach Phosphorus, approximately 61% of total sales are accounted for. The top three categories (Urea, NPK, and Phosphorus) together contribute to over 80% of total sales.



# Cumulative Sales % DAX Measure for Pareto Analysis

This repository contains the DAX measure used for calculating **Cumulative Sales %** in Power BI for performing Pareto Analysis.

## DAX Measure

The DAX measure for **Cumulative Sales %** is as follows:

```DAX
Cumulative Sales % = 
VAR thisCategorySale = [Sales] 
VAR Sale_All_Categories =
    CALCULATE([Sales], ALL(Products[Product Category])) 
RETURN
    CALCULATE(
        [Sales],
        FILTER(ALL(Products[Product Category]), [Sales] >= thisCategorySale)
    ) / Sale_All_Categories ```

## Explanation of Each Part

1. **`VAR thisCategorySale = [Sales]`**:
   - This variable captures the sales value for the current product category in the row context.
   - For example, if we are looking at **Urea**, `thisCategorySale` will be **$5,709,815**.

2. **`VAR Sale_All_Categories = CALCULATE([Sales], ALL(Products[Product Category]))`**:
   - This variable calculates the total sales across all product categories, disregarding any filters.
   - It helps to normalize the cumulative sales percentage by dividing it by the total sales.
   - In our case, `Sale_All_Categories` will be the sum of sales for all categories:
     - **Total Sales** = $5,709,815 + $5,588,670 + $5,466,995 + $5,458,235 + $5,415,980 = **$27,639,695**.

3. **`RETURN CALCULATE([Sales], FILTER(ALL(Products[Product Category]), [Sales] >= thisCategorySale))`**:
   - This part of the measure calculates the cumulative sales. It does this by filtering the product categories to only include those with sales greater than or equal to `thisCategorySale`.
   - The key step here is the `FILTER(ALL(Products[Product Category]), [Sales] >= thisCategorySale)`, which allows us to perform a cumulative sum. The filter applies to all product categories, regardless of any existing filters or order. It includes categories that have equal or higher sales than the current one being calculated.

4. **`/ Sale_All_Categories`**:
   - Finally, the cumulative sales is divided by the total sales to get the cumulative percentage.

---

## Walkthrough with Example Data

Let’s apply this measure to the provided data for the product categories:

| **Product Category** | **Sales**     |
|----------------------|---------------|
| Urea                 | $5,709,815    |
| NPK                  | $5,588,670    |
| Phosphorus           | $5,466,995    |
| Nitrogen             | $5,458,235    |
| Potassium            | $5,415,980    |

### **Cumulative Sales % Calculation:**

1. **For Urea (Sales = $5,709,815)**:
   - **`thisCategorySale`** = $5,709,815 (sales for Urea)
   - **`Sale_All_Categories`** = $27,639,695 (total sales)
   - **Cumulative Sales**: Since Urea is the first category, its cumulative sales is just its own sales.
     - **Cumulative Sales** = $5,709,815
   - **Cumulative Sales %**: 
     \[
     \frac{5,709,815}{27,639,695} \approx 20.67\%
     \]

2. **For NPK (Sales = $5,588,670)**:
   - **`thisCategorySale`** = $5,588,670 (sales for NPK)
   - **Cumulative Sales**: Add the sales from **Urea** and **NPK**:
     - **Cumulative Sales** = $5,709,815 + $5,588,670 = $11,298,485
   - **Cumulative Sales %**:
     \[
     \frac{11,298,485}{27,639,695} \approx 40.88\%
     \]

3. **For Phosphorus (Sales = $5,466,995)**:
   - **`thisCategorySale`** = $5,466,995 (sales for Phosphorus)
   - **Cumulative Sales**: Add the sales from **Urea**, **NPK**, and **Phosphorus**:
     - **Cumulative Sales** = $5,709,815 + $5,588,670 + $5,466,995 = $16,765,480
   - **Cumulative Sales %**:
     \[
     \frac{16,765,480}{27,639,695} \approx 60.67\%
     \]

4. **For Nitrogen (Sales = $5,458,235)**:
   - **`thisCategorySale`** = $5,458,235 (sales for Nitrogen)
   - **Cumulative Sales**: Add the sales from **Urea**, **NPK**, **Phosphorus**, and **Nitrogen**:
     - **Cumulative Sales** = $5,709,815 + $5,588,670 + $5,466,995 + $5,458,235 = $22,223,715
   - **Cumulative Sales %**:
     \[
     \frac{22,223,715}{27,639,695} \approx 80.39\%
     \]

5. **For Potassium (Sales = $5,415,980)**:
   - **`thisCategorySale`** = $5,415,980 (sales for Potassium)
   - **Cumulative Sales**: Add the sales from all categories:
     - **Cumulative Sales** = $5,709,815 + $5,588,670 + $5,466,995 + $5,458,235 + $5,415,980 = $27,639,695
   - **Cumulative Sales %**:
     \[
     \frac{27,639,695}{27,639,695} = 100\%
     \]

---

## Final Results

| **Product Category** | **Sales**     | **Cumulative Sales** | **Cumulative Sales %** |
|----------------------|---------------|----------------------|------------------------|
| Urea                 | $5,709,815    | $5,709,815           | 20.67%                 |
| NPK                  | $5,588,670    | $11,298,485          | 40.88%                 |
| Phosphorus           | $5,466,995    | $16,765,480          | 60.67%                 |
| Nitrogen             | $5,458,235    | $22,223,715          | 80.39%                 |
| Potassium            | $5,415,980    | $27,639,695          | 100%                   |

---

### **Summary**:

- The **Cumulative Sales %** measure works by summing the sales of all product categories greater than or equal to the current category’s sales.
- As the DAX measure iterates through each category (in Power BI's visual context), it calculates the cumulative sum and then divides it by the total sales to produce the percentage.
- The results show that **Urea**, **NPK**, and **Phosphorus** contribute significantly to the total sales, and these are the categories you would likely focus on in a Pareto analysis for inventory, marketing, and sales strategy purposes.

## Implications for Business

1. **Focus on Key Products**: Prioritize production, distribution, and marketing strategies for the dominant product categories.
2. **Inventory Management**: Efficiently manage inventory for top-selling products to avoid stockouts and reduce carrying costs.
3. **Product Portfolio Analysis**: Evaluate the performance of less popular products for potential discontinuation or rebranding.
4. **Marketing and Sales Strategies**: Target marketing and sales efforts on the most profitable product categories.

---

## Recommendations

- **Optimize Product Mix**: Focus on promoting high-performing products and revising underperforming ones.
- **Enhance Marketing Strategies**: Implement targeted campaigns to increase brand awareness and customer acquisition.
- **Improve Inventory Management**: Optimize inventory to prevent stockouts and reduce excess inventory.
- **Strengthen Distribution Channels**: Enhance distribution efficiency and explore new markets.
- **Monitor Sales Trends**: Regularly monitor sales performance to refine strategies as needed.

