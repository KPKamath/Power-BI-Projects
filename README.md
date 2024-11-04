The repository contains PowerBI dashboard images and a text report explaining the insights. It also includes a summary of the data extraction, transformation, and management processes used to generate these reports.
These visualizations aim to provide data-driven insights for both shareholders and management, supporting informed decision-making and evaluating salesperson performance for potential promotions.

Universal Export is a UK-based garment manufacturer producing blank clothing for retailers and wholesalers. As part of the analytics team, you've created two PowerBI reports for 2023 data:

External Report for Shareholders:
1.Overview of sales and profit trends
2.Product performance analysis
3.Sales across different countries
4.Progress on reducing air shipments (July-December 2023)

Internal Report on Salesperson Performance:
1.Individual sales and profit generation
2.New customer acquisition
3.Focus on profitable products




REPORT:


#TECHNICAL SUMMARY
The first section of this report presents the operational overview of Universal Export, while the second section focuses on the 2023 performance evaluation of the sales team. This analysis draws on various metrics derived from five datasets, each containing critical information on transactions, products, customers, logistics, and sales personnel.
The Transactions dataset includes 11 columns capturing details such as unique order numbers, customer, logistics, and product IDs, transaction dates, shipment countries, order quantities, total order value, and product price and cost per order. The Products dataset comprises 6 columns, offering insights into the different product types identified by unique product IDs, including product names, categories, colours, cost, and price per unit. The Customer dataset, with 8 columns, provides information on customers' unique IDs, names, addresses, emails, business categories, year of acquisition, and assigned salespersons. The Logistics dataset includes 5 columns that detail shipping companies, including name, ID, type (air, land, or sea), office locations, and contact details. Lastly, the Salespeople dataset provides data on 18 salespersons, including sales ID, nationality, gender, education, and age.
Data files, available in formats such as .xlsx, .csv, .txt, and .json, were imported into PowerBI using the "Get Data" option. Before creating visualizations, data preparation steps were conducted, including identifying and handling missing data. Some cells were observed to be empty in the PRICE_PER_UNIT, COST, and PRODUCT_COLOUR columns in the Products table, and in the CONTACT_EMAIL and CONTACT_NUMBER columns in the Logistics table. As removing these rows would result in data loss, the missing values were replaced with "null" to maintain dataset integrity for further analysis.
##Transformations on Transactions table:
The first transformation performed is that, a custom column is added to the transactions table which contains the profit generated by ‘n’ quantities of each product within an order. This is calculated as the difference between PRODUCT_PRICE and PRODUCT_COST and the type is saved as a whole number. Under another custom column called PROFIT_PER_UNIT, the value of profit generated divided by the quantity is stored as a decimal type. PRODUCT_PRICE is divided by QUANTITY to get the product price per unit and is saved as PRICE_PER_UNIT. The column TRANSACTION_DATE is duplicated and is transformed to get the transaction week of the year. A conditional column called TRANSACTION_MONTH is created to identify the transaction done on or before 30th June as ‘First half of the year’ and from 1st July to December as ‘Second half of the year’. 
Further, the transactions table is duplicated, unnecessary columns like TRANSACTION_DATE, TRANSACTION_WEEK, TRANSACTION_MONTH, TRANSACTION_ID, TOTAL_PRICE, CUSTOMER_ID, LOGISTIC_ID, SHIPMENT_COUNTRY, SHIPMENT_CITY, are removed and the table is renamed as Transactions_Complete. Custom column called COST_PER_UNIT is added which contains the values of PRODUCT_COST divided by the QUANTITY with type as decimal number. The Transactions_Complete table contains only the QUANTITY, PRODUCT_PRICE, PRODUCT_COST, PROFIT, PROFIT_PER_UNIT, PRICE_PER_UNIT and COST_PER_UNIT columns grouped by PRODUCT_ID. Now, new custom column named MARGINAL_PROFIT expressed in terms of percentage is added to the Transactions_Complete table which calculates the percentage of marginal profit for each product ID as PROFIT_PER_UNIT divided by PRICE_PER_UNIT.
##Transformations of Product table:
It can be observed that the per unit price and cost is missing for some of the product IDs in the products table. Moreover, for PRODUCT_ID 89, product cost is a negative number (-5) and for 29 the per unit price is 7000000 which is a very high number. If these values are not handled appropriately then this can lead to incorrect or biased results. However, from the transformations done on the Transactions_Complete table, the per unit price and cost for each product ID are accessible. Two new columns are created in products table using the following data analysis expression:
•	PPU_COMPLETE = RELATED(Transactions_Complete[PRICE_PER_UNIT])
•	CPU_COMPLETE = RELATED(Transactions_Complete[COST_PER_UNIT])
These columns contain all the missing and correct values of price per unit and cost per unit for each product ID. 
##Transformations on Salespeople table:
A link is created between the SALES_ID and Salespeople_unique_identification of the salespeople and customers table respectively. A new conditional column called “Regions” is added in the Salespeople table to split the salespeople by regions they belong to. The regions are divided into Africa, Asia, South America and Europe. 
##General transformations:
Quick measures are created to calculate the month over month change of PROFIT, PRODUCT_PRICE and count of TRANSACTION_ID. All of these transformations are necessary for curating the data in the right format as required to build the visualisations for the report.



