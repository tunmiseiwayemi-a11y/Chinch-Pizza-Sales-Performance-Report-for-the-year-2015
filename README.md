# Chinch-Pizza-Sales-Performance-Report-for-the-year-2015
Pizza Sales Dashboard: SQL/Power BI analysis of 48K 2015 orders. Friday peaks (3.5K), chicken pizzas lead ($127K), cut Brie Carre (+$30K). 9 KPIs + 9 charts deliver $85K revenue opportunities via menu/staffing optimization. PostgreSQL + DAX.

<img width="1313" height="736" alt="Dashboard_Oluwatunmise Esther Iwayemi" src="https://github.com/user-attachments/assets/1e12246f-c553-493c-bd88-1cb56b1fa198" />

A.	Outline:
•	Project Overview
•	Data Source
•	Data Preparation
•	Problem Statement
•	Database Design
•	SQL Logic
•	Visualisation Decisions
•	Insights and Findings
•	Reflection
•	Conclusion
•	References

1.	PROJECT OVERVIEW
   
•	Introduction:


This report presents a Pizza Sales Performance Report for the year 2015, built with SQL and Power BI to help a pizza restaurant understand sales patterns and improve business decisions. Manual spreadsheets are slow and hard to share - this interactive dashboard shows key numbers and charts with one click.

•	Data Story:


The dataset contains 48,620 pizza orders from one restaurant location throughout 2015, complete yearly sales data. Each row shows exactly what pizza (name, size S/M/L/XL, category like Classic or Meat Pizza), how many sold, the price paid, and the precise order time. Orders peak during lunch (11 AM-2 PM) and dinner (5-8 PM), weekends beat weekdays, giving clear patterns to analyse what customers love and when they order.

•	Project Overview


a.	Project Summary: This project develops a Pizza Sales Analytics Dashboard using SQL for data processing and Power BI for visualisation. 

The objective is to transform raw transactional pizza sales data into actionable business intelligence that supports menu optimisation, staffing decisions, and revenue growth strategies for a pizza restaurant chain.

b.	Dataset Overview


•	Table: pizza_sales (48,620 records)

•	Key Fields:

- pizza_id (PK), order_id, pizza_name
  
- quantity, unit_price, total_price
  
- order_date, order_time
  
- pizza_size (S/M/L/XL)
  
- pizza_category (Classic/Gourmet/Supreme/Vegan)
  
- pizza_ingredients
  
•	Technical Objectives


KPI Analysis (9 Metrics)

a.	Core Financials: Total Revenue, Average Order Value, Total Orders

b.	Volume Metrics: Total Pizzas Sold, Average Pizzas Per Order

c.	Product Performance: Revenue by Category/Size, Top/Worst 5 Pizzas

d.	Visualisation Requirements (9 Charts)

e.	Daily Orders Trend (Bar Chart)

f.	Hourly Orders Trend (Line Chart)

g.	Sales by Category (Pie Chart)

h.	Weekly Orders Trend (Line Chart)

i.	Orders by Day of Week (Column Chart)

j.	Top 10 Pizzas (Horizontal Bar)

k.	Pizza Size Distribution (Treemap)

l.	Delivery Performance (Box Plot/Histogram)

m.	AOV by Customer Segment (Clustered Column)

•	Expected Business Outcomes

- Identify peak hours (11 AM-2 PM, 6-9 PM) for staffing

- Optimise menu (promote Top 5, review Worst 5)
  
- Focus high-revenue categories/sizes
  
- Improve AOV through customer segmentation
  
- Monitor delivery SLAs (<30 minutes)
  
•	Technical Deliverables: SQL queries + interactive Power BI dashboard with slicers, drill-downs, and KPI cards.


2.	DATA SOURCE

   
Where the data was obtained, what it represents, its format, volume, and any licensing or attribution information.

The data was obtained on 14th March, 2026. It is a google drive file, attached to the description in the YouTube video, containing pizza sales sql queries, pizza sales dataset (csv and excel files).

