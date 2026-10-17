# Sample Business Questions

## Purpose

This document demonstrates the types of business questions a Natural Language to SQL Agent could handle using a fictional sales database.

All examples are illustrative. They do not use real company data or a production database.

## 1. Clear Business Questions

| User question | Intended SQL behavior |
|---|---|
| Show sales from Mumbai last month | Filter sales by Mumbai and the previous calendar month |
| Which city generated the highest sales? | Group sales by city, sum the sales amount, and rank the results |
| Count delivered orders by city | Filter for delivered orders and group by city |
| Show the top five products by revenue | Group by product, calculate revenue, and return the five highest |
| What were total sales in January 2026? | Filter records to January 2026 and calculate total sales |

## 2. Ambiguous Questions

### Example A: Missing time period

**User:** Show me sales.

**Expected behavior:** Ask whether the user wants sales for a particular period, or whether all available records should be included.

### Example B: Unclear metric

**User:** Show me the best-performing city.

**Expected behavior:** Ask what "best-performing" means, such as highest sales revenue, highest order count, or highest average order value.

### Example C: Unspecified date range

**User:** Compare sales with the previous period.

**Expected behavior:** Clarify the intended period and comparison basis before generating a query.

## 3. Data Availability

**User:** Show sales for a city that has no matching records.

**Expected behavior:** Return an accurate no-results message if the query succeeds but finds no matching records. Do not invent sales figures.

**User:** Show revenue by a field that is not available in the database.

**Expected behavior:** Explain that the requested field is unavailable and, if possible, suggest a related question that can be answered using available fields.

## 4. Expected Quality Standards

A reliable solution should:

- Interpret the question correctly.
- Use tables and columns that exist in the database.
- Apply the correct filters, aggregations, and date ranges.
- Ask follow-up questions when essential details are missing.
- Distinguish between zero matching records and a query execution error.
- Present results that agree with the database output.
- Never fabricate data.

## Scope

These examples define expected behavior, not verified outputs from a running agent. They should be tested against a synthetic database before being described as successfully implemented.
