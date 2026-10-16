Power BI Data Analysis & Modeling 


📋 Overview

This project contains a comprehensive Power BI Desktop solution engineered to transform raw, disconnected tabular business assets into an interactive analytical model. It provides clear visibility into historical customer operations, geographical order placement frequencies, and global corporate layoff trends.
The underlying architecture leverages optimized relational mappings, row-level calculated columns, and context-aware Data Analysis Expressions (DAX) specifically customized to bypass structured zero-value anomalies.

🏗️ Data Architecture & Visualizations


1. Data Ingestion & Transformation

Three separate programmatic workbook assets were extracted, transformed, and loaded (ETL) straight into the data mesh:
• Amazingcart.xlsx — Regional and country-specific shipment parameters.
• Customer_Data.xlsx — Granular product quantities, prices, and chronological timelines.
• Employee_Layoffs.xlsx — Corporate downsizing figures, company funding metrics, and geographic tracking indices.

2. Analytical Dashboard Visuals

• Country Distribution Performance: Built a Clustered Column Chart to display countries ranked by highest transaction velocity. It handles a count aggregation across structural fields to map global performance accurately.
• Temporal Order Frequencies: Created a historical Line Chart plotting sequential timelines against global order placement metrics to reveal moving purchase shifts over time.
• Macro Organizational Impact Mapping: Engineered an executive-level Pie Chart breaking down regional corporate restructuring metrics across target geographical technology hubs.

💾 Modeling & Advanced DAX Calculations


1. Row-Level Calculated Column

To optimize granular calculations across transactional records, a calculated row-level matrix was added to the Customer_Data matrix. It accurately multiplies moving inventory items by baseline unit costs to verify ledger totals:
dax
Replicated_Total_Price = Customer_Data[Quantity] * Customer_Data[Price Per Unit ]
Use code with caution.

2. High-Performance Measures

To avoid reporting inflation caused by zero-value placeholders (0 fields acting as missing value indices instead of true blank fields), tailored evaluation criteria were injected into the data schema:

Data Density Indicators

Counts total record parameters logged across the dataset context:
dax
Total Rows Count = COUNTROWS(Customer_Data)
Use code with caution.
Isolates populated fields to distinguish recorded layoff metrics from unrecorded line properties:
dax
Valid Layoff Records = COUNT(Employee_Layoffs[Total_Laid_Off])
Use code with caution.

Custom Null Evaluation Strategy

Because missing values are explicitly populated as 0 instead of standard blank systems, a contextual table override filter was deployed via CALCULATE to extract zero-values without skewing standard system averages:
dax
Missing Layoff Values = 
CALCULATE(
    COUNTROWS(Employee_Layoffs),
    Employee_Layoffs[Total_Laid_Off] = 0
)
Use code with caution.

Extreme Boundaries Analysis

Extracts the floor inventory unit threshold across customer transactions:
dax
Smallest Quantity Ordered = MIN(Customer_Data[Quantity])
Use code with caution.
Filters out zero-value statistical anomalies to isolate the true non-zero layoff floor:
dax
True Smallest Layoff = 
CALCULATE(
    MIN(Employee_Layoffs[Total_Laid_Off]),
    Employee_Layoffs[Total_Laid_Off] > 0
)
Use code with caution.
Finds the maximum unit pricing index noted across the transactional grid:
dax
Largest Unit Price = MAX(Customer_Data[Price Per Unit ])
Use code with caution.

Financial Summarization

Aggregates capitalization metrics to track funding profiles:
dax
Total Funds Raised = SUM(Employee_Layoffs[Funds_Raised])
Use code with caution.

🚀 How to Run the Project

1. Clone this repository to your local system.
2. Install Power BI Desktop (latest release).
3. Open the .pbix dashboard model file.
4. If prompted, refresh the data links or map the file locations to the local storage path of the uploaded source files (Amazingcart.xlsx, Customer_Data.xlsx, Employee_Layoffs.xlsx).
