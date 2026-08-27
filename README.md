# Broadband-Recharge📡 Broadband Database — SQL Data Analysis Project

# 📌 Project Overview

Broadband Database is a MySQL-based database project designed to manage and analyze broadband/internet service provider data.

The project stores information about:

  Customers
  Broadband plans
  Customer accounts/users
  Internet usage
  Payments and transactions
  Password reset requests
  Renewal alerts

The main purpose of this project is to practice SQL database design, relationships, data retrieval, aggregation, joins, subqueries, and advanced data analysis using a realistic broadband-service scenario.

# 🎯 Objectives

The project focuses on:

  Designing a relational database using MySQL.
  Creating multiple related tables.
  Establishing Primary Key and Foreign Key relationships.
  Inserting realistic broadband customer data.
  Retrieving and filtering data using SQL.
  Performing customer and revenue analysis.
  Analyzing internet usage.
  Analyzing successful and failed payments.
  Practicing JOIN, GROUP BY, HAVING, and subqueries.  
  Applying advanced SQL concepts such as CTEs and Window Functions.

# 🗄️ Database Structure

Database name: broadband_db
  
The project contains 7 tables:

Table:      Purpose

plans       : Stores broadband plan information
customers   : Stores customer information
users       : Stores login/user information
usage_logs  : Stores customer data consumption
transactions : Stores payment transactions
password_resets : Stores password reset information
renewal_alert_logs :Stores renewal notification records

# 🔗 Database Relationships

                    ┌──────────────┐
                    │    plans     │
                    └──────┬───────┘
                           │
                       plan_id
                           │
                    ┌──────▼───────┐
                    │  customers   │
                    └──┬───┬───┬───┘
                       │   │   │
             ┌─────────┘   │   └──────────┐
             │             │              │
             ▼             ▼              ▼
       ┌──────────┐  ┌────────────┐  ┌──────────────────┐
       │  users   │  │usage_logs  │  │renewal_alert_logs│
       └──────────┘  └────────────┘  └──────────────────┘
             │
             │
             ▼
       ┌──────────────┐
       │transactions  │
       └──────┬───────┘
              │
              ▼
            plans

# Primary relationships
1.
customers.plan_id
          ↓
plans.id
2.
users.customer_id
        ↓
customers.id
3.
usage_logs.customer_id
        ↓
customers.id
4.
transactions.customer_id
        ↓
customers.id
5.
transactions.plan_id
        ↓
plans.id
6.
renewal_alert_logs.customer_id
        ↓
customers.id

# 🛠️ Technologies Used

Database: MySQL
Language: SQL
Tool: MySQL Workbench / MySQL CLI
Database Type: Relational Database

# 📂 Table Details

1. plans-Stores available broadband plans.
Important columns:
id
name
speed
data_limit
data_limit_gb
validity_days
price

Example plans include:

Home Basic
Home Plus
Home Pro Unlimited
Home Gamer Ultra
Home Starter

2. customers-Stores broadband customer details.

Important columns:

id
name
connection_id
email
address
plan_id
start_date
due_date
followed_up

plan_id connects each customer to a broadband plan.

3. users-Stores system users and customer login information.

Important columns:

id
username
password_hash
role
display_name
email
customer_id

Different roles include:

admin
staff
customer

4. usage_logs-Stores customer internet usage.

Important columns:

id
customer_id
date
data_consumed

This table can be used to calculate:

Total data consumption
Average usage
Maximum usage
Minimum usage
Usage by customer

5. transactions-Stores payment information.

Important columns:

id
customer_id
plan_id
amount
payment_mode
date
status

Payment modes include:

UPI
Card
Net Banking

Transaction statuses include:

Success
Failed

6. password_resets-Stores password reset information.

Columns include:

id
email
otp
created_at
expires_at

7. renewal_alert_logs-Stores renewal alert information.

Columns include:

id
customer_id
due_date
alert_type
sent_at

# 📊 SQL Analysis Performed

The project contains 100 SQL practice and analysis queries divided into three levels.

# 🟢 Simple Queries

Basic SQL operations:

SELECT
WHERE
LIKE
BETWEEN
ORDER BY
LIMIT
COUNT()
SUM()
AVG()
MIN()
MAX()

Example:

SELECT
    name,
    email
FROM customers;

Another example:

SELECT
    name,
    price
FROM plans
WHERE price > 500;

# 🟡 Medium Queries

Intermediate relational analysis using:

INNER JOIN
LEFT JOIN
GROUP BY
HAVING
Aggregate functions
Subqueries
Multiple-table relationships

Example:

SELECT
    c.name AS customer_name,
    p.name AS plan_name,
    p.price
FROM customers c
JOIN plans p
    ON c.plan_id = p.id;

Another example:

SELECT
    c.name,
    SUM(t.amount) AS total_revenue
