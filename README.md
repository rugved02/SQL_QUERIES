# SQL Queries

*This repository contains Simple SQL queries*.  
It demonstrates database creation, table relationships, and commonly used SQL operations such as `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `BETWEEN`, `LIKE`, `IN`, `ORDER BY`, `GROUP BY`, and `UNION`.

*The project is designed for **learning and practice purposes** using MySQL.*
---

## 🗂️ Tables Overview

### 1️⃣ Product Table
Stores information about products available in the store.

**Columns:**
- product_id (Primary Key)
- product_name
- category
- sub_category
- original_price
- selling_price
- stock

---

### 2️⃣ Customer Table
Stores customer details.

**Columns:**
- customer_id (Primary Key)
- name
- city
- email
- phone_no
- address
- pin_code

---

### 3️⃣ Order_Details Table
Stores order and purchase information.

**Columns:**
- order_id (Primary Key, Auto Increment)
- customer_id (Foreign Key)
- product_id (Foreign Key)
- quantity
- total_price
- payment_mode
- order_date
- order_status

---

## 📌 Database Used

```sql
CREATE DATABASE ecommerce;
USE ecommerce;
```

---

## 📦 Table Creation Queries

### Product Table

```sql
CREATE TABLE product (
  product_id VARCHAR(10) NOT NULL PRIMARY KEY,
  product_name VARCHAR(100) NOT NULL,
  category VARCHAR(65) NOT NULL,
  sub_category VARCHAR(45) NOT NULL,
  original_price DOUBLE NOT NULL,
  selling_price DOUBLE NOT NULL,
  stock INT NOT NULL
);
```

### Customer Table

```sql
CREATE TABLE customer (
  customer_id VARCHAR(10) NOT NULL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  city VARCHAR(65) NOT NULL,
  email VARCHAR(45) NOT NULL,
  phone_no VARCHAR(15) NOT NULL,
  address VARCHAR(100) NOT NULL,
  pin_code INT NOT NULL
);
```

### Order Details Table

```sql
CREATE TABLE order_details (
  order_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  customer_id VARCHAR(10) NOT NULL,
  product_id VARCHAR(10) NOT NULL,
  quantity DOUBLE NOT NULL,
  total_price DOUBLE NOT NULL,
  payment_mode VARCHAR(60) NOT NULL,
  order_date DATETIME NOT NULL,
  order_status VARCHAR(20) NOT NULL,
  FOREIGN KEY (customer_id) REFERENCES customer(customer_id),
  FOREIGN KEY (product_id) REFERENCES product(product_id)
);
```

---

## 🧾 Insert Queries

### Insert into Product

```sql
INSERT INTO product VALUES
('P101','Television','Electronics','Phone',70000,55000,100),
('P102','Chair','Furniture','Chairs',20000,15000,10);
```

### Insert into Customer

```sql
INSERT INTO customer VALUES
('C1001','Steve','Tokyo','steve@gmail.com','4567897652','f.g.road',1000001),
('C1002','John','Sydney','john@gmail.com','9987234567','k.c.road',75001);
```

### Insert into Order Details

```sql
INSERT INTO order_details
(customer_id, product_id, quantity, total_price, payment_mode, order_date, order_status)
VALUES
('C1002','P101',1,55000,'COD','2023-11-19','Shipped'),
('C1001','P101',1,55000,'COD','2023-10-30','Delivered');
```

---

## 🔍 Select Queries

```sql
SELECT * FROM customer;
SELECT product_name, category, sub_category FROM product;
SELECT * FROM product;
SELECT * FROM customer WHERE name LIKE '%er';
SELECT * FROM customer WHERE email LIKE '%example%';
SELECT * FROM customer WHERE name LIKE 'J___';
```

---

## ✏️ Update & ❌ Delete Queries

```sql
UPDATE customer SET email='johndoe@example.com' WHERE customer_id='C1002';
UPDATE customer SET email='peter.parker@mail.com' WHERE customer_id='C1003';
DELETE FROM customer WHERE customer_id='C1007';
```

---

## 📊 BETWEEN Operator

```sql
SELECT * FROM product WHERE original_price BETWEEN 1000 AND 20000;
SELECT * FROM order_details WHERE order_date BETWEEN '2023-11-19' AND '2023-11-30';
SELECT * FROM product WHERE original_price NOT BETWEEN 1000 AND 20000;
SELECT * FROM product WHERE product_name BETWEEN 'A' AND 'P';
```

---

## 🔎 LIKE Operator

```sql
SELECT * FROM customer WHERE name LIKE 'J%';
SELECT * FROM customer WHERE name LIKE 'j___';
SELECT * FROM product WHERE product_name LIKE '%o_';
```

---

## 📥 IN / NOT IN Queries

```sql
SELECT * FROM customer WHERE customer_id IN ('C1001','C1003','C1005');
SELECT * FROM order_details WHERE customer_id IN (SELECT customer_id FROM customer WHERE city='Sydney');
SELECT * FROM product WHERE category IN ('Electronics','Furnitures');
SELECT * FROM product WHERE product_id NOT IN ('P102','P104');
```

---

## 🚫 NULL Checks

```sql
SELECT name, email, address FROM customer WHERE name IS NULL;
SELECT name, email, address FROM customer WHERE name IS NOT NULL;
```

---

## 🔃 ORDER BY Queries

```sql
SELECT * FROM customer ORDER BY name;
SELECT * FROM order_details ORDER BY order_date;
SELECT * FROM product ORDER BY original_price DESC;
```

---

## 📈 GROUP BY Query

```sql
SELECT order_status AS 'Delivery Status', COUNT(*) AS Total
FROM order_details
GROUP BY order_status;
```

---

## 🔀 UNION Queries

```sql
SELECT product_id FROM product
UNION
SELECT product_id FROM order_details;
```

---

## 🔁 INTERSECT Query

```sql
SELECT product_id FROM product
WHERE product_id IN (SELECT product_id FROM order_details);
```

---

## ➖ EXCEPT Query

```sql
SELECT * FROM product
WHERE product_id NOT IN (SELECT product_id FROM order_details);
```

---