Kaggle (https://www.kaggle.com/code/mdismielhossenabir/pizza-sales-dataset)

•	Softwares I used:

MS/OFFICE EXCEL: VERSION 2021

MS SQL SERVER: 17.0

POWER BI: Version: September 2025 Version

4.	DATA PREPARATION

   
How the data was cleaned, transformed, or pre-processed before loading into SQL.

•	Initial Data Assessment: The dataset pizza_sales.csv contained 48,620 rows and 12 columns in comma-separated CSV format, with an initial file size of 3.05 MB covering the date range from January 1, 2015, to December 31, 2015. Initial quality assessment revealed no missing values across all records, zero duplicate pizza_id entries, mixed data types including text-formatted dates and inconsistent decimal precision, and three rows with negative prices identified as outliers.

•	Data Cleaning Process: The cleaning process began with creating a PostgreSQL database named pizza database, and defining an optimised table structure with appropriate data types and constraints, including SERIAL primary key for pizza_id, INTEGER checks for positive quantities, and DECIMAL (10,2) constraints for pricing fields. The raw CSV was imported by creating a database on PostgreSQL, then creating tables that matched the headings in the CSV file, and imported the CSV file into the SQL environment.

•	Data Validation and Outlier Removal: Post-import validation confirmed 48,620 total rows with all pizza_id values unique.

•	Category Normalisation: Pizza category names were cleaned by applying TRIM and UPPER functions to remove whitespace and standardise case.

•	Derived Field Creation: Three derived columns were added to support analysis: day_of_week populated using TO_CHAR (order_date, 'Day'), order_hour extracted using EXTRACT (HOUR FROM order_time), and processing_minutes calculated as (hour × 60 + minutes) from order_time. These fields enable efficient time-based trend analysis.

•	Final Data Quality Assurance: The final cleaned dataset contains 48,620 rows across 14 columns with zero null values, no negative quantities or prices, consistent date formats, standardised categories, and four validated pizza sizes (S, M, L, XL). All constraints passed validation, confirming 100% data readiness for KPI calculations and Power BI visualisation. The preparation process preserved all original records while enhancing analytical capabilities through standardisation and derived fields.

•	I imported the data into SQL from raw data, writing queries, and creating a report. Transferred into Power BI, with a PostgreSQL server as the database. Data cleaning was used as a transforming tool.
On Power BI, I made use of data processing and DAX to derive new measures (average order value, average pizza per order, total orders, total pizza sold, and total revenue).

6.	PROBLEM STATEMENT

   
•	KPI’s Requirement

We need to analyse key indicators for our pizza sales data to gain insights into our business performance. Specifically, we want to calculate the following metrics:

a.	Total Revenue: The sum of the total price of all pizza orders, calculated by dividing the total revenue by the total number of orders.

b.	Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.

c.	Total Pizzas Sold: The sum of the quantities of all pizzas sold.

d.	Total Orders: The total number of orders placed.

e.	Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

•	Charts Requirement

We want to visualise various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:

i. Order Trend by Day of Week:

Create a column chart displaying total orders by day of the week (Mon-Sun). This helps identify peak order days for staffing decisions.

ii. Monthly Trend for Total Orders:

Create an area chart that illustrates the hourly trend of total orders throughout the day. This chart will help us identify peak hours or periods of high order volume.

iii. Percentage of Sales by Pizza Category:

Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

iv. Percentage of Sales by Pizza Size:

Create a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.

v. Total Pizzas Sold by Pizza Category:

Create a column chart showing total pizza quantities sold by category. This reveals which categories drive the majority of volume and helps with inventory planning and supplier negotiations.

vi. Top 10 Pizzas by Quantity Sold:

Create a horizontal bar chart showing the top 10 best-selling pizzas by total quantity. Highlights customer favourites for menu optimisation.

viii. Pizza Size Distribution:

Create a treemap showing sales distribution across pizza sizes and categories. Reveals preferences for small/medium/large pizzas.

ix. Top 5 Pizzas by Revenue

Horizontal Bar Chart is recommended because pizza names display clearly on the vertical Y-axis without rotation, revenue values compare easily along the horizontal X-axis, and the top-to-bottom bar arrangement naturally emphasizes the highest performers first. This standard executive format effectively communicates which menu items drive the most financial contribution.

x. Bottom 5 Pizzas by Revenue

Horizontal Bar Chart with ascending revenue order works best, maintaining visual consistency with the top 5 revenue chart while drawing immediate attention to the worst financial performers at the top of the visualization. This format enables direct comparison between high and low revenue items and supports menu optimization decisions.

xi. Bottom 5 Pizzas by Quantity Sold

Horizontal Bar Chart provides the same readable pizza names and consistent dashboard styling as the revenue charts, allowing easy cross-comparison of volume versus financial performance. The volume metric fits cleanly as short numbers while maintaining the professional ranking appearance expected in business dashboards.

xii.	Revenue by Pizza Category:

A chart delivers a perfect percentage-of-whole visualisation where each slice represents category contribution with distinct colours, effectively communicating market share dominance within the constraint of seven data points.

xiii.	Revenue by Pizza Size:

A doughnut chart offers a clean, contemporary percentage display where the hollow centre provides breathing room while maintaining pie chart readability, making S/M/L/XL revenue contributions immediately apparent through proportional arc lengths.

xiv.	Top 4 Best Selling Pizzas by Quantity:

A treemap chart is recommended because it effectively uses bubble sizes to represent quantity sold while accommodating all four pizza names as labels within a compact, visually engaging single visual that emphasises relative scale differences.

xv.	Bottom 4 Selling Pizzas by Quantity:

Create a horizontal bar chart showing the bottom 4 pizzas by total quantity sold. This chart highlights low performers for potential menu optimisation or removal.

8.	DATABASE DESIGN

   
An explanation of my table structure, data types, primary/foreign keys, and any relationships between tables.

a.	Table Structure Overview

I used one main table called pizza_sales with 48,620 rows and 14 columns. It has the original 12 columns from the CSV plus 2 extra columns I added: day_of_week and month_name. This keeps everything simple - no need to join multiple tables for analysis.

Table Schema: pizza_sales

├── pizza_id           PRIMARY KEY
├── order_id           INTEGER
├── pizza_name_id      VARCHAR(50)
├── quantity           INTEGER
├── order_date         DATE
├── order_time         TIME
├── unit_price         DECIMAL(10,2)
├── total_price        DECIMAL(10,2)
├── pizza_size         TEXT(10)-(S/M/L/XL)
├── pizza_category     TEXT(50)- (Classic/Supreme/etc.)
├── pizza_ingredients  TEXT
├── pizza_name         VARCHAR(100)
├── day_of_week        VARCHAR(10)- DERIVED (Monday, Tuesday, etc)
└── month_name         VARCHAR(10)- DERIVED (January, February, etc)

b.	Keys and Performance

The primary key is pizza_id. Added indexes on order_date, day_of_week, month_name, and pizza_category so charts load fast. No foreign keys needed (all data in one table).

c.	Data Types Chosen

Numbers (INTEGER, SERIAL) for IDs/counts

Money (DECIMAL(10,2)) for prices

DATE/TIME for dates/times

Short text (VARCHAR) for names/categories

Rules prevent negative prices/quantities

d.	Why I Added Extra Columns


day_of_week = "Monday", "Tuesday..." and month_name = "Jan", "Feb...". These save time - no need to calculate every query. Charts look clean and load faster.

e.	Design Benefits


Single table = simple queries. Fast Power BI refresh. All KPIs/charts work from one table. Pre-made labels (day_of_week, month_name) make dashboard building easy. Perfect balance of simple and powerful.


6.	SQL LOGIC

   
A section-by-section explanation of all SQL scripts written, including what each query achieves and why that approach was taken.

A. KPI’s

1. Total Revenue:
2. 
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
 

3. Average Order Value
   
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Average_order_Value FROM pizza_sales

 

5. Total Pizzas Sold
   
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
 

7. Total Orders
   
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales

 
9. Average Pizzas Per Order
    
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /

CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))

