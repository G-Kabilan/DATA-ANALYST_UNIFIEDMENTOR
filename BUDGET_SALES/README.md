
## BUDGET SALES ANALYSIS FOR SALES DOMAIN - DATA ANALYTICS


## Overview
The Budget Sales Analytics project is designed to analyze sales and budget data for a retail and sales company, providing valuable insights to aid strategic decision-making. This advanced-level project leverages Python for data processing and analysis, along Power BI for interactive visualization. The primary goals include extracting key information about sales, budget, and variance, comparing these metrics across various attributes, and uncovering meaningful relationships between different data points. Additionally, the project focuses on analyzing customer behavior and product performance, creating comprehensive dashboards, and presenting findings in a detailed project report.


### STEPS FOLLWED IN JUPYTER NOTEBOOK (Python)

- Data preparation: Ensure the data (.csv) is properly formatted and organised for import into Jupyter Notebook
- Merging the data from workbook.
- Exploratory Data Analysis- EDA
- Feature Engineering AND Data Preprocessing
- Data visualisations and Analysis

### STEPS FOLLOWED IN POWER BI
- Data preparation: Ensure the data is properly formatted and organised for import into Power BI.
- Data Modelling: Create data models and relationships within PowerBi to facilitate data analysis and visualisations.
- Dashboard Creation: Develop Interactive dashboards and reports using PowerBi visuals to visualise Budget and Sales metrics and KPIs.
- Interact with data: Explore and interact with data through filters to gain deeper insights.

for creating a new table and  column following the DAX   expression was written;
       
 	Month = Budget[Date].[month]

	Calender_1 = 
	var maxdate = max(Sales[OrderDate])
	var mindate = min(Sales[OrderDate])
	return 
	ADDCOLUMNS(
	CALENDAR(mindate,maxdate),"Year",year([Date]),"Month_Name",		FORMAT([Date],"mmm"),"Month_Number",MONTH([Date])
	,"Quarter",CONCATENATE("Q",QUARTER([Date]))
	,"Year_Quarter",CONCATENATE(year([Date]),CONCATENATE("-Q",		QUARTER([Date])))
	,"Year_Month",CONCATENATE(YEAR([Date]),CONCATENATE("-",			FORMAT	(	[Date],"mmm")))
	,"Sort_YM",YEAR([Date])*100+MONTH([Date]) 
	)

	AGE = DATEDIFF(Customers[BirthDate],TODAY(),YEAR)
	AGE BIN = SWITCH(TRUE(),
            [AGE] <= 40 , "0-40",
            [AGE] <= 60, "41-60",
            [AGE] <= 80, "61-80",
            [AGE] >= 80, "80+"
            )
	Profit Margin = (Sales[UnitPrice]*Sales[OrderQuantity])- Sales[TotalProductCost]
	sale = SUM(Sales[SalesAmount])
	Total Sales Amount = Sales[SalesAmount] + Sales[TaxAmt]

## Following DAX expressions were created using new measures.
 
- abs variance = ABS([Variance %])
- budget_1 = SUM(Budget[BudgetAmount])
- Month = Budget[Date].[month]
- Target sales = SUM(Budget[BudgetAmount])
- Variance = METRICS[Revenue]- Budget[Target sales]
- Variance % = DIVIDE([Variance],[Target sales])
- Budget = SUM(Budget[BudgetAmount])
- cost = sum(Sales[TotalProductCost])
- Profit Margin % = DIVIDE([Total Profit Margin], [Revenue],0)
- Profit margin contribution % = DIVIDE([Total Profit Margin],CALCULATE([Total Profit Margin],ALL('Product'),ALL(Territory),ALL(Customers))) 
- PYTD TOTAL SALES = CALCULATE(SUM(Sales[SalesAmount]),DATESYTD(DATEADD('Calender_1'[Date],-1,YEAR)))
- Revenue = SUM(Sales[SalesAmount])
- Revenue contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('Product'),ALL(Territory),ALL(Customers)))
- Total Profit Margin = SUM(Sales[Profit Margin])
- YoY sales = [YTD SALES]-[PYTD TOTAL SALES]/[PYTD TOTAL SALES]
- YTD SALES = CALCULATE(TOTALYTD(sum(Sales[SalesAmount]),'Calender_1'[Date]))
        
# Snapshot of Dashboard (Power BI Desktop)
## SALES OVERVIEW
![SALES_BD_SC](https://github.com/G-Kabilan/DATA-ANALYST_UNIFIEDMENTOR/assets/148671435/d43f9337-44b8-403f-918b-323a8ede9ef6)

## PROFIT OVERVIEW
![PROFIT_BD_SC](https://github.com/G-Kabilan/DATA-ANALYST_UNIFIEDMENTOR/assets/148671435/061ed522-e8fa-4cfc-b614-06eb97ef00b2)

## VARIANCE OVERVIEW
![VARIANCE_BD_SC](https://github.com/G-Kabilan/DATA-ANALYST_UNIFIEDMENTOR/assets/148671435/96cff79d-f552-408f-a07d-a8f0f2e6b1f7)

## PRODUCT OVERVIEW
![PRODUCT_BD_SC](https://github.com/G-Kabilan/DATA-ANALYST_UNIFIEDMENTOR/assets/148671435/50652812-5cea-4e1f-a02b-e6a651950db3)

## CUSTOMER OVERVIEW
![CUSTOMER_BD_SC](https://github.com/G-Kabilan/DATA-ANALYST_UNIFIEDMENTOR/assets/148671435/e26f1806-5ae8-42fa-a63b-72f462266119)
