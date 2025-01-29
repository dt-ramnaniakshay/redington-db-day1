# create a database online_stores and create customers and orders table

# Table Structure for `customers` and `orders`

## `customers` Table

| **Field Name**  | **Data Type**     | **Description**                                  |
|-----------------|-------------------|--------------------------------------------------|
| `customer_id`   | `SERIAL`          | Unique identifier for each customer. This is the primary key. |
| `first_name`    | `VARCHAR(100)`     | Customer's first name.                           |
| `last_name`     | `VARCHAR(100)`     | Customer's last name.                            |
| `email`         | `VARCHAR(100)`     | Customer's email address.                        |
| `phone`         | `VARCHAR(15)`      | Customer's phone number.                         |

## `orders` Table

| **Field Name**  | **Data Type**     | **Description**                                  |
|-----------------|-------------------|--------------------------------------------------|
| `order_id`      | `SERIAL`          | Unique identifier for each order. This is the primary key. |
| `customer_id`   | `INT`             | The ID of the customer who placed the order. This references the `customer_id` in the `customers` table (foreign key). |
| `order_date`    | `DATE`            | The date when the order was placed.              |
| `total_amount`  | `DECIMAL`         | The total amount for the order.                  |


```sql
CREATE DATABASE online_store;
\c online_store

CREATE TABLE customers (
  customer_id SERIAL PRIMARY KEY,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  email VARCHAR(100)
);

CREATE TABLE orders (
  order_id SERIAL PRIMARY KEY,
  customer_id INT REFERENCES customers(customer_id),
  order_date DATE,
  total_amount DECIMAL
);
```