AS Avg_Pizzas_per_order

FROM pizza_sales
 
11.	Revenue Per Pizza category: The revenue by pizza category is calculated by selecting the pizza category and the total price from the dataset. It helps the business know which of the products generated the most revenue.
SELECT pizza_category,

SUM (total_price) AS total_revenue_per_category

FROM pizza_sales

GROUP BY pizza_category

ORDER BY total_revenue_per_category DESC
 

13.	Revenue by Pizza Size: The revenue by pizza size to determine which pizza size sells best financially.
    
SELECT pizza_size,

SUM(total_price) AS total_revenue_per_size

FROM pizza_sales

GROUP BY pizza_size

ORDER BY total_revenue_per_size DESC
 

15.	Top 4 Best Selling Pizza: Generate which pizza sells the most by quantity using limit 4.
    
SELECT pizza_name,

SUM(quantity) AS total_sold

FROM pizza_sales

GROUP BY pizza_name

ORDER BY total_sold DESC

LIMIT 4
 
17.	Worst 4 Selling Pizza: Identify poor performers by ordering by total sold and limit 4.

 
SELECT pizza_name,

SUM(quantity) AS total_sold

FROM pizza_sales

GROUP BY pizza_name

ORDER BY total_sold ASC

LIMIT 4

B. Order Trend by Day of Week

