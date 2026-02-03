# Lesson 1: Data Types 

### Purpose 
Learning data types is important because they determine what kind of data can be stored, how it’s validated, and how operations behave when you query it. Understanding data types helps you avoid errors, write accurate comparisons and calculations, and ensure your SQL logic matches the real meaning of the data

### Objectives
After completing this section, you will be able to: 
* Recognize common data types
* Differentiate between the different data types and when to use them

## Data Types 

### Types of data 
* Numeric (int, float)
  - **Integer (i.e., int): A whole number.**
  - Examples:
    * user_id
    * quantity
    * age
    * count of events
      
  - **Float: A decimal that can be rounded.**
  - Examples:
    * sensor readings
    * averages
    * scientific data

**Rules of thumb:**
  * Do not use a float for money
  * INT ≠ FLOAT (e.g., 25 does not equal 25.5)

    
* String (char, varchar, text)
**  **- Char: Fixed-length string (always uses the same space) ****
  - Examples:
    * country_code ("US", "CA")
      
  *** Varchar: Variable-length string**
    - Examples:
      * email
      * username
      * city
        
 ** * Text: Large, unbounded strings**
  - Examples:
    * comments
    * descriptions
    * logs
      
* Dates & Times (DATE, TIMESTAMP)
- DATE: Calendar date only (no time component)

- Examples:

* signup_date

birth_date

invoice_date

- TIMESTAMP: Date and time combined (often stored in UTC)

Examples:

created_at

last_login

event_time

Boolean / NULL

* BOOLEAN: True / False values (logical flags)

  - Examples:
    * is_active
    * has_paid
    * is_deleted

* NULL: Represents missing or unknown data (not a value)

Examples:

  middle_name (unknown)

end_date (not yet occurred)

optional_phone_number
 
