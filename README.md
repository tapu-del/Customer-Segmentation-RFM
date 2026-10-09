# Customer-Segmentation-RFM
Analyzed 541,910 rows of retail transaction data to segment customers using RFM (Recency, Frequency, Monetary) analysis. Built an interactive Power BI dashboard connected directly to a PostgreSQL database.
## Tools Used
- PostgreSQL
- SQL
- Power BI

## What I Did
- Created a database in PostgreSQL (CustomerDB)
- Imported 541,910 rows of retail data
- Calculated RFM metrics for 4,373 unique customers
- Segmented customers into Loyal, New, At Risk, and Regular
- Connected Power BI directly to SQL database
- Built an interactive dashboard with KPI cards, charts, and slicer

## Key Insights
- Total Customers: 4,373
- Total Revenue: 9.75M
- Total Quantity Sold: 5M
- Average Unit Price: 4.61
- United Kingdom has the highest revenue (84%)

## Dashboard Features
- KPI Cards: Customers, Revenue, Quantity, Average Price
- Donut Chart: Revenue by Country
- Bar Chart: Revenue by Year
- Bar Chart: Revenue by Country
- Slicer: Country filter

  ## Screenshot and Query
   <img width="586" height="511" alt="image" src="https://github.com/user-attachments/assets/ac0221ef-d615-48a2-bc14-6a6715e4d435" />
  <img width="565" height="742" alt="image" src="https://github.com/user-attachments/assets/fae5ceb2-9311-403d-9fd8-fd2a55c6f704" />
  SELECT 
    CustomerID,
    MAX(InvoiceDate) AS LastPurchase,
    COUNT(DISTINCT InvoiceNo) AS Frequency,
    SUM(Quantity * UnitPrice) AS Monetary
FROM sales
WHERE CustomerID IS NOT NULL
GROUP BY CustomerID
ORDER BY Monetary DESC;SELECT 
    CustomerID,
    MAX(InvoiceDate) AS LastPurchase,
    CURRENT_DATE - MAX(InvoiceDate)::date AS Recency,
    COUNT(DISTINCT InvoiceNo) AS Frequency,
    SUM(Quantity * UnitPrice) AS Monetary
FROM sales
WHERE CustomerID IS NOT NULL
GROUP BY CustomerID
ORDER BY Monetary DESC;
SELECT 
    CustomerID,
    CURRENT_DATE - MAX(InvoiceDate)::date AS Recency,
    COUNT(DISTINCT InvoiceNo) AS Frequency,
    SUM(Quantity * UnitPrice) AS Monetary,
    CASE 
        WHEN CURRENT_DATE - MAX(InvoiceDate)::date <= 30 AND COUNT(DISTINCT InvoiceNo) >= 10 THEN 'Loyal'
        WHEN CURRENT_DATE - MAX(InvoiceDate)::date <= 30 THEN 'New'
        WHEN CURRENT_DATE - MAX(InvoiceDate)::date > 90 THEN 'At Risk'
        ELSE 'Regular'
    END AS Segment
FROM sales
WHERE CustomerID IS NOT NULL
GROUP BY CustomerID
ORDER BY Monetary DESC;
<img width="972" height="579" alt="image" src="https://github.com/user-attachments/assets/ee73dd22-9406-4f12-9bfe-2225c29a3f95" />
<img width="1094" height="607" alt="image" src="https://github.com/user-attachments/assets/d5b813b8-5250-492b-b405-3a7c7dc6d543" />




## Screenshot
![Dashboard](custom
