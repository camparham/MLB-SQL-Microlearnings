# Competency 3: Building Reliable Metrics with Joins (Pre-Multi-Aggregation) 

## Purpose 
Learn how to combine tables safely so your metrics stay trustworthy before you aggregate, summarize, or report.

## 🎯 Competency Objectives
By the end of this section, you will be able to answer questions:
- Translate business questions into multi-table SQL queries (what tables, what keys, what join type)
- Identify the relationship type between tables (1:1, 1:many, many:many) and predict row behavior
- Select the correct join type (INNER, LEFT, FULL, CROSS) based on what must be included/excluded
- Validate join correctness with row count checks and “coverage” checks (what % of records matched)
- Prevent row multiplication and grain mismatch that silently breaks metrics (double counting, inflated revenue)
- Build a debugging mindset: isolate joins, test join keys, and confirm assumptions with small samples
  
## Competency Outcome
Demonstrate the ability to create accurate, non-duplicated business metrics from relational data by:

- Choosing correct join paths and keys
- Preserving the intended grain
- Proving join integrity through row-count and match-rate validation
- Explaining why a join is correct in plain language

---
## 1. What are Keys?
**Keys** attributes (columns) or sets of attributes used to uniquely identify rows within a table and establish relationships between different tables. There are two different types of keys: **foreign keys**, which are columns that reference a **primary key** in another table. Foreign keys allow tables to be joined together. 

Using primary and foreign keys, you can (1)connect customers to orders; (2) connect orders to products, and (3) connect orders to salespeople. Primary and foreign keys help you answer: (1)who placed the order?; (2) what did they buy?; (3)How many items were ordered?; and 4) who sold the order?

- Primary Key Examples: `CustomerID`, `OrderID`, `ProductID`
  * Must be unique
  * Cannot be `NULL`
  * Should not change over time
    
- Foreign Key Examples
  * Order.CustomerID → Customer.CustomerID
  * Order.SalespersonID → Salesperson.SalespersonID

### Example(s):
1. Are ticket sales uniquely identifiable?
2. Are there duplicate game records?

### Explanation/Debug
This helps you get preliminary information about the data so you can see which tables have data commonality in order to join tables on the same row. 


### Business Value Exercise 
1. Are there duplicate game records?
2. Can every ticket be linked to seat information?

---

## 2. How to use JOINS
**JOINS** combines rows from two or more tables, based on a related column. This is how data connects! 


### Examples: 

1. What fields are available from both tables before we start building reports or models?
```
-- Instruction: Select all columns from club reports and primary sales tables on the rows where the game ids match.

SELECT *
FROM workspace.mlb_ticketing.club_reports 
JOIN workspace.mlb_ticketing.primary_sales 
on club_reports.game_id = primary_sales.game_id;

```

2. What game_id data is available for price_face and reported_revenue before we start building reports or models?
```
-- Instruction: Select price_face and reported_revenue columns from club reports and primary sales tables on the rows where game ids match.

SELECT primary_sales.price_face, club_reports.reported_revenue, primary_sales.game_id
FROM workspace.mlb_ticketing.primary_sales
JOIN workspace.mlb_ticketing. club_reports
on club_reports.game_id = primary_sales.game_id;
``` 

### Business Value Exercise 
Instruction: Use workspace.mlb_ticketing.primary_sales 
Question(s): 
   1. How do ticket sales compare to club performance metrics?
   2. What is the total ticket revenue by club?
   3. Are clubs on track to meet attendance goals?

### Explanation/Debug
  * Explanation:  
  * Debug: 
---