#Business Performance Report for Universal Export – FY 2023


This report discusses the overview of performance and operational status of Universal Export for the fiscal year 2023. This year-end report aims to provide insights on overall sales and profit generated by Universal Export throughout the year paving the way to make informed decisions about the investments. 

##Product Distribution and Sales Volume Across Categories:
The product portfolio comprises 109 items across six categories, with Hoodies and T-shirts representing the largest shares of the product mix. This distribution reinforces the company’s emphasis on high-demand products, which align well with current market trends. Investing in these categories not only strengthens our competitive position but also provides a foundation for steady revenue growth. Lower-volume categories, such as Cardigans, present an opportunity to explore new marketing or product development strategies to boost demand.
 <img width="832" alt="Image 1" src="https://github.com/user-attachments/assets/5631762e-d945-4b8b-80a8-aee77c4390a5">

Sales volume analysis highlights that Hoodies and T-shirts continue to lead, contributing significantly to total revenue. The Hoodie category, generated a revenue of £271 million, followed by Jackets and Polo shirts. These core categories account for over 50% of the total revenue, reinforcing their importance to our product strategy. This pattern underscores the strong consumer preference for these categories, which should be prioritized in production and marketing strategies. By focusing on these high-performing areas, the company can maintain stable revenue streams while exploring targeted initiatives for Cardigans and other underperforming categories to stimulate additional sales. 

##Annual Sales and Profit:
In 2023, Universal Export achieved remarkable financial outcomes, recording an annual revenue of £1.04 billion with a solid profit margin of 44.8%.
 <img width="828" alt="Image 3" src="https://github.com/user-attachments/assets/7f64cbd9-2f8e-407b-bb8c-c42098b7bdc0">

##Monthly Sales and Profit Trends:
 <img width="832" alt="image 2" src="https://github.com/user-attachments/assets/c3118e4c-041b-40aa-abd5-98b36b65ac9f">
 <img width="771" alt="Image 5" src="https://github.com/user-attachments/assets/30389762-89ad-4264-92e2-4e6dbe210c8a">

Monthly performance peaked in August and July, driven largely by demand for Polo shirts and Hoodies. This seasonal growth aligns with back-to-school demand and supports strategies for future promotional timing. Lower sales in February and March reflect typical post-holiday slowdowns, indicating the need for focused inventory and cost management during these periods.

##Sales Distribution by Country:
Universal Export has a solid market presence across Europe, with the United Kingdom being the leading revenue driver, contributing £249 million. France and Spain also contribute significantly to our overall revenue, further cementing the company’s strong position within Europe. These insights guide our geographic resource allocation and highlight the need for targeted marketing to reinforce and expand our foothold in these high-performing regions.
 <img width="828" alt="Image 4" src="https://github.com/user-attachments/assets/66438cd1-6d7e-4fa9-bed0-23a447e2f337">

##Shipment Mode Trends:
Universal Export promotes sustainability by its deep commitment to shipping the orders in an environment friendly manner. Aligned with the commitment, a goal was set to minimise the shipment of orders done exclusively through air from 1st July 2023. 
 <img width="828" alt="Image 6" src="https://github.com/user-attachments/assets/f0250ea0-9d1f-4789-8e02-9f1997cbd06c">
 <img width="830" alt="Image 7" src="https://github.com/user-attachments/assets/ee751698-ab29-4acb-bc41-db194ddd3993">

In FY-23, 11K orders were shipped through air, 9K via land, 3K through the sea and 12K through mixed mode of air, land and sea throughout the year. 
A month-by-month breakdown of air shipments reflects a noticeable increase in July, driven by demand surges. In the first half of the year a total of 5K orders were shipped through air and during the second half it raised to 5.5K. An increase of 10% was witnessed in the shipment exclusively done through air during the second half of the year. Even through great efforts were made, the results failed to meet expectations. This unexpected increase was due to several sudden operational constraints. Despite the setback, Universal Export will continue to be committed to sustainability. This experience emphasized on the requirement of a robust planning to address the potential hurdles. 
To conclude it can be said that FY-23 was a year with challenges and opportunities for the company. The diverse product portfolio contributed largely to the profitability of the company. Universal Export closed the year of 2023 with remarkable sales of £1.04 billion that lead to a profit of £0.46 billion. This in-depth report provides a transparent analysis of the company’s overall performance, strengths and improvement opportunities. 


