# DSA3050-PowerBI-SamuelKasusya-668694
# DSA3050 Business Intelligence & Data Visualisation — End Semester Examination

**Name:** Samuel Mwanzia Kasusya  
**Registration Number:** 668694  
**Dataset:** Brazilian E-Commerce Public Dataset by Olist

---

## Section A: Dataset Selection & Understanding

### 1. Dataset Source

Brazilian E-Commerce Public Dataset by Olist, published by Olist on Kaggle.

Source: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Olist is a Brazilian e-commerce platform that connects small and medium sellers to large online marketplaces. The company released this dataset publicly. It covers real orders placed on the platform between September 2016 and October 2018, with customer and seller identifiers anonymised.

### 2. What the Dataset Represents

The dataset contains 99,441 orders spread across nine related CSV files rather than a single flat table. Each file covers a different part of the transaction.

| File | Rows | Columns | Contents |
|---|---|---|---|
| olist_orders_dataset | 99,441 | 8 | One row per order, with status and four timestamps |
| olist_order_items_dataset | 112,650 | 7 | One row per item within an order, with price and freight |
| olist_order_payments_dataset | 103,886 | 5 | Payment method, instalments and value |
| olist_order_reviews_dataset | 99,224 | 7 | Review score and comments per order |
| olist_customers_dataset | 99,441 | 5 | Customer keys, city, state and zip prefix |
| olist_products_dataset | 32,951 | 9 | Category, dimensions and weight |
| olist_sellers_dataset | 3,095 | 4 | Seller location |
| product_category_name_translation | 71 | 2 | Portuguese to English category names |
| olist_geolocation_dataset | 1,000,163 | 5 | Zip prefix coordinates (excluded, see below) |

### 3. Why I Selected It

It is real transactional data released by the company itself, not a simulated or generated file, and the source is verifiable.

It arrives as *9* related tables rather than one flat file, so the data already has a natural fact and dimension structure. This supports proper dimensional modelling instead of forcing a star schema onto a single table.

At 99,441 orders and 112,650 order items it comfortably exceeds the 20,000 record minimum.

The geolocation table was *excluded* from the model. The customers table already carries city and state, which answers the geographic questions, and geolocation adds a million rows with heavy duplication and no analytical gain.

### 4. Main Variables

**Numerical:** price, freight_value, payment_value, payment_installments, review_score, product_weight_g, product dimensions.

**Categorical:** order_status, payment_type, product_category_name, customer_state, customer_city, seller_state.

**Date and time:** order_purchase_timestamp, order_approved_at, order_delivered_carrier_date, order_delivered_customer_date, order_estimated_delivery_date, review_creation_date.

**Keys:** order_id, customer_id, customer_unique_id, product_id, seller_id.

### 5. Business Problem

Olist does not control delivery itself. Orders are fulfilled by independent sellers and shipped through third party carriers, which means delivery performance varies and the platform carries the *reputational* cost when it goes wrong.

This project investigates delivery performance across the platform and whether it affects customer satisfaction. The dataset gives both an estimated delivery date and an actual delivery date for each order, alongside a customer review score, so it is possible to measure how often the platform misses its own delivery promise and then test whether missing it damages the *review score*.

The practical question for management is where to intervene. If late deliveries are concentrated in particular states, categories or sellers, and if lateness measurably lowers review scores, then those are the areas worth fixing first.

### 6. Analytical Questions

1. How have order volume and revenue changed over the period covered, and which product categories contribute most to revenue?
2. Which states account for the most orders and revenue, and how is the customer base distributed geographically?
3. How long do deliveries actually take compared with the estimated delivery date, and what proportion of orders arrive late?
4. Do late deliveries receive lower review scores than on time deliveries?
5. Which product categories and seller states have the worst delivery performance, and how much revenue is
