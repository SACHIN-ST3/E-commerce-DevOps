

# E-Commerce Database Design

## Why Are We Designing the Database First?

Before building APIs, frontend pages, Docker containers, or Kubernetes deployments, we must define how data will be stored.

A database is the foundation of the entire application.

Every feature in the system depends on the database:

* User Registration → Users Table
* Product Listing → Products Table
* Shopping Cart → Cart Table
* Orders → Orders Table
* Payments → Payments Table
* Reviews → Reviews Table

Designing the database first helps:

* Avoid future redesign
* Keep microservices organized
* Create scalable APIs
* Support production deployment on AWS RDS PostgreSQL

---

# 1. Users Table

## Purpose

Stores customer account information.

Every registered user in the platform will have one record in this table.

## Columns

| Column     | Description            |
| ---------- | ---------------------- |
| id         | Unique user identifier |
| full_name  | Customer full name     |
| email      | Login email            |
| password   | Encrypted password     |
| phone      | Mobile number          |
| created_at | Registration date      |

## Example Data

| id | full_name     |
| -- | ------------- |
| 1  | Stephen Kumar |
| 2  | John Smith    |

---

# 2. Addresses Table

## Purpose

Stores delivery addresses.

One user can have multiple addresses.

Example:

* Home
* Office
* Friend's House

## Columns

| Column       | Description    |
| ------------ | -------------- |
| id           | Address ID     |
| user_id      | Owner user     |
| address_line | Street address |
| city         | City           |
| state        | State          |
| country      | Country        |
| postal_code  | ZIP/PIN code   |

## Relationship

One User → Many Addresses

---

# 3. Categories Table

## Purpose

Groups products into categories.

Examples:

* Electronics
* Fashion
* Grocery
* Books

## Columns

| Column        | Description   |
| ------------- | ------------- |
| id            | Category ID   |
| category_name | Category Name |

---

# 4. Brands Table

## Purpose

Stores product brands.

Examples:

* Apple
* Samsung
* Nike
* Adidas

## Columns

| Column     | Description |
| ---------- | ----------- |
| id         | Brand ID    |
| brand_name | Brand Name  |

---

# 5. Products Table

## Purpose

Stores all products displayed on the website.

This is one of the most important tables.

## Columns

| Column       | Description      |
| ------------ | ---------------- |
| id           | Product ID       |
| product_name | Product Name     |
| description  | Product Details  |
| price        | Product Price    |
| category_id  | Product Category |
| brand_id     | Product Brand    |
| image_url    | Product Image    |

## Relationship

One Category → Many Products

One Brand → Many Products

---

# 6. Cart Table

## Purpose

Stores products added to the user's cart.

Example:

User adds:

* iPhone
* Headphones

before checkout.

## Columns

| Column     | Description      |
| ---------- | ---------------- |
| id         | Cart Item ID     |
| user_id    | Owner User       |
| product_id | Selected Product |
| quantity   | Quantity         |

## Relationship

One User → Many Cart Items

---

# 7. Orders Table

## Purpose

Stores customer orders.

Created after successful checkout.

## Columns

| Column       | Description  |
| ------------ | ------------ |
| id           | Order ID     |
| user_id      | Customer     |
| total_amount | Order Total  |
| status       | Order Status |
| created_at   | Order Date   |

## Status Values

* PENDING
* PAID
* SHIPPED
* DELIVERED
* CANCELLED

---

# 8. Order Items Table

## Purpose

Stores individual products inside an order.

Example:

Order #1001

Contains:

* iPhone
* AirPods

Each product becomes an Order Item.

## Columns

| Column     | Description    |
| ---------- | -------------- |
| id         | Item ID        |
| order_id   | Parent Order   |
| product_id | Product        |
| quantity   | Quantity       |
| price      | Purchase Price |

---

# 9. Payments Table

## Purpose

Stores payment transactions.

Tracks whether payment was successful.

Supports gateways like:

* Razorpay
* Stripe

## Columns

| Column         | Description            |
| -------------- | ---------------------- |
| id             | Payment ID             |
| order_id       | Related Order          |
| payment_method | Card/UPI/Wallet        |
| transaction_id | Gateway Transaction ID |
| payment_status | Success/Failed         |

---

# 10. Inventory Table

## Purpose

Tracks available stock.

Prevents overselling products.

Example:

iPhone Stock = 25

If customer buys 1:

Stock becomes 24.

## Columns

| Column         | Description     |
| -------------- | --------------- |
| id             | Inventory ID    |
| product_id     | Product         |
| stock_quantity | Available Stock |

---

# 11. Reviews Table

## Purpose

Stores customer product reviews.

Allows customers to rate products.

## Columns

| Column     | Description |
| ---------- | ----------- |
| id         | Review ID   |
| user_id    | Reviewer    |
| product_id | Product     |
| rating     | 1-5 Stars   |
| comment    | Review Text |

## Example

Rating: 5

Comment:
Excellent product and fast delivery.

---

# Database Relationships Summary

User
├── Addresses
├── Cart
├── Orders
└── Reviews

Orders
└── Order Items

Products
├── Categories
├── Brands
├── Inventory
├── Reviews
└── Cart

Payments
└── Orders

This database structure provides the foundation for all future microservices including User Service, Product Service, Cart Service, Order Service, Payment Service, Inventory Service, and Review Service.
