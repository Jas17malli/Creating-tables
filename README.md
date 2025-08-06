# Creating-tables

CREATE TABLE Customer (
  customer_id   INT PRIMARY KEY,
  name          VARCHAR(255) NOT NULL,
  email         VARCHAR(255) UNIQUE NOT NULL
);

CREATE TABLE Product (
  product_id    INT PRIMARY KEY,
  name          VARCHAR(255) NOT NULL,
  price         DECIMAL(10,2) NOT NULL
);

CREATE TABLE Order (
  order_id      INT PRIMARY KEY,
  customer_id   INT NOT NULL REFERENCES Customer(customer_id),
  order_date    DATE NOT NULL,
  total_amount  DECIMAL(10,2) NOT NULL
);

-- Join table to link products to orders
CREATE TABLE OrderItem (
  order_id      INT NOT NULL REFERENCES "Order"(order_id),
  product_id    INT NOT NULL REFERENCES Product(product_id),
  quantity      INT NOT NULL CHECK (quantity > 0),
  unit_price    DECIMAL(10,2) NOT NULL,
  PRIMARY KEY (order_id, product_id)
);
