# Business Intelligence and Visualization Practical Exam

## 1. Brief Description of Approach
This Power BI project focused on transforming and visualizing AdventureWorks data using Power BI Desktop and the Power BI Service. The approach followed best practices in data modeling, transformation, and visual storytelling.
Key steps included:

•	Data import and transformation using Power Query (e.g., profit calculations, name cleanup, category creation)

•	Creation of a star schema connecting Sales, Dates, Products, and Customers with defined relationships and hierarchies

•	Development of DAX measures for KPIs such as Total Sales, Profit Margin, Sales Target, YoY Growth, and Outliers

•	Design of interactive report pages using visuals like decomposition trees, KPI cards, bullet charts, line graphs, and geographic maps

•	Publishing to Power BI Service, dashboard creation, enabling Q&A, and implementing Row-Level Security (RLS)

To manage the project effectively, my approach was to complete each step thoroughly before moving on. I documented all significant decisions, DAX logic, modeling steps, and challenges in a notebook during development. Once the main components were finalized, I returned to capture relevant screenshots and upload the report and supporting assets to my GitHub repository. This ensured accuracy, clarity, and a smooth development workflow.
________________________________________

## 2. Challenges Faced and Solutions
•	Date Table Relationship: Issue with reversed relationship direction between Sales[OrderDateKey] and Date[DateKey] was fixed by using the original Date table and aligning data types

•	Name Cleanup: Values like "not applicable" required manual correction to maintain consistency

•	Ambiguous Aggregations: Monthly summary creation was separated into a dedicated grouped query for clarity

•	Outlier Detection Without Bloat: Used DAX to create summary-level outlier detection (99th percentile & IQR) instead of loading large datasets

•	Mapping Without Coordinates: Azure Maps was used to visualize locations without manually inputting latitude/longitude

•	Manual Hierarchy Creation: Columns like Year, Month, and Day were created manually due to auto-detection limitations

•	Model Optimization: Removed surrogate keys and unnecessary fields to streamline the model
________________________________________

## 3. Power BI Service Report Link

Report URL:
https://app.powerbi.com/links/zyqiuLeCZJ?ctid=16d83ee6-254a-469d-a6cc-54e2ca2313e7&pbi_source=linkShare
________________________________________

## 4. Screenshots of Report, Model, and Setup

// The Gallery View Screenshots can be found in the Screenshots folder, in which a folder is named after it. //

### ** Power Query Editor **

#### Transformations applied to Sales and Customers data

<img width="1905" height="1065" alt="Screenshot 2025-08-16 111420" src="https://github.com/user-attachments/assets/b3a24cf9-3360-477d-82e9-8cbd6fe61262" />


<img width="1914" height="1025" alt="Screenshot 2025-08-16 111316" src="https://github.com/user-attachments/assets/bc2f9f42-013c-4bdc-9152-5222c4071e26" />

 
### Data Model View

#### Star schema with relationships and hierarchies across tables

<img width="1200" height="713" alt="Screenshot 2025-08-16 112112" src="https://github.com/user-attachments/assets/dda406bc-d350-4cb6-bf3c-f11a51fbe946" />

 
### ** Report Pages **

### Sales Overview

<img width="1453" height="799" alt="Sales" src="https://github.com/user-attachments/assets/a9ee9320-2e51-4321-83e3-3158d700ef01" />


### Product Analysis

<img width="1427" height="788" alt="Products Top 5" src="https://github.com/user-attachments/assets/7020329b-eb8f-4ee2-bf1b-1df318e69072" />


#### Before section 5
<img width="1428" height="808" alt="Products Best" src="https://github.com/user-attachments/assets/2361bcd5-7db3-440c-83c7-caeb95a91486" />


### Customer Insights
<img width="1439" height="804" alt="Customers" src="https://github.com/user-attachments/assets/a0a54419-ad93-45e8-b2a0-b77958b49365" />


