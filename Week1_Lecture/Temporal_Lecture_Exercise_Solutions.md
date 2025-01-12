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
>>> Transaction time records the period during which a piece of data is stored in the database. It reflects when a record existed in the database system, regardless of whether it is valid in the real world.
>>> This allows the database to keep a complete history of changes over time.
  
  3. Query the Books table to retrieve a list of all changes (versions) made to the database for book records since January 1, 2024.

-- Write your SQL query here.
```sql
SELECT * 
   FROM Books FOR SYSTEM_TIME ALL
   WHERE AddedDate >= '2024-01-01';


```

**Part B: Valid Time**
  3. The BorrowHistory table uses valid time to track the periods during which data is valid in the real world. What do ValidFrom and ValidTo represent?
    - ValidFrom: Represents the start of the period during which the data is valid in the real world.
    - ValidTo: Represents the end of the period during which the data is valid in the real world.
  
  4. Write an SQL query to find all books borrowed by "Alice" that were valid during January 2024.

```sql
SELECT * 
FROM BorrowHistory
WHERE Borrower = 'Alice' 
  AND ValidFrom <= '2024-01-31'
  AND ValidTo >= '2024-01-01';

```

**Part C: Decision Time**
  5. Define **decision time** in the context of temporal databases. How does it differ from transaction time?
>>>Decision time refers to the point at which a decision affecting the data was made.
>>>Unlike transaction time, which reflects the database's internal state, decision time focuses on when the user or system decided on a specific action.
  
  6. Provide an example scenario where decision time is crucial in a library system.
>>> In the library system, decision time is crucial when extending a book's due date.
>>> For example, if a staff member decides on January 10 to extend a book's return date to February 1, the decision time is recorded as January 10.

**Part D: System Versioning**

  7. Explain the purpose of system versioning in the Books and BorrowHistory tables.
>>> System versioning enables the database to automatically maintain and manage multiple versions of a record.
>>> This allows tracking of historical changes, rollback to previous states, and auditing.

  8. Write an SQL query to retrieve the complete version history of the book with BookID = 101.

```sql
SELECT * 
FROM Books FOR SYSTEM_TIME ALL
WHERE BookID = 101;

```

**Part E: Practical Analysis**
  9. Imagine that a record in the BorrowHistory table shows the following:
    - BorrowedDate = '2024-01-01'
    - ReturnDueDate = '2024-01-15'
    - ActualReturnDate = '2024-01-10'
    - ValidFrom = '2024-01-01'
    - ValidTo = '2024-01-15'

A system administrator corrects the ValidTo value to '2024-01-10'. What does this change signify, and how does it affect system versioning?

  - The update from ValidTo = '2024-01-15' to ValidTo = '2024-01-10' signifies that the record is only valid in the real world until January 10, instead of January 15.
  - This change implies that the borrower returned the book earlier than initially expected.
  - In terms of system versioning, the database will create a new version of the record to reflect the updated ValidTo value, preserving the original state for historical reference.

**Part F: Implementation**

  10. Create a query to insert a new versioned record into the Books table for a new book with the title "Temporal Databases Explained" by "John Doe". Ensure the AddedDate is set to today's date, and the book is removed after one year.

```sql
INSERT INTO Books (BookID, Title, Author, AddedDate, RemovedDate)
VALUES (201, 'Temporal Databases Explained', 'John Doe', CURRENT_DATE, DATE_ADD(CURRENT_DATE, INTERVAL 1 YEAR));

```

**Bonus** 

Design a new table Events to record decisions made by library staff. The table should include fields for:

  - Event ID
  - Decision description
  - Decision time
  - Staff member
  - Related BookID

Write the SQL statement to create this table.

```sql
CREATE TABLE Events (
    EventID INT PRIMARY KEY,
    DecisionDescription VARCHAR(255),
    DecisionTime DATETIME,
    StaffMember VARCHAR(100),
    RelatedBookID INT,
    FOREIGN KEY (RelatedBookID) REFERENCES Books(BookID)
);


```
