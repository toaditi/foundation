# SQL Assignment 1

## Business Context

Your company is experiencing rapid growth in its e-commerce operations, with orders coming in from various locations and channels. As the data analyst for the fulfillment team, you are tasked with creating reports that will provide deep insights into the company's order and fulfillment processes. These reports will help management make data-driven decisions about how to optimize shipping, improve location-based logistics, and enhance revenue tracking for store-specific and online orders.

Management has provided you with several key questions to answer using SQL queries. Based on the company's data model, which you have reviewed, it's your job to query the system and provide accurate, insightful answers. The insights you gather will be instrumental in shaping the company's fulfillment strategy for the next quarter.

## Task Categories

### 1. Shipment Analysis

The fulfillment team wants to understand overall shipment trends and uncover any bottlenecks in the process. Your task is to provide answers to the following questions:

- **Total Shipments in January 2022 (Q1):**  
  Management is keen to review performance in the first quarter of 2022. Write a query to find the total number of shipments made in January 2022, broken down by days if necessary.
  
- **Shipments by Tracking Number:**  
  Every shipment should have a unique tracking number. Create a query to list or analyze all shipments, grouped by their unique tracking numbers.

- **Average Shipments per Month:**  
  Management is interested in understanding the overall shipment volume and how it fluctuates. Write a query to calculate the average number of shipments made per month in Q1.

- **Payment Captured but Not Shipped:**  
  Sometimes, there are delays between payment being captured and an order being shipped. Identify orders where payment has been successfully captured but no shipment has been made yet. This helps identify potential delays in fulfillment.

- **Multi-Item Orders (Single Ship Group):**  
  The logistics team needs to identify orders where multiple items were shipped together. Write a query to find orders where multiple items were consolidated into a single shipment group.

- **Brokered but Not Shipped Orders:**  
  Orders that have been brokered but not shipped represent a delay in the process. Create a query to identify these orders.

- **Orders Completed Hourly:**  
  The operations team is analyzing staffing needs based on order completion times. Write a query that provides a breakdown of completed orders on an hourly basis.

---

### 2. Location-Based Fulfillment Metrics

In order to optimize inventory distribution and store shipments, the company needs to understand how units are being fulfilled at different locations.

- **Shipped Units by Location:**  
  Generate a report showing the number of units shipped from each fulfillment center or store location. This will help identify which locations are handling the most volume.

- **Maximum Units Fulfilled by Location:**  
  Management wants to know which location fulfilled the most units in a given period. Write a query to identify this location and provide details on the number of units fulfilled.

- **Total Shipment Value (Facility 904/906 to Q1):**  
  Specific facilities (904 and 906) need performance tracking. Calculate the total value of shipments made from these two facilities in Q1.

---

### 3. Store-Specific Financial Insights

Your finance team wants to ensure that each store is performing well in terms of revenue. They have tasked you with the following reports:

- **Facility-Wise Revenue:**  
  Write a query to break down the revenue generated by each fulfillment facility or store. This information will help the team assess the financial health of each location.

---

### 4. Financial Metrics for Fulfillment

Tracking shipping-related revenue and refunds is crucial for profitability.

- **Shipping Refund (Last Month):**  
  Create a query that calculates the total value of shipping refunds issued last month. This helps the team identify how much money is being refunded due to shipping issues.

- **Shipping Revenue (Last Month):**  
  Write a query to calculate the total shipping revenue generated in the last month. This will provide insights into whether the shipping charges are contributing positively to the company's bottom line.

---

### 5. Historical Orders and Items

The warehouse and fulfillment teams are focused on improving efficiency by analyzing past data.

- **Last Week's Imported Orders & Items:**  
  The operations team wants to review orders and items imported last week to spot any potential trends. Write a query to identify and count the orders and items imported during this period.

- **Send Sale Orders Shipped from Warehouse:**  
  Create a report showing send sale orders (orders sold from one store location but fulfilled from a warehouse) that have been shipped from the warehouse. This will help identify if the correct items are being shipped from the proper location.

---

### 6. BOPIS (Buy Online, Pick-up In Store) Metrics

With an increasing number of customers using BOPIS, management wants to understand how much revenue this channel generates.

- **BOPIS Orders Revenue (Last Year):**  
  Write a query that calculates the total revenue generated from BOPIS orders over the past year. This will help assess the popularity and profitability of this fulfillment method.

## Conclusion

By completing this assignment, you will help the company gain critical insights into its operations, enabling better decision-making around staffing, inventory, and shipping strategies. Your SQL queries should be optimized and formatted to handle potentially large datasets efficiently.

Make sure to write clean and efficient SQL queries. Your queries should address the specific requirements while also ensuring clarity and accuracy in the data being retrieved.