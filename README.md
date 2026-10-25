# Power BI: Data Transformation, Modeling, DAX & Data Visualization for the E Commerce Sales Dataset

## Executive Summary
This project represents an end-to-end e-commerce data analytics solution built using **Power BI Desktop**, **Power Query Editor**, and **DAX (Data Analysis Expressions)**. It encompasses data import, multi-table transformation, relational star-schema modeling, advanced calculated columns, time-intelligence measures, and an interactive executive dashboard layout.

---

## 1. Architecture & Data Modeling
- **Datasets Integrated:** `List of Orders`, `Order Details`, and `Sales Target` [cite: 3].
- **Star Schema Design:** 
  - Established a active One-to-Many (`1:*`) relationship between `List of Orders` and `Order Details` using `Order ID` [cite: 18].
  - Implemented a clean **Category Lookup Dimension (`Category_Dim`)** to bridge `Order Details` and `Sales Target`, successfully resolving Many-to-Many relational conflicts on `Category` [cite: 18].

---

## 2. Power Query Data Transformation & Cleaning
- **Row Limiting & Types:** Restricted `List of Orders` to the first 500 rows; formatted `Order Date` to Date, and financial fields (`Amount`, `Target`) to Fixed Decimal Numbers [cite: 17].
- **Text Formatting:** Standardized `CustomerName` to Proper Case [cite: 17].
- **Custom & Conditional Columns:**
  - `Location`: Merged `City` and `State` (`City, State`) [cite: 17].
  - `Profit Margin`: Calculated as `Profit / Amount` (expressed as a percentage) [cite: 17].
  - `Profit Status`: Conditional evaluation (`Profit < 0` $
ightarrow$ Loss; `Profit = 0` $
ightarrow$ Break-Even; `Profit > 0` $
ightarrow$ Profit) [cite: 17].
- **Data Quality:** Conducted thorough missing value imputation and removed duplicate transaction records based on unique keys [cite: 17].

---

## 3. DAX Calculations & Business Logic

### **Calculated Columns (`Order Details` Table)**
1. **Category Type:**
   ```dax
   Category Type = 'Order Details'[Category] & " - " & 'Order Details'[Sub-Category]
   ```
2. **Revenue per Order:**
   ```dax
   Revenue per Order = 'Order Details'[Amount] * 'Order Details'[Quantity]
   ```
3. **Sales Category:**
   ```dax
   Sales Category = IF('Order Details'[Amount] > CALCULATE(AVERAGE('Order Details'[Amount]), ALL('Order Details')), "Above Average", "Below Average")
   ```

### **DAX Measures**
1. **Order Count:**
   ```dax
   Order Count = COUNT('Order Details'[Order ID])
   ```
2. **Average Profit in Delhi:**
   ```dax
   Average Profit in Delhi = CALCULATE(AVERAGE('Order Details'[Profit]), 'List of Orders'[State] = "Delhi")
   ```
3. **Year-to-Date (YTD) Sales:**
   ```dax
   YTD Sales = TOTALYTD(SUM('Order Details'[Amount]), 'List of Orders'[Order Date])
   ```

---

## 4. Interactive Visualizations & Dashboard Layout (`E-Commerce Sales Analysis`)

1. **Executive KPI Cards:** Displaying `Order Count` (2K), `Average Profit in Delhi` (40.36), `YTD Sales` (₹158.8K), `Total Sales` (₹2.14687M), and `Sales Target` (436K) for quick performance tracking [cite: 23].
2. **Sales Target Achievement by Category:** Clustered column chart comparing actual revenue against monthly targets across categories [cite: 23].
3. **Max Profit Margin by Sub-Category:** Donut chart analyzing maximum profit margins per sub-category [cite: 23].
4. **Monthly Sales Trend:** Line chart visualizing revenue trajectory across months [cite: 23].
5. **Comparison of Profit and Quantity by Sub-Category:** Scatter plot illustrating operational correlation [cite: 23].
6. **Minimum Target Multi-Row Card:** Displays minimum targets segmented by category [cite: 23].
7. **Sales Performance Matrix:** Comprehensive cross-tabulation comparing actual sales to targets across categories and months [cite: 24].
8. **Geographic Sales Analysis:** Map visualization tracking revenue distribution across cities [cite: 24].
9. **Sales Distribution by Sub-Category:** Treemap representing sub-category performance proportions [cite: 24].
10. **Order Count Analysis by State:** Funnel chart highlighting regional order volume distribution [cite: 24].