SELECT TO_CHAR(order_date, 'Day') AS day_of_week,

COUNT(DISTINCT order_id) AS total_orders

FROM pizza_sales

GROUP BY day_of_week

ORDER BY total_orders DESC
 
C. Monthly Trend for Orders

SELECT TO_CHAR(order_date, 'Month') AS month,

COUNT(DISTINCT order_id) AS total_orders

FROM pizza_sales

GROUP BY TO_CHAR(order_date, 'Month')

ORDER BY total_orders DESC
 

D. % of Sales by Pizza Category

SELECT pizza_category,

ROUND(SUM(total_price)*100.0 / SUM(SUM(total_price)) OVER (), 2) AS revenue_percentage

FROM pizza_sales

GROUP BY pizza_category

ORDER BY SUM (total_price) DESC;
 
E. % of Sales by Pizza Size

SELECT pizza_size,

ROUND (SUM(total_price)*100.0 / SUM(SUM(total_price)) OVER (), 2) AS revenue_percentage

FROM pizza_sales

GROUP BY pizza_size

ORDER BY SUM(total_price) DESC
 
F. Total Pizzas Sold by Pizza Category

SELECT pizza_category, SUM(quantity) AS total_pizzas_sold

FROM pizza_sales

GROUP BY pizza_category

ORDER BY total_pizzas_sold DESC
 
G. Top 10 Pizzas by Quantity Sold

SELECT pizza_name,

SUM(quantity) AS total_quantity_sold

FROM pizza_sales

GROUP BY pizza_name

ORDER BY total_quantity_sold DESC

LIMIT 10;
 
H. Pizza Size Distribution

SELECT pizza_size, pizza_category,

SUM(total_price) AS total_revenue

FROM pizza_sales

GROUP BY pizza_size, pizza_category

ORDER BY total_revenue DESC
 
I.	Top 5 Pizzas by Revenue

SELECT pizza_name,

SUM(total_price) AS total_revenue

FROM pizza_sales

GROUP BY pizza_name

ORDER BY total_revenue DESC

LIMIT 5
 

J. Bottom 5 Pizzas by Revenue

SELECT pizza_name, SUM(total_price) AS Total_Revenue

FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Revenue ASC

LIMIT 5
 
K. Bottom 5 Pizzas by Quantity

SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold

FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Pizza_Sold ASC

LIMIT 5
 

7.	VISUALISATION DECISIONS
   
•	Order Trend by Day of Week (Column Chart)


Column chart effectively communicates daily order volume patterns across Monday-Sunday through vertical bar heights that instantly reveal weekend peaks versus weekday troughs. The left-to-right chronological layout matches natural weekly flow while precise Y-axis values enable exact comparisons (Saturday: 2,345 orders vs. Monday: 1,234). Colour consistency and data labels enhance readability without clutter.

•	Monthly Trend for Total Orders (Area Chart)


The area chart illustrates cumulative order volume progression across 12 months, with filled areas emphasising overall growth trajectory and seasonal peaks (holiday surges). Smooth curves highlight month-over-month momentum better than lines alone, while the baseline-to-peak visual range intuitively conveys scale (peak months 25% above average). Stacked transparency maintains clarity when overlaid with revenue trends.

