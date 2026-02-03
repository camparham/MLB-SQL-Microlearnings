# Competency 1: Data Modeling Before SQL Syntax 

## Purpose 
Data modeling helps you understand how entities relate, which tables should be connected, and how data will behave when queried. Without this foundation, SQL syntax may execute correctly but produce misleading or incorrect results due to flawed logic.

## 🎯 Competency Objectives
By the end of this section, you will be able to:
- Define a relational database
- Identify entities and relationships
- Explain common relationship types
- Understand primary keys and foreign keys
- Describe referential integrity
- Read a basic Entity-Relationship Diagram (ERD)
  
## Competency Outcome
Foundational Data Modeling Thinking

---

## 1️⃣ What Is a Relational Database?
A **relational database** stores data in **tables** that are related to one another.

Each table represents an **entity** — a real-world object such as:
- a customer
- an order
- a product
- an employee

Each entity is unique, and relationships between entities allow us to analyze and understand the data.

---

## 2️⃣ Entities and Relationships
An **entity** is a single object, person, place, or thing stored in a table.

### Example
In a SAAS business:
- Customers place orders
- Orders contain products (software name)
- Products have features
- Salespeople sell orders

These connections form **relationships** between entities.

---

## 3️⃣ Types of Relationships
There are **three main types** of relationships in a relational database.

### 🔹 One-to-One (1:1)
One record in a table is related to one record in another table.

**Example:**
- A customer ↔ a username

---

### 🔹 One-to-Many (1:M)
One record in a table can relate to many records in another table.

**Example:**
- One customer → many orders

---

### 🔹 Many-to-Many (M:M)
Multiple records in one table can relate to multiple records in another table.

**Example:**
- Salespeople ↔ customers

⚠️ Many-to-many relationships require an **intermediary (junction) table** to define the relationship clearly.

---

## 4️⃣ Entity-Relationship Diagrams (ERDs)
An **Entity-Relationship Diagram (ERD)** visually represents:
- entities (tables)
- relationships between entities
- keys connecting tables

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


