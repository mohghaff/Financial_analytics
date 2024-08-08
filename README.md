Bike Share Data Analysis Project Documentation
Overview
This project focuses on analyzing bike share data to understand usage patterns and financial performance over different periods. Using SQL Server Management Studio (SSMS) for data manipulation and Power BI for visualization, we have implemented a robust pipeline that integrates raw data into meaningful insights.

Project Objectives
Data Integration: Merge datasets from multiple years to create a unified view of bike-sharing data.
Financial Analysis: Calculate revenue and profit to assess financial performance.
Visualization: Use Power BI to provide actionable insights through interactive dashboards.
Tools and Technologies
SQL Server Management Studio (SSMS): For database management, data manipulation, and query execution.
Power BI: For data visualization and reporting.
Data Source
The dataset used in this project comprises bike share data from multiple years, imported from CSV files. It includes information on daily rides, seasonal variations, rider types, and financial metrics.

Data Processing Steps
1. Data Import
Database Creation: A new database named bike_data was created in SSMS.
Data Import: Flat file data in CSV format was imported into the database, creating tables bike_share_yr_0 and bike_share_yr_1.
2. Data Merging
Union Command: The UNION SQL command was used to append tables bike_share_yr_0 and bike_share_yr_1 into a single table.
sql
Copy code
WITH merged_tables AS (
    SELECT * FROM [bike_share_yr_0]
    UNION
    SELECT * FROM [bike_share_yr_1]
)
SELECT * FROM merged_tables;
Common Table Expression (CTE): A CTE was utilized to simplify the query and enable easier manipulation of the merged data.
3. Data Joining
Left Join: The merged data was left joined with a cost_table to integrate cost-related information, ensuring comprehensive financial analysis.
sql
Copy code
SELECT dteday,
       season,
       mt.yr,
       mnth,
       hr,
       weekday,
       rider_type,
       riders,
       price,
       COGS,
       riders * price AS revenue,
       riders * price - COGS AS profit
FROM merged_tables mt
LEFT JOIN cost_table ct ON mt.yr = ct.yr;
4. Calculations
Revenue Calculation: Revenue was calculated as the product of the number of riders and the price.
Profit Calculation: Profit was calculated as the difference between revenue and the cost of goods sold (COGS).
Data Visualization
Power BI Integration
Connection to SQL Server: The SQL Server database was connected to Power BI to enable dynamic data visualization.
Dashboard Creation: Interactive dashboards were created to visualize key performance indicators, including:
Revenue Peaks Throughout the Day: A matrix displaying revenue per hour.
KPI Over Time: A bar chart showing rider numbers over time.
Revenue by Season: A bar chart analyzing seasonal revenue.
Rider Demography: A pie chart highlighting the ratio of casual to registered riders.

Insights and Findings
Revenue Trends: Identified peak hours for revenue generation, aiding in resource allocation and operational efficiency.
Seasonal Patterns: Uncovered seasonal variations in bike usage, informing marketing and promotional strategies.
Rider Analysis: Analyzed demographics to tailor services and improve user experience.
Conclusion
This project successfully integrated multiple data sources, performed comprehensive data analysis, and provided actionable insights into bike share usage and financial performance. By leveraging SQL and Power BI, we created a powerful tool for decision-making and strategic planning.