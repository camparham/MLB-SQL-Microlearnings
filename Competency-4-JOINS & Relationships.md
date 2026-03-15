# Competency 4: Building Reliable Metrics with Joins (Pre-Multi-Aggregation) 

## Purpose 
Learn how to combine tables safely so your metrics stay trustworthy before you aggregate, summarize, or report.

## 🎯 Competency Objectives
By the end of this section, you will be able to answer questions:
- Translate business questions into multi-table SQL queries (what tables, what keys, what join type)
- Identify the relationship type between tables (1:1, 1:many, many:many) and predict row behavior
- Select the correct join type (INNER, LEFT, FULL, CROSS) based on what must be included/excluded
- Build a debugging mindset: isolate joins, test join keys, and confirm assumptions with small samples
  
## Competency Outcome
Demonstrate the ability to create accurate, non-duplicated business metrics from relational data by:

- Choosing correct join paths and keys
- Preserving the intended grain
- Proving join integrity through row-count and match-rate validation
- Explaining why a join is correct in plain language

---
## 1. What are the most common JOIN paths? 
**Keys** attributes (columns) or sets of attributes used to uniquely identify rows within a table and establish relationships between different tables. There are two different types of keys: **foreign keys**, which are columns that reference a **primary key** in another table. Foreign keys allow tables to be joined together. 

* Using primary and foreign keys, you can:
  * (1)Connect customers to orders; (2) Connect orders to products, and (3) Connect orders to salespeople.
* Primary and foreign keys help you answer:
  * (1) Who placed the order? (2) What did they buy? (3)How many items were ordered? and 4) who sold the order?

- Primary Key Examples: `CustomerID`, `OrderID`, `ProductID`
  * Must be unique
  * Cannot be `NULL`
  * Should not change over time
    
- Foreign Key Examples
  * Order.CustomerID → Customer.CustomerID
  * Order.SalespersonID → Salesperson.SalespersonID

### Example(s):
1. Are ticket sales uniquely identifiable? (i.e., Does each ticket sale have a unique identifier (e.g., sale_id or ticket_id?) **(primary key)**
```
-- Instruction: Select all columns titled ticket_id from the sales table, group by ticket_id, and show me how many there are that are more than one.

SELECT ticket_id, COUNT(*)
FROM workspace.mlb_ticketing.primary_sales
GROUP BY ticket_id
HAVING COUNT(*) > 1;

```
2. Are there duplicate game records? **(foreign key)**

```
-- Instruction: Select all rows with duplicate game records.

SELECT * game_id
FROM workspace.mlb_ticketing.game_metadata
HAVING COUNT(*) > 1;

```

### Explanation/Debug
This query is used to inspect the data and identify shared keys across tables so records can be joined correctly. Validating those relationships helps prevent duplicate revenue reporting, preserve data integrity, and ensure accurate financial reporting and dashboard metrics.

### Business Value Exercise

Instruction: Use workspace.mlb_ticketing.primary_sales 

Question(s): 
1. Are there duplicate game records?
2. Can every ticket be linked to seat information?

---

## 2. How to use JOINS
**JOINS** combines rows from two or more tables, based on a related column. This is how data connects! 


### Examples: 

1. What fields are available from both tables before we start building reports or models, and what primary key can we use to ensure there is a unique identifier to join the two tables?
```
-- Instruction: Select enough columns from club_reports and primary sales tables on the rows where the game ids match.

SELECT *
FROM workspace.mlb_ticketing.club_reports
JOIN workspace.mlb_ticketing.primary_sales
ON club_reports.game_id = primary_sales.game_id
LIMIT 5;
```

2. How many ticket sales are associated with each club’s game?

```
-- Instruction: Select price_face and reported_revenue columns from club reports and primary sales tables on the rows where game ids match.

SELECT club_reports.club_id, club_reports.game_id, COUNT (primary_sales.tickets_id)
FROM workspace.mlb_ticketing. club_reports 
JOIN workspace.mlb_ticketing.primary_sales
ON club_reports.game_id = primary_sales.game_id
AND club_reports.club_id = primary_sales.club_id
GROUP BY club_reports.club_id, club_reports.game_id;

``` 
### Explanation/Debug
Helps verify ticket activity and compare it to tickets_reported. 

### Business Value Exercise 
Instruction: Use workspace.mlb_ticketing.primary_sales and workspace.mlb_ticketing.club_reports
Question(s): 
   1. What seat sections were sold for each game?
   2. What sales channels are used for each game?
   3. What was the price of tickets sold for each game?

### Explanation/Debug
  * Explanation:  
  * Debug: 
---
