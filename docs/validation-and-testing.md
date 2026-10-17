# Validation and Testing Strategy

## Objective

Evaluate whether a Natural Language to SQL Agent interprets business questions correctly, generates appropriate queries, and returns answers consistent with the underlying data.

This document describes a proposed testing strategy. Test results should be recorded only after the corresponding tests have been executed.

## Test Scenarios

| Test ID | Scenario | Expected behavior | Status |
|---|---|---|---|
| T01 | Clear question with valid fields | Generate a query using the appropriate fields | Not yet tested |
| T02 | Question requiring aggregation | Apply the correct aggregation and grouping | Not yet tested |
| T03 | Question with a date range | Apply the intended date boundaries | Not yet tested |
| T04 | Ambiguous business terminology | Ask for clarification when needed | Not yet tested |
| T05 | No matching records | Explain that no matching records were found | Not yet tested |
| T06 | Requested field does not exist | Explain the limitation without inventing data | Not yet tested |
| T07 | Invalid SQL or database error | Handle the error without presenting fabricated results | Not yet tested |
| T08 | Destructive SQL operation | Reject the operation under the read-only access policy | Not yet tested |
| T09 | Query result accuracy | Match returned values against independently calculated expected results | Not yet tested |

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
