# GymNation Churn Calculation Methodology

## Overview

This document explains how GymNation calculates customer churn, which measures the rate at which customers stop doing business with the company. Understanding churn is critical for business health and growth planning.

## Key Definitions

**Churn**: The percentage of customers who stop their subscription in a given month, calculated as a combination of payment defaults and subscription cancellations.

**Agreement ID**: A unique identifier for each customer's gym membership contract.

**Transaction Statuses**:
- **Authorised/Accepted**: Successful payment transactions
- **Declined/Error**: Failed payment transactions

## Calculation Process

The churn calculation follows a systematic 6-step process:

### 1. Initial Defaults (ID)
- **Definition**: Customers who paid successfully last month but failed to pay this month
- **Calculation**: Find customers with successful payments in the previous month who have declined/error transactions in the current month
- **Business Impact**: These represent customers at immediate risk of churning due to payment issues

### 2. Within Month Recovery (WMR)
- **Definition**: Customers from the Initial Defaults group who successfully made a payment within the same month
- **Conditions**: 
  - Must have successful transactions in the current month
  - Transaction cannot be classified as "New sales"
  - Customer must not have made any new sales purchases in the past 25 days
- **Business Impact**: These customers recovered from their initial payment failure without intervention

### 3. Prior Month Recovery (PMR)
- **Definition**: Customers from the Initial Defaults group who make successful payments in future months
- **Calculation**: Uses a 4-month forward-looking window to identify customers who eventually pay
- **Business Impact**: These customers eventually recovered, showing they weren't truly churned

### 4. Net Defaults
- **Formula**: Initial Defaults - Within Month Recovery - Prior Month Recovery
- **Definition**: Customers who truly defaulted and didn't recover through any means
- **Business Impact**: These represent genuine payment-related churn

### 5. Cancellations
- **Definition**: Customers who formally cancelled their gym membership agreements
- **Data Source**: Pulled from the cancellations database based on "Agreement Cancelled Date"
- **Business Impact**: These represent voluntary churn decisions

### 6. Final Churn Calculation
- **Formula**: (Net Defaults + Cancellations) / Total Successful Transactions × 100
- **Result**: Percentage representing the monthly churn rate for each store

## Data Processing Features

### Store-Level Analysis
- Calculations are performed separately for each GymNation location
- Store names are cleaned and standardized for consistency
- Regional groupings (UAE vs KSA) are applied for comparative analysis

### Normalization for Recent Data
- Recent months (within 12 weeks) may have incomplete data
- Normalization factors are applied to project final values
- This ensures more accurate reporting for current/recent periods

### Quality Controls
- Invalid Agreement IDs are filtered out
- Duplicate records are removed
- Data validation ensures accuracy across all calculations

## Business Applications

### Monthly Reporting
- Each store receives monthly churn metrics
- Regional comparisons help identify performance patterns
- Historical trends support strategic planning

### Predictive Insights
- Forward-looking PMR calculations help predict true churn
- Early identification of at-risk customers enables intervention
- Recovery tracking measures effectiveness of retention efforts

### Operational Improvements
- Payment failure analysis helps improve billing processes
- Cancellation tracking identifies service improvement opportunities
- Store-specific metrics enable targeted management actions

## Technical Implementation

The calculation process is automated and runs monthly, processing:
- Transaction data from payment systems
- Cancellation records from membership management
- Historical data for trend analysis and normalization

Results are stored in the `churn_historical` database table and made available through business intelligence dashboards for management review.

## Data Accuracy Notes

- **Historical Data**: Calculations become more accurate over time as the 4-month PMR window completes
- **Current Month**: May show higher apparent churn that will be adjusted as recovery data becomes available
- **Normalization**: Recent months use statistical models to project final values based on historical patterns

This methodology provides GymNation with a comprehensive understanding of customer retention patterns, enabling data-driven decisions for business growth and customer satisfaction improvements. 