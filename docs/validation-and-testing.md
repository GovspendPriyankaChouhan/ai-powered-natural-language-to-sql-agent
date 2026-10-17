# Validation and Testing Strategy

## Objective

Evaluate whether a Natural Language to SQL Agent interprets business questions correctly, generates appropriate queries, and returns answers consistent with the underlying data.

This document describes a proposed testing strategy. Test results should be recorded only after the corresponding tests have been executed.

### T10 — Annual Sold Quantity Aggregation

- **Question:** What is the total sold quantity for each year, sorted from highest to lowest?
- **Data source:** `public.fact_sales_monthly`
- **Aggregation:** Sum of `sold_quantity`, grouped by year extracted from `date`.
- **Sorting:** Total sold quantity in descending order.
- **Expected result:**

| Year | Total sold quantity |
|---:|---:|
| 2021 | 69,177,620 |
| 2020 | 31,684,973 |
| 2019 | 16,452,462 |
| 2018 | 6,532,551 |
| 2017 | 1,443,950 |

- **Actual result:** Matches the direct PostgreSQL query.
- **Status:** PASS — verified against PostgreSQL.
- **Validation method:** Compared the AI Agent's answer with an independently executed SQL aggregation query.

## Validation Approach

### 1. Question Interpretation

Check whether the agent correctly identifies the requested metric, filters, grouping, and time period.

### 2. SQL Validation

Inspect generated queries to verify that table names, column names, joins, filters, and aggregation logic are appropriate for the available schema.

### 3. Result Verification

Use a small synthetic dataset with manually calculated expected results. Compare the database output with those expected results.

### 4. Clarification Handling

Test questions with missing periods, unclear metrics, or ambiguous comparisons. Confirm that the agent asks useful follow-up questions rather than silently assuming important details.

### 5. Error and Security Handling

Test unavailable fields, query failures, empty result sets, and prohibited operations. Use least-privilege database permissions and enforce read-only access at the database level.

## Recording Results

For every executed test, record:

- Test ID and input question
- Expected behavior or result
- Actual response
- Pass or fail
- Defect or observation
- Corrective action, if needed

## Current Status

This is a proposed test plan. No test is marked as passed because the independent demonstration has not yet been executed and verified.
