# Competency 2: Reading Data (Pre-Manipulation) 

## Purpose 
Learn how to read data before manipulating it.

## 🎯 Competency Objectives
By the end of this section, you will be able to answer questions:
- Translate business questions into SQL queries
- Identify the correct grain before aggregating
- Avoid double-counting when summing revenue
- Reflect on where you get stuck and why (debugging mindset)
  
## Competency Outcome
Demonstrate the ability to construct trustworthy business metrics from raw transactional data using SQL aggregations, grouping logic, and grain validation.

---

## 1️⃣ How to use SELECT 
A **SELECT** statement is the core SQL command used to retrieve data from a database

## Examples: 

1. What fields are available before we start building reports or models?
   SELECT * FROM workspace.default.mlb_active_rosters_new;
   * --  i.e., Give me all the rows in columns in this database/table.
     
2. Who is currently on the active roster?
   SELECT player_name FROM workspace.default.mlb_active_rosters_new;
   * -- i.e., Select the column you want to pull from this table
     
3. What jersey number corresponds to each player?
SELECT player_name, jersey_number FROM workspace.default.mlb_active_rosters_new;
   * -- i.e., Select data from two columns


### Explanation/Debug
  * Explanation: This helps teams audit roster data before building reports or making staffing decisions. Each grain is identified by club_id. 
  * Debug: The numeric values are not the same data.
         
### Business Value Exercise 
Instruction: Use workspace.mlb_ticketing.primary_sales 
Question(s): 
   1. What fields are available before we start building reports or models?
   2. Can we analyze revenue patterns by channel?
   3. What is the sum of each game by channel? 
      
### Explanation/Debug
  * Explanation:  
  * Debug: 

---

## 2️⃣ How to use WHERE
**WHERE** is a clause for filtering, i.e., it decides which rows, columns, and data values stay in your result set.  

### Examples: 
1. What data is related to Alek Thomas? 
   SELECT * FROM workspace.default.mlb_active_rosters_new WHERE player_name = "Alek Thomas";
   * -- i.e., Give me the row with Alek Thomas 
2. Who's on the Arizona Diamondbacks team? 
   SELECT * FROM workspace.default.mlb_active_rosters_new WHERE team_name = "Arizona Diamondbacks";
   * -- i.e, Give me the rows with Arizona Diamondbacks

### Business Value Exercise 
Instruction: Use workspace.mlb_ticketing.primary_sales 
Question(s): 
   1. What data is associated with Club_06? 
   2. How many tickets were for the lower seat_section? 

### Explanation/Debug
  * Explanation:  
  * Debug: 

---

## 3️⃣ IS
**IS** is an operator, most commonly used to test for NULL and boolean values (true/false). 

### Examples: 
1. Who does not have a jersey number? 
   SELECT * FROM workspace.default.mlb_active_rosters_new WHERE jersey_number IS null;
 * --i.e., Give me the nulls from this specific column

### Business Value Exercise 
Instruction: Use workspace.mlb_ticketing.primary_sales 
Question(s): 
   1. How many people didn't pay for a ticket? 


### Explanation/Debug
  * Explanation:  
  * Debug: 


---

## 4️⃣ How to use JOINS
**JOINS** combines rows from two or more tables, based on a related column.

### Examples: 

1. SELECT *
FROM workspace.mlb_ticketing.club_reports 
JOIN workspace.mlb_ticketing.primary_sales 
on club_reports.game_id = primary_sales.game_id;
 -- Select all columns from club reports and primary sales tables on the rows where the game ids match

ERDs provide a high-level view of the database structure and available data.

---

## 5️⃣ Primary Keys
A **primary key** uniquely identifies each record in a table.

### Rules for Primary Keys:
- Must be unique
- Cannot be `NULL`
- Should not change over time

### Examples:
- `CustomerID`
- `OrderID`
- `ProductID`

### Composite Keys
A **composite key** uses multiple columns to uniquely identify a record.

⚠️ Poor choices (like first name + last name) can cause issues if duplicates exist.

---

## 6️⃣ Foreign Keys
A **foreign key** is a column that references a **primary key** in another table.

### Examples:
- `Order.CustomerID` → `Customer.CustomerID`
- `Order.SalespersonID` → `Salesperson.SalespersonID`

Foreign keys allow tables to be joined together.

---

## 7️⃣ Joining Tables (How Data Connects)
Using primary and foreign keys, you can:
- connect customers to orders
- connect orders to products
- connect orders to salespeople

This enables questions like:
> Who placed the order?  
> What did they buy?  
> How many items were ordered?  
> Who sold the order?

---

## 8️⃣ Referential Integrity
**Referential integrity** ensures that:
- every foreign key references an existing primary key
- relationships between tables remain valid

### Why It Matters:
- prevents broken references
- maintains data accuracy and consistency

Database constraints enforce referential integrity.

---

## ✅ Key Takeaways
- Relational databases store data in connected tables
- Entities represent real-world objects
- Relationships define how entities connect
- ERDs visualize database structure
- Primary keys uniquely identify records
- Foreign keys connect tables
- Referential integrity keeps data reliable