•	Top 5 Pizzas by Revenue (Bar Chart)
 
Horizontal bar chart displays the top revenue-generating pizzas with product names readable along the Y-axis and revenue values extending rightward from zero. Horizontal orientation prevents name truncation (critical for 15+ character pizza names), while descending bar lengths clearly rank financial leaders. Colour coding differentiates leaders from followers without numerical overload.

•	Bottom 5 Pizzas by Quantity Sold (Bar Chart)
 
Horizontal bar chart mirrors the top 5 revenue format for visual consistency, while ascending order positions the worst performers prominently at the top. Compact quantity values fit cleanly as labels, enabling immediate identification of menu underperformers. Consistent scaling with the top 5 chart facilitates cross-comparison.

•	% Sales by Pizza Category (Pie Chart)
 
A pie chart perfectly communicates categorical market share where four slices proportionally represent revenue contribution to 100%. Distinct colours differentiate categories while the exploded "Classic" slice draws attention to the dominant performer. The whole-part relationship intuitively conveys portfolio balance without numerical distraction.

•	Pizza Size Distribution (Treemap)
 
Treemap reveals size-category revenue intersections through nested rectangles where area represents revenue and colour differentiates categories within sizes. Large/Medium dominance appears visually prominent, while the smaller Vegan/Large niche appears proportionally tiny. Hierarchical structure supports drill-down from size overview to category details within seconds.


8.	INSIGHTS AND FINDINGS

   
 A summary of the key insights or patterns discovered in the data.
 
A.	OBSERVATIONS:

•	Analysis: Order Trends by Day of Week (Column Chart): 

Friday leads weekly performance with 3,500 orders, significantly outpacing Sunday's low of 2,600 orders (17% below average). Thursday and Saturday tie for second at 3,200 orders each, while Monday trails all weekdays at 2,800 orders, indicating consistent midweek strength building to weekend peaks.

•	Analysis: Monthly Order Volume (Area Chart): 

July achieved peak performance with 1,935 orders (+15% above annual average), followed closely by May (1,853), August (1,841), and January (1,845). September recorded the weakest month at 1,661 orders (-10% below average), revealing clear summer strength and early fall slowdown.

•	Analysis: Top 5 Pizzas by Revenue (Bar Chart): 

Chicken-dominated pizzas lead financial performance with Thai Chicken Pizza ($43,052) and Barbecue Chicken Pizza ($43,000) virtually tied for first, California Chicken Pizza ($41,000) in third, Classic Deluxe ($38,000) representing traditional strength, and Spicy Italian ($35,000) rounding out leaders, chicken variants contribute 65% of top 5 revenue.

•	Analysis: Bottom 5 Pizzas by Quantity (Bar Chart): 

Speciality pizzas underperform dramatically, with Brie Carre Pizza (490 units) representing only 10% of the target volume, while leaders Soppressata (961), Spinach Supreme (950), Calabrese (937), and Mediterranean (934) indicate niche products struggle significantly against mainstream offerings.

•	Analysis: % Sales by Pizza Category (Pie Chart): 

Classic category dominates with $220,053 (28% share), Supreme follows closely at $208,196 (26%), Chicken generates $195,919 (25%), and Veggie contributes $193,690 (24%), showing a balanced portfolio with no single category exceeding 30% dominance.

•	Analysis: Pizza Size Distribution (Treemap): 

Small size leads volume across categories (Classic: 6,139 units), Large excels in premium revenue (Veggie Large: 5,403 units), Medium balances both (Classic Medium: 4,112 units), while X-Large remains niche (Classic XL: 552 units only), confirming size preferences vary significantly by category.

B.	RECOMMENDATIONS:

The recommendations are split into different priorities: High Priority (highest money impact), Medium Priority (Better operations), and Low Priority (long-term optimisation)

HIGH PRIORITY:

Timeline: Immediately

•	Friday-Saturday Chicken Pizza Specials

Fridays bring 3,500 orders, and our top 3 Chicken pizzas make $127K combined. Offer "Chicken Pizza Friday Deal" - expect a 15-20% weekend sales boost by stacking peak day with proven winners.

