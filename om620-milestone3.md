---
layout: page
title: "OM 620 Tools & Tech for Analytics"
permalink: /om620-milestone3/
---
# Tools and Technologies for Analytics — OM 620


This repository contains my work for the OM 620 course Tools and Technologies for Analytics, taken as part of the MS in Supply Chain Analytics program at CSUSM. The purpose of this repo is to organize the course assignments, document my analytical approach, and present the insights gathered so far. The repository includes a combined notebook for Milestones 1 and 2, a structured folder layout (data/ and notebooks/), and this README summarizing the core business problem and findings.

## Business Problem Overview

Throughout this assignment, the objective was to help a company determine appropriate safety stock levels for a set of SKUs using a large historical transaction dataset. The task involved computing safety stock using two different methodologies:

A calculation that assumes demand follows a normal distribution

A calculation using empirical quantiles derived directly from the data

The goal was to compare both approaches and assess which method more realistically reflects actual demand behavior.

## Data Description

The dataset provided consisted of detailed transactional records with fields such as:

sku_number

inventory_type

stocking_type

lead_time

unit_price

manufacturing_site

division_code

transaction_date

order_quantity

After initial inspection, the dataset contained over 400,000 transaction rows spanning nearly 500 SKUs. Before analysis, several cleaning steps were required, including:

Ensuring consistent formatting of data types

Addressing missing or inconsistent values

Filtering out irrelevant or non-stocked items

Verifying date and quantity fields for anomalies

## Exploratory Data Review

To prepare for safety stock calculations, I narrowed the dataset to items that are actually intended to be stocked. This included filtering based on criteria such as “make to stock” and “finished goods”.

Some basic exploratory questions helped frame the scope:

How many SKUs are included after filtering?
→ A reduced but meaningful set of stocked SKUs remained for analysis.

How diverse are the manufacturing locations?
→ Multiple sites were represented, illustrating varied production sources.

How many divisions are included?
→ A number of unique divisions operated within the dataset.

These checks ensured the dataset was ready for statistical evaluation.

## Safety Stock Calculations

### 1. Normal Distribution Approach

The first method assumes order quantities are normally distributed. The formula used was:

Safety Stock = Z * (Std Dev of Order Qty) * sqrt(Average Lead Time)


Service level coefficients (Z-values) of 75%, 90%, and 95% were applied to generate safety stock recommendations under different risk tolerances.

### 2. Empirical Quantile Approach

The second method used quantiles from the actual distribution of order quantities. The formula applied was:

Safety Stock = Quantile(order quantity at service level) – Average Order Quantity


This method relies entirely on observed behavior rather than assuming normality.

## Comparison & Key Takeaways

Both methods produced safety stock suggestions, but their results differed noticeably for many SKUs. In several cases, the normal distribution approach recommended higher safety stock, especially when the data showed irregular or skewed demand patterns.

The empirical quantile method tended to produce values that aligned more closely with real-world expectations, particularly for SKUs with sporadic or non-normal demand patterns—which is common in practice.

Recommendation:
Based on the characteristics of the dataset, the empirical approach appears more reliable for this scenario. Real demand rarely fits neatly into a normal distribution, so using quantiles may produce more grounded and actionable safety stock guidelines.