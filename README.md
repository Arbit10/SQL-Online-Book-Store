# 📚 Online Bookstore Database Project (MySQL)

## 📌 Project Overview

This project demonstrates the design, implementation, and querying of an **Online Bookstore Database** using **MySQL**. It covers end-to-end database operations including database creation, table design, CSV data import, data cleaning, and analytical SQL queries.

The project is ideal for showcasing **SQL skills** relevant to roles such as **Data Analyst, Business Analyst, or SQL Developer**.

---

## 🛠️ Tech Stack

* **Database:** MySQL 8.0
* **Tool:** MySQL Workbench
* **Data Source:** CSV files (Books, Customers, Orders)
* **Language:** SQL

---

## 🗂️ Database Schema

### 📘 Books Table

| Column         | Data Type | Description            |
| -------------- | --------- | ---------------------- |
| Book_ID        | INT (PK)  | Unique book identifier |
| Title          | VARCHAR   | Book title             |
| Author         | VARCHAR   | Author name            |
| Genre          | VARCHAR   | Book genre             |
| Published_Year | INT       | Year of publication    |
| Price          | DECIMAL   | Book price             |
| Stock          | INT       | Available stock        |

### 👤 Customers Table

| Column      | Data Type | Description                |
| ----------- | --------- | -------------------------- |
| Customer_ID | INT (PK)  | Unique customer identifier |
| Name        | VARCHAR   | Customer name              |
| Email       | VARCHAR   | Email address              |
| Phone       | VARCHAR   | Contact number             |
| City        | VARCHAR   | City                       |
| Country     | VARCHAR   | Country                    |

### 🧾 Orders Table

| Column       | Data Type | Description             |
| ------------ | --------- | ----------------------- |
| Order_ID     | INT (PK)  | Unique order identifier |
| Customer_ID  | INT (FK)  | References Customers    |
| Book_ID      | INT (FK)  | References Books        |
| Order_Date   | DATE      | Date of order           |
| Quantity     | INT       | Quantity ordered        |
| Total_Amount | DECIMAL   | Order value             |

---

## 📥 Data Import

Data was imported from CSV files using **LOAD DATA INFILE**. Special care was taken to handle:

* Header rows
* Windows line endings (`\r\n`)
* Quoted text values

Example:

```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/Customers.csv'
INTO TABLE Customers
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;
```

---

## 🧹 Data Cleaning

During analysis, hidden carriage return characters (`\r`) were detected in the `country` column after CSV import.

### Fix Applied (Safe Update Mode Compliant):

```sql
UPDATE Customers
SET country = TRIM(REPLACE(country, CHAR(13), ''))
WHERE Customer_ID IN (
    SELECT Customer_ID FROM (
        SELECT Customer_ID FROM Customers WHERE country LIKE '%Canada%'
    ) AS t
);
```

This ensured accurate filtering using equality conditions.

---

## 🔍 Key SQL Queries Implemented

### Basic Queries

* Retrieve books by genre
* Filter books by publication year
* Find customers by country
* Orders placed within a date range
* Total stock and total revenue

### Advanced Queries

* Total books sold per genre
* Average price by genre
* Customers with multiple orders
* Most frequently ordered book
* Top 3 expensive books by genre
* Revenue generated per customer
* Remaining stock after fulfilling orders

---

## 📊 Sample Analytical Query

```sql
SELECT b.genre, SUM(o.quantity) AS total_books_sold
FROM Orders o
JOIN Books b ON o.book_id = b.book_id
GROUP BY b.genre;
```

---

## 🚀 Learning Outcomes

* Practical understanding of **relational database design**
* Hands-on experience with **CSV data ingestion in MySQL**
* Handling real-world **data quality issues**
* Writing optimized **JOIN, GROUP BY, and aggregate queries**
* Understanding **MySQL Safe Update Mode**

---

## 📌 How to Run This Project

1. Clone the repository
2. Open MySQL Workbench
3. Run the schema creation SQL script
4. Place CSV files in the `secure_file_priv` directory
5. Execute `LOAD DATA INFILE` commands
6. Run analysis queries

---

## 📎 Use Cases

* Portfolio project for Data Analyst roles
* SQL practice with realistic business data
* Interview preparation reference

---

## 🙌 Author

**Arbit Saha**
Aspiring Data Analyst

---

## ⭐ If you find this project useful

Give it a ⭐ on GitHub and feel free to fork or suggest improvements!