### **Power BI Service Dashboard **
#### Web View
<img width="1589" height="828" alt="DashBoard" src="https://github.com/user-attachments/assets/86f9cad9-ef60-40af-a7dd-f7549bcbf431" />


#### Mobile View
<img width="466" height="745" alt="Mobile Dash Board (1)" src="https://github.com/user-attachments/assets/009d2ccd-a22e-4393-afe3-bec081d84f80" />


### **Row-Level Security (RLS) **
<img width="1354" height="799" alt="Screenshot 2025-08-16 131958" src="https://github.com/user-attachments/assets/803f7834-cdb8-4784-92d8-9eab3cb0a9b2" />


________________________________________

## 5. Key Insights

•	Sales Performance vs. Target: In 2019, total sales reached $4.81M against a goal of $3.02M, exceeding the target by +59.24%.

•	Top Reseller: "A Bicycle Association" was the highest-performing reseller, contributing a significant share of orders and sales.

•	Regional Breakdown: Europe led in profit with ~$866K, followed by Oceania ($637K) and North America ($495K), confirming strong performance in international markets.

•	Growth Trends: Monthly YoY growth showed mixed trends with strong rebounds in later months, supported by an uptick in total sales in Q3 and Q4.

•	Product Performance: Mountain Bikes dominated sales, especially the "Mountain-200" series. The top product, "Mountain-200 Black, 38", alone contributed over $2.24M.

•	Profit Distribution: Scatter plots showed a strong correlation between high order quantity and high-profit products, validating top product performance.

•	Customer Insights: The top customer, "Maurice Shan" from France, had over $8.2K in purchases. France dominated the top customer list with most high-value customers. 

•	Sales & Profit Summary: Total sales across customers reached $7.91M with $3.18M in profit.

•	Order Activity: Order quantity peaked during FY2020 Q1 and Q2, indicating seasonally strong performance in early fiscal quarters.

•	Outlier Detection: Over 5.5K outliers were identified using combined 99th Percentile and IQR logic, used for advanced filtering and model robustness.

________________________________________

## 6. Assumptions and Limitations

•	Forecast assumes a linear trend with no seasonality

•	Budget is calculated as 1.2x of product cost due to missing actuals

•	Azure Maps used instead of manual coordinates

•	Customer names like "not applicable" were manually corrected

•	RLS only implemented for United States and Europe; dynamic RLS not configured

•	Product hierarchies assumed where none were explicitly defined

•	Not Applicable was ignored when it should up in both customers or products which creates a knowledge gap.

________________________________________

## 7. DAX Measures Summary

### KPI and Performance Metrics:

Total Sales = SUM(Sales[Sales Amount])  

Sales PY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))  

Sales Target = [Sales PY] * 1.10  

Profit Margin = SUM(Sales[Profit]) / SUM(Sales[Sales Amount])  

Profit Target = 0.3  

Average Sales = AVERAGE(Sales[Sales Amount])  

Product Rank = RANKX(ALL('Product'[Product]), [Total Sales], , DESC)  

Budget = SUM(Sales[Total Product Cost]) * 1.2

### Outlier Detection:

Outliers = 
(SUM('99th Percentile'[OutlierCount]) + 
 SUM('IQR'[OutlierCount])) / 2
 
### Time Intelligence:

MonthName = FORMAT(DATE([Year], [Month], 1), "MMMM")

### Geography Table:

The Geography table was created by summarizing customer location data across key fields like City, State/Province, Country/Region, and Postal Code. It included several enriched columns:

•	GeographyKey: A unique key built by concatenating address fields

•	StateProvinceCode: Standardized codes for US and Canada provinces/states

•	FullAddress: Used for mapping and tooltip clarity

•	Continent: Derived using conditional logic based on country

•	IsDomestic: Indicates whether the customer is based in the United States

In addition to supporting dynamic geographic analysis and map visuals, this table played a critical role in implementing Row-Level Security (RLS). It enabled region-based filtering and ensured that users only had access to data relevant to their assigned geography (e.g., United States or Europe).

