# 📂 Datasets: MLB SQL Microlearning Course

This folder contains datasets used throughout the competency-based SQL microlearning curriculum.

All datasets are derived from real-world Major League Baseball (MLB) data and are structured to support beginner-friendly SQL exercises.

---

## 📊 Available Datasets

---

### 1. MLB Active Roster

**File:** [`mlb_active_roster.csv`](https://docs.google.com/spreadsheets/d/1Vg0cYQLL16h6lFBeq331NxvUnMrZf-aue75I1tzOXmA/edit?usp=sharing)

**Description:**  
Contains a snapshot of active MLB players across teams. Used to practice foundational SQL concepts like selecting, filtering, and understanding dataset structure.

**Common Use Cases:**
- Identify players on active rosters  
- Explore available fields before analysis  
- Practice basic `SELECT` queries  

**Example Query:**
```sql
SELECT player_name, team
FROM mlb_active_roster;
```
---

**### 2. MLB Ticket Sales**

**File:** [`primary_sales.csv`](https://docs.google.com/spreadsheets/d/1Vg0cYQLL16h6lFBeq331NxvUnMrZf-aue75I1tzOXmA/edit?gid=1770571503#gid=1770571503)

****Description:** ** 
Represents ticket sales data at the transaction level. Used to practice SQL concepts like filtering, aggregation, and understanding data grain.

****Common Use Cases:****
- Count tickets sold per game  
- Analyze ticket pricing  
- Calculate total and average revenue  
- Understand transactional-level data  

****Example Query:****
```sql
SELECT game_id, COUNT(ticket_id) AS tickets_sold
FROM primary_sales
GROUP BY game_id;
```
---

### 3. MLB Game Metadata

**File:** [`game_metadata.csv`] (https://docs.google.com/spreadsheets/d/1Vg0cYQLL16h6lFBeq331NxvUnMrZf-aue75I1tzOXmA/edit?gid=199746582#gid=199746582)

**Description:**  
Provides contextual information about each game, such as date, teams, and location. Used to support joins and enrich transactional data.

**Common Use Cases:**
- Add context to ticket sales data  
- Analyze games by date or team  
- Join with sales data for deeper insights  

**Example Query:**
```sql
SELECT g.game_date, s.price_face
FROM primary_sales s
JOIN game_metadata g
ON s.game_id = g.game_id;
```
