# SQL for Beginners: MLB Microlearning Course

A competency-based SQL learning experience using real MLB data to help you think like a data analyst — not just write queries.

---

## 📌 Overview

This course is designed for beginners who want to learn SQL through structured, real-world practice.

Each lesson is built around a **core competency** — a practical skill you need to work with data effectively.

Instead of memorizing syntax, you’ll build competencies like:
- understanding data structure
- asking better questions
- creating reliable insights

---

## 🎯 What You’ll Learn

By the end of this course, you’ll be able to:

- Explore datasets before analyzing them  
- Translate business questions into SQL queries  
- Identify the correct **grain** of your data  
- Avoid common mistakes like double-counting  
- Debug your queries when results don’t make sense  

---

## 🧠 Competency-Based Curriculum

Each section focuses on a specific skill you’ll build as you progress:

---

### Competency 1: Data Modeling Foundations  
Learn how data is structured before writing queries.

---

### Competency 2: Reading Data (Pre-Manipulation)  
Learn how to explore and validate your data before analysis.

- Understand what data is available  
- Use `SELECT` to explore tables  
- Identify the correct data grain  
- Avoid incorrect assumptions  

---

### Competency 3: Preparing Data for Analysis  
Learn how to shape data into something usable.

- Filter and structure your data  
- Prepare for aggregations  
- Build clean, readable queries  

---

## ⚾ Dataset

This course uses real-world MLB data, including:

- Player rosters  
- Ticket sales  
- Game-level data  

This allows you to answer questions like:

- Who is currently on the active roster?  
- What data is available before building reports?  
- How do we avoid double-counting revenue?  

---

## 💡 Example Competency in Action

Before building reports, we always ask:

> “What data do we actually have?”

```sql
SELECT * 
FROM workspace.default.mlb_active_rosters_new;
