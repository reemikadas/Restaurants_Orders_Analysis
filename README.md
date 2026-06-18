# 🍽️ Restaurant Orders SQL Analysis

A structured SQL project exploring restaurant menu and order data to uncover customer behavior and business insights.

> **Data Source:** [Maven Analytics Data Playground – Restaurant Orders](https://mavenanalytics.io/data-playground?order=date_added%2Cdesc&pageSize=10&search=Restaurant%20Orders)

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Database Schema](#database-schema)
- [Data Dictionary](#data-dictionary)
- [Project Structure](#project-structure)
- [Analysis Objectives](#analysis-objectives)
- [Key Findings](#key-findings)
- [How to Run](#how-to-run)
- [Tools Used](#tools-used)

---

## Project Overview

This project analyzes a restaurant's menu and order data spanning **Q1 2023 (January – March)**. The goal is to explore the menu offerings, understand ordering patterns, and analyze customer spending behavior using MySQL.

The analysis is broken into three objectives:
1. Explore the menu
2. Explore order activity
3. Analyze customer behavior by joining the two tables

---

## Database Schema

The database `restaurant_db` contains two tables joined by `item_id` ↔ `menu_item_id`:

```
menu_items
──────────────────────────────
menu_item_id  (PK, SMALLINT)
item_name     (VARCHAR 45)
category      (VARCHAR 45)
price         (DECIMAL 5,2)

order_details
──────────────────────────────
order_details_id  (PK, SMALLINT)
order_id          (SMALLINT)
order_date        (DATE)
order_time        (TIME)
item_id           (SMALLINT) → FK to menu_items.menu_item_id
```

**Relationship:** `order_details.item_id` → `menu_items.menu_item_id`

---

## Data Dictionary

### `menu_items`

| Field          | Type         | Description                                      |
|----------------|--------------|--------------------------------------------------|
| menu_item_id   | SMALLINT     | Unique ID of a menu item                         |
| item_name      | VARCHAR(45)  | Name of the menu item                            |
| category       | VARCHAR(45)  | Cuisine category (American, Asian, Mexican, Italian) |
| price          | DECIMAL(5,2) | Price in US Dollars                              |

### `order_details`

| Field            | Type      | Description                                        |
|------------------|-----------|----------------------------------------------------|
| order_details_id | SMALLINT  | Unique ID of a line item in an order               |
| order_id         | SMALLINT  | ID of the order (groups multiple items together)   |
| order_date       | DATE      | Date the order was placed (MM/DD/YY)               |
| order_time       | TIME      | Time the order was placed (HH:MM:SS AM/PM)         |
| item_id          | SMALLINT  | References `menu_item_id` in the menu_items table  |

---

## Project Structure

```
restaurant-orders-sql/
│
├── create_restaurant_db.sql          # Schema creation + data insert scripts
├── menu_items.csv                    # Raw menu data (32 items)
├── order_details.csv                 # Raw order transaction data (~12,000+ rows)
├── restaurant_db_data_dictionary.csv # Field descriptions for both tables
└── Project_1_Restaurants_Orders.sql  # All analysis queries (3 objectives)
```

---

## Analysis Objectives

### Objective 1 – Explore the Menu

| # | Question |
|---|----------|
| 1 | View all menu items |
| 2 | How many items are on the menu? |
| 3 | What are the least and most expensive items? |
| 4 | How many Italian dishes are on the menu? |
| 5 | What are the least and most expensive Italian dishes? |
| 6 | How many dishes are in each category? |
| 7 | What is the average price per category? |

---

### Objective 2 – Explore the Orders Table

| # | Question |
|---|----------|
| 1 | View all order details |
| 2 | What is the date range of the data? |
| 3 | How many unique orders were placed? |
| 4 | How many total items were ordered? |
| 5 | Which orders had the most items? |
| 6 | How many orders contained more than 12 items? |

---

### Objective 3 – Analyze Customer Behavior

| # | Question |
|---|----------|
| 1 | Join menu and order tables into a single result set |
| 2 | What were the least and most ordered items, and which categories were they in? |
| 3 | What were the top 5 highest-spending orders? |
| 4 | What did the highest-spend order contain? |
| 5 | What did the top 5 highest-spend orders contain? |

---

## Key Findings

- **Menu size:** 32 items across 4 cuisine categories — American, Asian, Mexican, and Italian
- **Price range:** Items range from **$5.00** (Edamame) to **$19.95** (Shrimp Scampi)
- **Italian is the priciest category** on average; American is the most affordable
- **Date range:** Orders span January 1, 2023 – March 31, 2023 (Q1 2023)
- **Most ordered item:** Hamburger (American)
- **Least ordered item:** Chicken Tacos (Mexican)
- **Largest orders:** Some orders contained up to **14 items**
- **Top spender (Order #440):** Heavily skewed toward Italian dishes, reflecting higher per-item prices

---

## How to Run

### Prerequisites
- MySQL 8.0+ (or compatible)
- A MySQL client (MySQL Workbench, DBeaver, or CLI)

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/reemikadas/restaurant-orders-sql.git
   cd restaurant-orders-sql
   ```

2. **Set up the database**
   ```bash
   mysql -u your_mysql_username -p < create_restaurant_db.sql
   ```
   Replace `your_mysql_username` with your local MySQL username (e.g., `root`). This will create the `restaurant_db` schema, define the tables, and insert all data.

3. **Run the analysis queries**
   ```bash
   mysql -u your_mysql_username -p restaurant_db < Project_1_Restaurants_Orders.sql
   ```
   Or open `Project_1_Restaurants_Orders.sql` in MySQL Workbench and run it section by section.

---

## Tools Used

- **MySQL** – Database creation, data loading, and querying
- **MySQL Workbench** – Query development and execution
- **CSV files** – Raw source data from Maven Analytics

---

## Acknowledgements

Dataset provided by [Maven Analytics](https://mavenanalytics.io/data-playground) as part of their free data playground resources.

---

## 👩‍💻 Author

**Reemika Subrata Das**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-reemikadas-blue?logo=linkedin&style=flat)](https://linkedin.com/in/reemikadas)
[![GitHub](https://img.shields.io/badge/GitHub-reemikadas-black?logo=github&style=flat)](https://github.com/reemikadas)
[![Email](https://img.shields.io/badge/Email-das.reemika%40gmail.com-red?logo=gmail&style=flat)](mailto:das.reemika@gmail.com)