FROM customers c
JOIN transactions t
    ON c.id = t.customer_id
WHERE t.status = 'Success'
GROUP BY c.id, c.name;

# 🔴 Hard Queries

Advanced SQL analysis using:

Nested subqueries
CTEs
CASE
Window functions
RANK()
PARTITION BY
Complex aggregations
Business intelligence queries

Example:

SELECT
    customer_name,
    total_revenue,
    RANK() OVER (
        ORDER BY total_revenue DESC
    ) AS revenue_rank
FROM (
    SELECT
        c.name AS customer_name,
        SUM(t.amount) AS total_revenue
    FROM customers c
    JOIN transactions t
        ON c.id = t.customer_id
    WHERE t.status = 'Success'
    GROUP BY c.id, c.name
) x;

# 💼 Business Questions Answered

The SQL analysis can answer questions such as:
Which customer generates the highest revenue?
Which broadband plan is most popular?
Which plan generates the highest revenue?
Which customers have failed payments?
Which customers consume the most data?
Which customers have no transactions?
Which payment mode is used most frequently?
What is the monthly revenue?
Which customers consume more than 80% of their plan limit?
Which customers use multiple payment methods?
Which plan has no customers?
Who are the highest-revenue customers within each plan?
Which customers need renewal soon?

# 📈 Key SQL Concepts Demonstrated

Basic SQL

SELECT
WHERE
ORDER BY
LIMIT
LIKE
BETWEEN

Aggregation

COUNT()
SUM()
AVG()
MIN()
MAX()

Relational Operations

INNER JOIN
LEFT JOIN
GROUP BY
HAVING

Advanced SQL

Subqueries
CTE
CASE
RANK()
PARTITION BY
Window Functions

# 🚀 How to Run the Project

Step 1 — Install MySQL

Install:
MySQL Server

MySQL Workbench

Step 2 — Open MySQL Workbench

Create a new SQL tab.

Step 3 — Run the database creation script

Execute:

DROP DATABASE IF EXISTS broadband_db;

CREATE DATABASE broadband_db;

USE broadband_db;

Step 4 — Create the tables

Execute the CREATE TABLE statements in dependency order:

plans
  ↓
customers
  ↓
users
  ↓
usage_logs
  ↓
transactions
  ↓
password_resets
  ↓
renewal_alert_logs

Step 5 — Insert the data

Run the corresponding INSERT INTO statements.

Step 6 — Verify the database

USE broadband_db;

SHOW TABLES;

Step 7 — View the data

SELECT * FROM plans;

SELECT * FROM customers;

SELECT * FROM users;

SELECT * FROM usage_logs;

SELECT * FROM transactions;

SELECT * FROM password_resets;

SELECT * FROM renewal_alert_logs;

Step 8 — Run the 100 analysis queries

Execute the queries progressively:

Simple   → 1–35
Medium   → 36–70
Hard     → 71–100

# 📁 Suggested GitHub Structure

broadband-database-sql/
│
├── README.md
│
├── 01_database_setup.sql
├── 02_table_creation.sql
├── 03_data_insertion.sql
├── 04_simple_queries.sql
├── 05_medium_queries.sql
└── 06_hard_queries.sql

Or, for a simpler repository:

broadband-database-sql/
│
├── README.md
└── broadband_db.sql

# 🎓 Learning Outcomes

After completing this project, the major skills practiced are:

Relational database design
Primary and foreign keys
One-to-many relationships
SQL CRUD fundamentals
Filtering and sorting
Aggregate functions
Table joins
Grouped analysis
Subqueries
CTEs
Window functions
Revenue analysis
Customer analysis
Usage analysis
Payment analysis
Business-oriented SQL problem solving

# 🔮 Possible Future Improvements

The database could be extended with:

Support tickets — track customer complaints.
Service outages — analyze downtime by customer/area.
Employee table — manage staff separately.
Plan upgrade history — track customers changing plans.
Monthly billing table — maintain generated invoices.
Location/area table — analyze customers geographically.

# 👨‍💻 Project Summary

Broadband Database SQL Project is a relational MySQL project that models a broadband service provider and provides a practical environment for SQL analysis.

It combines customer management, broadband plans, usage tracking, payment transactions, user management, password resets, and renewal alerts into a connected relational database.

The project progresses from basic SQL queries to advanced analytical queries, making it suitable for practicing SQL for Data Analyst, Python Full-Stack, and database-focused interviews.

# ⭐ Skills Demonstrated

MySQL
SQL
Database Design
Primary & Foreign Keys
Joins
Aggregation
Subqueries
CTEs
Window Functions
Data Analysis
Business Intelligence
Relational Database Management

Project: Broadband Database SQL Data Analysis
Database: broadband_db
Tables: 7
Analysis Queries: 100
Difficulty Levels: Simple → Medium → Hard
