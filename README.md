# 🛒 Grocery Shop Database Management System

## 📌 Project Overview

The **Grocery Shop Database Management System** is a SQL-based project designed to manage customers, products, orders, order items, and payments. It demonstrates how relational databases can be used to organize business data and generate useful insights through SQL queries.

This project includes database creation, table relationships, sample data insertion, and analytical queries to calculate revenue, identify cancelled orders, analyze customer spending, and track product sales.

## 🎯 Objectives

* Create and manage a relational database using MySQL.
* Store customer, product, order, and payment information.
* Establish relationships between tables using primary and foreign keys.
* Insert sample records for testing and analysis.
* Perform SQL-based business analysis using aggregate functions and joins.
* Generate insights into revenue, customer spending, and product sales.

## 🛠️ Technologies Used

* **Database:** MySQL
* **Language:** SQL
* **Concepts:** DDL, DML, Primary Keys, Foreign Keys, Joins, Aggregate Functions, GROUP BY, ORDER BY, and Filtering

## 🗂️ Database Structure

The database is named `groceryshop` and contains five tables.

| Table         | Description                                                         |
| ------------- | ------------------------------------------------------------------- |
| `customers`   | Stores customer details, email addresses, cities, and signup dates. |
| `products`    | Stores product names, categories, prices, and available stock.      |
| `orders`      | Stores order dates, customer references, and order statuses.        |
| `order_items` | Stores products and quantities associated with each order.          |
| `payments`    | Stores payment modes, payment amounts, and payment dates.           |

### Entity Relationships

* One customer can place multiple orders.
* One order can contain multiple order items.
* One product can appear in multiple order items.
* Orders are linked to payments through `order_id`.

```text
customers
    |
    | customer_id
    |
  orders
    |
    | order_id
    |
 order_items -------- products
    |
    |
 payments
```

## 📊 Sample Dataset

The project includes sample data for testing SQL queries.

| Table       | Number of Records |
| ----------- | ----------------: |
| Customers   |                20 |
| Products    |                20 |
| Orders      |                20 |
| Order Items |                21 |
| Payments    |                20 |

The sample products include clothing, accessories, and stationery items. Orders contain different statuses, such as `Delivered`, `Pending`, and `Cancelled`, allowing the analysis of various business scenarios.

## 🔍 SQL Analysis and Queries

### 1. Calculate Total Payment Revenue

Calculates the sum of all recorded payment amounts.

```sql
SELECT SUM(amount) AS total_revenue
FROM payments;
```

**Purpose:** Provides the total amount recorded in the payments table, including payments associated with orders of different statuses.

### 2. Calculate Revenue by Product

Calculates product-level revenue for delivered orders and sorts products from highest to lowest revenue.

```sql
SELECT
    p.product_name,
    SUM(oi.quantity * p.price) AS revenue
FROM order_items oi
JOIN products p
    ON oi.product_id = p.product_id
JOIN orders o
    ON oi.order_id = o.order_id
WHERE o.order_status = 'Delivered'
GROUP BY p.product_name
ORDER BY revenue DESC;
```

**Purpose:** Identifies which products generate the most revenue from delivered orders.

### 3. Count Cancelled Orders

```sql
SELECT COUNT(*) AS cancelled
FROM orders
WHERE order_status = 'Cancelled';
```

**Purpose:** Counts the number of orders that have been cancelled.

### 4. Analyze Customer Spending

```sql
SELECT
    c.name,
    SUM(p.amount) AS total_spent
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN payments p
    ON o.order_id = p.order_id
GROUP BY c.name
ORDER BY total_spent DESC;
```

**Purpose:** Calculates the total recorded payment amount associated with each customer and ranks customers by spending.

### 5. Analyze Product Sales Quantity

```sql
SELECT
    p.product_name,
    SUM(oi.quantity) AS total_sold
FROM order_items oi
JOIN products p
    ON oi.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC;
```

**Purpose:** Determines the total quantity of each product appearing in order items.

## ⚙️ How to Run the Project

1. Install MySQL Server or open a MySQL-compatible database environment.
2. Open MySQL Workbench or your preferred SQL editor.
3. Create a new SQL script.
4. Copy the SQL code from this project into the script.
5. Execute the script to create the database, tables, and sample records.
6. Run the analytical queries at the end of the script.
7. Review the query results to understand the business insights.

The database is created using:

```sql
CREATE DATABASE groceryshop;
USE groceryshop;
```

**Note:** Run the full setup script only once in a fresh environment, or adjust it to handle existing databases and tables before rerunning it.

## 💡 Key SQL Concepts Demonstrated

* **CREATE DATABASE and CREATE TABLE:** Database and table creation.
* **INSERT INTO:** Inserting sample records.
* **PRIMARY KEY:** Uniquely identifying records.
* **AUTO_INCREMENT:** Automatically generating IDs.
* **FOREIGN KEY:** Establishing relationships between tables.
* **JOIN:** Combining data from related tables.
* **SUM() and COUNT():** Performing calculations and counting records.
* **GROUP BY:** Aggregating data by customer or product.
* **ORDER BY:** Sorting query results.
* **WHERE:** Filtering records based on conditions.

## 🚀 Possible Future Enhancements

* Add product stock validation and inventory tracking.
* Introduce constraints for positive prices and quantities.
* Add payment status and refund tracking.
* Create views for frequently used reports.
* Add stored procedures and triggers for order processing.
* Build a dashboard to visualize revenue and product performance.
* Improve revenue calculations by excluding cancelled orders and handling unpaid or refunded payments appropriately.

## 📌 Important Notes

* The database contains sample data for demonstration and learning purposes.
* The total revenue query currently sums all payment records, regardless of order status.
* The product revenue query uses product prices multiplied by quantities, rather than payment amounts.
* Customer spending is based on recorded payment amounts and may include cancelled orders.
* Payment records and order statuses should be reconciled before using these calculations for real business reporting.

## 👨‍💻 Author

**Your Name**

Aspiring Data Analyst | SQL | MySQL | Data Analysis

---

⭐ If you find this project useful, consider giving the repository a star on GitHub.
