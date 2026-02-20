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
**JOINS** combines rows from two or more tables, based on a related column. This is how data connects! 

This enables questions like:
> Who placed the order?  
> What did they buy?  
> How many items were ordered?  
> Who sold the order?
They join on **foreign keys**, which are columns that reference a **primary key** in another table. Foreign keys allow tables to be joined together.
**Primary keys** uniquely identify each record in a table.


### Keys:
- Primary Key Examples: `CustomerID`, `OrderID`, `ProductID`
* Must be unique
* Cannot be `NULL`
* Should not change over time
- Foreign Key Examples
* Order.CustomerID → Customer.CustomerID
* Order.SalespersonID → Salesperson.SalespersonID

### Keys Summary:
Using primary and foreign keys, you can:
- connect customers to orders
- connect orders to products
- connect orders to salespeople
Example questions: This enables questions like:
> Who placed the order?  
> What did they buy?  
> How many items were ordered?  
> Who sold the order?

### Examples: 

1. What fields are available from both tables before we start building reports or models?
  SELECT *
  FROM workspace.mlb_ticketing.club_reports 
  JOIN workspace.mlb_ticketing.primary_sales 
  on club_reports.game_id = primary_sales.game_id;
 * -- Select all columns from club reports and primary sales tables on the rows where the game ids match

2. What game_id data is available for price_face and reported_revenue before we start building reports or models?
  SELECT primary_sales.price_face, club_reports.reported_revenue, primary_sales.game_id
  FROM workspace.mlb_ticketing.primary_sales 
  JOIN workspace.mlb_ticketing. club_reports
  on club_reports.game_id = primary_sales.game_id;
* -- Select price_face and reported_revenue columns from club reports and primary sales tables on the rows where game ids match

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

## 5️⃣ SUM
**SUM** adds up numeric values across rows, i.e., add all these numbers together. To use SUM, you have to use GROUP BY. 
**GROUP BY** is a clause used to group rows that have the same values in specified columns into summary rows. 
**ORDER BY** sorts your query results.
**DISTINCT** identifies the unique values in a column; it removes duplicate rows so each value appears only once.
**DESC** orders results from highest to lowest. 
**ASC** orders results from lowest to highest. 
**MAX**

### Examples: 
1. What is the revenue per channel per game, i.e., for each game, we'll need how much revenue was generated from each channel?
-- Step 1: Select 5 records to understand the data schema 
SELECT * FROM workspace.mlb_ticketing.primary_sales 
LIMIT 5;

-- Step 2: Choose the columns that need to be analyzed 
SELECT primary_sales.channel, primary_sales.game_id, primary_sales.price_face
FROM workspace.mlb_ticketing.primary_sales;

--Step 3: Add the total price for each game_id by channel 
SELECT SUM(price_face), primary_sales.channel, primary_sales.game_id
FROM workspace.mlb_ticketing.primary_sales
GROUP BY channel, game_id;

2.  What game brought in the most money?
-- Step 1: Analyze 20 records to understand the data schema 
SELECT * FROM workspace.mlb_ticketing.primary_sales 
LIMIT 20;

-- Step 2: Sum by channel descending to get the most lucrative 
SELECT SUM(price_face), primary_sales.channel
FROM workspace.mlb_ticketing.primary_sales
GROUP BY channel
ORDER BY SUM(price_face) DESC;

3. Which clubs are represented in this dataset? I don't need to see the duplicate date
SELECT DISTINCT club_id FROM workspace.mlb_ticketing.primary_sales;
--Select the unique values in the club_id column

4. What is the earliest and latest ticket sold?
--Latest
SELECT primary_sales.sale_datetime, primary_sales.ticket_id
FROM workspace.mlb_ticketing.primary_sales
ORDER BY sale_datetime DESC LIMIT 1;

**or** 

SELECT MAX(primary_sales.sale_datetime)
FROM workspace.mlb_ticketing.primary_sales;

-- Earliest 
SELECT primary_sales.sale_datetime, primary_sales.ticket_id
FROM workspace.mlb_ticketing.primary_sales
ORDER BY sale_datetime ASC LIMIT 1;
 
**or**

SELECT MIN(primary_sales.sale_datetime)
FROM workspace.mlb_ticketing.primary_sales;

### Business Value Exercise 
Instruction: Use workspace.mlb_ticketing.primary_sales 
Question(s): 
   1. Which teams drive the most ticket revenue?
   2. Where are we seeing premium demand?

### Explanation/Debug
  * Explanation:  
  * Debug: 


---

## 8️⃣ COUNT
**COUNT** is used to measure volume. 
**AVG** calculates the mean value of a numeric column. It is used to determine central tendency. 
**AS** helps you change the name of the columns so stakeholders have better insight. You'll have to define this in the first line with SELECT or it will not work. 

### Examples: 
1. What is the count for distinct ticket_id values? 
SELECT COUNT(DISTINCT ticket_id)
FROM workspace.mlb_ticketing.primary_sales;

2. What is the average ticket purchase? 
SELECT AVG(primary_sales.price_face) AS average_ticket_price
FROM workspace.mlb_ticketing.primary_sales;

### Business Value Exercise 
Instruction: Use workspace.mlb_ticketing.primary_sales 
Question(s): 
   1. How many tickets were sold in total?
   2. Are sales increasing or decreasing over time?
   3. What is the typical ticket price?
   4. Are customers paying more or less over time?

### Explanation/Debug
  * Explanation:  
  * Debug: 

---

## ✅ Key Takeaways
- Learned how to explore and understand datasets using SELECT, filtering, and sorting to ask meaningful questions before analysis.

- Built the ability to define and calculate core metrics (COUNT, SUM, AVG, MIN, MAX) that translate raw data into business insights.

- Understood how GROUP BY sets the level of analysis and why grain awareness is critical to avoid double-counting.

- Developed habits for validating results, including distinguishing WHERE vs HAVING and checking assumptions.

- Strengthened the mindset of connecting SQL to business decisions, turning queries into clear, interpretable insights for stakeholders.