#INTERNAL REPORT
This report intends to provide a comprehensive evaluation of the sales performance for 2023 of individual salespeople contributing to the success of Universal Export. Several key criteria are taken into account for the evaluation that is essential to determine the best employees to be promoted to the positions of head and deputy head of the sales department.
##Salespeople Information & Performance Summary:
Universal Export has a total of 18 salespeople from different parts of the world. There are 4 men and 9 women from various parts of Europe. Further, there is one female each from Africa and South America. Moreover, there is one male representative from Africa and two from Asia.
 <img width="857" alt="Image 8" src="https://github.com/user-attachments/assets/9a264436-8e0a-4718-911b-b09c8bdbdb53">

The chart provides a clear comparison between the revenue and profit generated by each sales person throughout the fiscal year of 2023. A noticeable difference exists in the ranking of the performance by each individual indicating their abilities to strategically sell the products to the customers. The sales person with ID 22 has outperformed the others by making a revenue of £112 million contributing to £50 million of the total net profit. Sales person ID 12 is observed to be the second highest with a sales total of £85 million generating £38 million profits. ID number 7 appeared as the third highest with sales equal to £75 million and contributed to £34 million of the total profit. The rest of the salespeople have comparatively underperformed suggesting a need to focus, and a scope for development. 
##New customers acquired in 2023:
Acquiring new customers is vital for sustainable growth, and several team members stood out by successfully expanding the customer base. Salespersons ID 4, 5, 12, and 22 each brought in new clients in 2023, reflecting proactive approaches that contribute to business development.
 <img width="542" alt="Image 10" src="https://github.com/user-attachments/assets/5f6df25f-5ff5-456c-9f43-365d0cac66bd">
 
##Top Revenue-Generating Products:
 <img width="542" alt="Image 9" src="https://github.com/user-attachments/assets/90c9f591-d3ba-4913-9d83-0f2d516164cd">
Product-level analysis reveals that certain items in the Jacket category, such as the V1 Bomber Jacket in Tan(ID-70) and Sunlight (ID-69), drive significant revenue equal to £23.47 million and £23.09 million respectively. The Military Jacket Blue (ID-73) was the third highest with a contribution of £23.03 million. Sales data indicates strong sales of these products by top-performing salespeople, further emphasising the importance of high-demand items.

 <img width="680" alt="Image 11" src="https://github.com/user-attachments/assets/04b1d251-6273-4106-a3c1-01a428f096a8">
Looking at the quantity of the top three revenue generating products sold by each sales person, it is noticeable that sales ID 22 has surpassed the others by selling 181K units of these products. The second highest is ID 12 by selling 147K units and the third is ID 7 with 140K units throughout the year.

##Profit margin analysis:
The term marginal profit is calculated as the difference between the selling price and manufacturing cost of a product divided by the selling price expressed as percentage.
After the margin calculation it can be said that about 14 products, all belonging to the Hoodie category have the highest profit margin of 68.75%. These 14 products are the Xtra Sport Hoodie for Athlete in different colours (product ID 89 to 102). The specified products stand out in the entire portfolio of products with highest potential to drive profitability for Universal Export.
 <img width="680" alt="Image 12" src="https://github.com/user-attachments/assets/97b9e18e-62bd-4756-b73f-b364294d50af">

The salespeople who strategically focused on marketing and selling the maximum units of these products demonstrate a good understanding of the company’s profit margin and contribute significantly to the overall profitability of Universal Export.
 <img width="680" alt="Image 13" src="https://github.com/user-attachments/assets/b3e86732-95ee-427f-af23-cc5a714a399a">

It can be concluded that sales person ID 22 and 12 have outperformed once again by exhibiting a clear understanding of the company profit margins and selling 847K and 671K units of Xtra Sport Hoodie for Athlete respectively. Sales ID number 7 is again in the third spot by selling 580K units. These top 3 salespeople have collaboratively contributed to the overall profit significantly by their strategic focus on company’s profitability.
Hence, it can be concluded that although most of the salespeople performed well, salespeople ID 22 and 12 have emerged as the top 2 best performers for the year by outshining in all the key metrics like revenue and profit by emphasizing on increasing the sales volume of high revenue generating as well as high marginally profitable products. They have also proven to be successful in acquiring a new customer for the fiscal year 2023. In spite of performing well in most of the metrics, sales ID 7 was unable to acquire a new customer for the year. Additionally, the report highlights the top 3 revenue generating products and the corresponding sales made by the salespeople highlighting their skills and abilities. All the above discussed insights are provided after a critical analysis of the data. This report can be used to make informed decision regarding the promotions of salespeople for the position of head and the deputy head of the company’s sales department.