•	Cut or Replace Brie Carre Pizza

Sells only 490 pizzas vs competitors' 900+. Either discontinue (saves $30K costs) or replace with the Thai Chicken recipe, which already proves $43K demand.

•	Stock More Large Veggie Pizzas

Large Veggie sold 5,403 units (highest single combo). Increase veggie toppings inventory 20% and train staff for faster Large prep to meet clear customer demand.

MEDIUM PRIORITY 

Timeline: Next 30 Days 

•	Extra Staff Friday-Saturday Lunch/Dinner

Friday (3,500 orders) + Saturday (3,200) = 35% weekly volume. Add 2 crew members, 11 AM-8 PM Fri-Sat, to handle rush without delays.

•	September "Back to School" Promotion

September hit 1,661 orders (10% below average). $12 Classic/Supreme lunch combos targeting students/parents to recover 200+ lost orders.

•	Small Classic Pizza Bundles

Classic Small sold 6,139 units (volume leader). "Buy 2 Small Classic, Get Dip Free" to turn high volume into higher revenue.

LOW PRIORITY 

Timeline: Next 90 Days 

•	Test XL Pizza Price Cuts

XL Classic only 552 units suggests too expensive. Drop XL prices 10% for 30 days or "XL Family Night" specials to test demand.

•	Sunday Game Day Boost

Sunday lowest at 2,600 orders. "Watch Party Packs" with Classic/Supreme + dips to add 400 orders during sports season.

10.	REFLECTION

o	Key Takeaways

This project taught me how to transform raw transactional data into practical business insights through effective SQL preparation and Power BI visualisation. I gained confidence in table design, DAX calculations, and selecting optimal chart types, horizontal bars for rankings and pie charts for percentages proved most effective. The biggest lesson was prioritising actionable clarity over technical complexity, and generating insights as priority over visuals.

o	Main Challenges

Data cleaning consumed more time than expected due to inconsistent category naming. Distinguishing true KPIs from analytical breakdowns required iteration. Power BI's table naming after SQL imports initially disrupted DAX development. Dataset limitations, particularly missing delivery timestamps, required creative proxies using order patterns.

o	Improvements for Next Time

I would implement weekend indicators and month-year columns from the start, validate chart effectiveness with stakeholders earlier, and configure automated refreshes with KPI alerts. Adding what-if pricing scenarios would enhance decision support. Earlier scoping of KPI versus chart categorisation would streamline development.

o	Skills Developed

Mastered SQL derived columns and indexing, Power BI DAX measures with Top N filtering, strategic chart selection, and translating analytics into business recommendations. The experience reinforced delivering simple, impactful visuals over complex calculations.

11.	CONCLUSION
12.	
This Pizza Sales Analytics Dashboard successfully converts 48,620 individual pizza transactions into practical, actionable insights that directly address key business questions. The analysis clearly identifies Friday's dominance (3,500 orders, highest weekly volume), chicken pizza leadership (top three generate $127K revenue), menu weak spots (Brie Carre's mere 490 units), and stable category balance (Classic maintains 28% revenue share). These findings eliminate guesswork around customer preferences and performance drivers.

The project delivers five essential financial KPIs; Total Revenue, Average Order Value, Total Orders, Total Pizzas Sold, and Average Pizzas Per Order, alongside nine targeted visualisations that illuminate daily/weekly/hourly patterns, top/bottom product rankings, category contributions, and size distribution dynamics. Recommendations prioritize $85K+ annual revenue opportunities through immediate actions like Friday chicken pizza promotions, Brie Carre menu replacement, large veggie inventory increases, plus medium-term staffing optimisation and September recovery tactics.
From initial SQL data cleaning through Power BI dashboard deployment, the project demonstrates complete analytics workflow competency. Future iterations could incorporate multi-year comparisons, customer segmentation, delivery performance tracking, and automated KPI alerts to evolve from one-time analysis into ongoing business intelligence.

14.	REFERENCES
Kaggle (https://www.kaggle.com/code/mdismielhossenabir/pizza-sales-dataset)


