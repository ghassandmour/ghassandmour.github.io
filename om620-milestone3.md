---
layout: page
title: "OM 620 Tools & Tech for Analytics"
permalink: /om620-milestone3/
---
# Tools and Technologies for Analytics — OM 620

This repository presents my work for OM 620: Tools and Technologies for Analytics, a course in the MS in Supply Chain Analytics program at CSUSM. It includes the combined notebook for 2 assignments, an organized folder structure (data/ and notebooks/), and a summary of the business problem I addressed during the course.

## Business Problem

This project focused on determining appropriate safety stock levels for a group of SKUs using a substantial set of historical transaction data. I evaluated two distinct methods:

* A calculation based on a normal distribution
* An approach that uses empirical quantiles from the actual demand pattern

The aim was not just to compute values, but to understand which method better reflects how demand behaves in practice.

# Data Overview

The dataset includes more than 400,000 transaction records and nearly 500 SKUs. The fields are: sku_number

* inventory_type
* stocking_type
* lead_time
* unit_price
* manufacturing_site
* division_code
* transaction_date
* order_quantity

Before running any analysis, I spent time cleaning the data and ensuring everything was in order. This included fixing inconsistent types, removing irrelevant or non-stocked items, and verifying the accuracy of date and quantity fields.

# Initial Exploration

To focus on items that actually drive inventory decisions, I filtered the dataset to “make to stock” finished goods. From there, I looked at a few basic characteristics:

* How many SKUs remained after filtering
* How many manufacturing sites were represented
* How many divisions appeared in the data

These checks confirmed that the filtered subset still captured a meaningful sample of stocked items.

## Safety Stock Methods

### 1. Normal Distribution Method

This method uses the standard formula:

Safety Stock = Z × (Std Dev of Order Qty) × √(Average Lead Time)

I calculated safety stock at three service levels: 75%, 90%, and 95%. This provided a range of recommendations depending on how much risk the company is willing to take.

### 2. Empirical Quantile Method

The second method uses what the demand data actually looks like:

Safety Stock = Quantile(order quantity at service level) – Average Order Quantity

Since this approach doesn’t assume a particular distribution, it tends to reveal patterns that a normal distribution can obscure.

## Key Findings

The two methods produced noticeably different values for many SKUs. In several cases, the normal distribution method suggested significantly higher safety stock, especially where demand was skewed or irregular.

The empirical method lined up more closely with real-world expectations. Many SKUs in the dataset had lumpy or non-normal demand, and the quantile-based approach captured that behavior more accurately.

Recommendation

For this dataset, the empirical method is the better fit. Demand for many items doesn’t follow a normal curve, and using quantiles leads to safety stock levels that are more closely aligned with what actually occurs in operations.