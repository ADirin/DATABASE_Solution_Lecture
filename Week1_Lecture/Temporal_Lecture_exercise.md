# Exercise: Exploring Temporal Aspects of Databases

## Objective  
This exercise helps students understand temporal aspects of databases, including **transaction time**, **valid time**, **decision time**, and **system versioning**. Students will work with temporal concepts, querying a versioned database, and analyzing how temporal information affects data integrity and decision-making.

---

## Scenario  

You are working with a **temporal database** for a library system that tracks books, their availability, and borrower information. The database records both the **history of transactions** (transaction time) and the **validity of data in the real world** (valid time). Additionally, the system uses **system versioning** to manage multiple versions of records over time.

### Tables  

1. **Books**  
```sql
   CREATE TABLE Books (
       BookID INT PRIMARY KEY,
       Title VARCHAR(100),
       Author VARCHAR(100),
       AddedDate DATE,
       RemovedDate DATE
   ) WITH SYSTEM VERSIONING;
```
2. **BorrowHistory**  
```sql

CREATE TABLE BorrowHistory (
    TransactionID INT PRIMARY KEY,
    BookID INT,
    Borrower VARCHAR(100),
    BorrowedDate DATE,
    ReturnDueDate DATE,
    ActualReturnDate DATE,
    ValidFrom DATE,
    ValidTo DATE
) WITH SYSTEM VERSIONING;


  ```

## Questions
**Part A: Transaction Time**
  1. Explain the purpose of the transaction time in a temporal database.
  2. Query the Books table to retrieve a list of all changes (versions) made to the database for book records since January 1, 2024.

-- Write your SQL query here.

**Part B: Valid Time**
  3. The BorrowHistory table uses valid time to track the periods during which data is valid in the real world. What do ValidFrom and ValidTo represent?
  4. Write an SQL query to find all books borrowed by "Alice" that were valid during January 2024.

-- Write your SQL query here.

**Part C: Decision Time**
  5. Define **decision time** in the context of temporal databases. How does it differ from transaction time?
  6. Provide an example scenario where decision time is crucial in a library system.

**Part D: System Versioning**

  7. Explain the purpose of system versioning in the Books and BorrowHistory tables.
  8. Write an SQL query to retrieve the complete version history of the book with BookID = 101.

-- Write your SQL query here.

**Part E: Practical Analysis**
  9. Imagine that a record in the BorrowHistory table shows the following:
    - BorrowedDate = '2024-01-01'
    - ReturnDueDate = '2024-01-15'
    - ActualReturnDate = '2024-01-10'
    - ValidFrom = '2024-01-01'
    - ValidTo = '2024-01-15'

A system administrator corrects the ValidTo value to '2024-01-10'. What does this change signify, and how does it affect system versioning?

**Part F: Implementation**

  10. Create a query to insert a new versioned record into the Books table for a new book with the title "Temporal Databases Explained" by "John Doe". Ensure the AddedDate is set to today's date, and the book is removed after one year.

-- Write your SQL query here.

**Bonus** 

Design a new table Events to record decisions made by library staff. The table should include fields for:

  - Event ID
  - Decision description
  - Decision time
  - Staff member
  - Related BookID

Write the SQL statement to create this table.

