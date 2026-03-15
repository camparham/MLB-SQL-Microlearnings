# Competency 2: Data Types

## Purpose
Understand common data types and how they impact data modeling and analysis.

## Objectives
After completing this section, you will be able to:

- Recognize common data types
- Differentiate between data types and when to use them
- Apply rules of thumb when choosing data types

---

## Data Types

### 1️⃣ Numeric (INT, FLOAT)

#### Integer (`INT`)
A whole number (no decimals).

**Examples:**
- `user_id`
- `quantity`
- `age`
- `event_count`

#### Float (`FLOAT`)
A decimal number.

**Examples:**
- sensor readings
- averages
- scientific measurements

**Rules of thumb:**
- Do **not** use `FLOAT` for money (use `DECIMAL` instead).
- `INT` ≠ `FLOAT` (e.g., `25` is not the same as `25.5`).

---

### 2️⃣ String (CHAR, VARCHAR, TEXT)

#### `CHAR`
Fixed-length string (always uses the same space).

**Examples:**
- `country_code` ("US", "CA")

#### `VARCHAR`
Variable-length string.

**Examples:**
- `email`
- `username`
- `city`

#### `TEXT`
Large, unbounded strings.

**Examples:**
- `comments`
- `descriptions`
- `logs`

---

### 3️⃣ Dates & Times (DATE, TIMESTAMP)

#### `DATE`
Calendar date only (no time component).

**Examples:**
- `signup_date`
- `birth_date`
- `invoice_date`

#### `TIMESTAMP`
Date and time combined (often stored in UTC).

**Examples:**
- `created_at`
- `last_login`
- `event_time`

---

### 4️⃣ Boolean & NULL

#### `BOOLEAN`
True / False values (logical flags).

**Examples:**
- `is_active`
- `has_paid`
- `is_deleted`

#### `NULL`
Represents missing or unknown data (not a value).

**Examples:**
- `middle_name` (unknown)
- `end_date` (not yet occurred)
- `optional_phone_number`
