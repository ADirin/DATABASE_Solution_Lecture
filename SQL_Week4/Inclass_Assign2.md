# Exercise: Implementing Triggers, Events, and Stored Procedures

## Objective

The goal of this assignment is to gain hands-on experience with Triggers, Events, and Stored Procedures in MariaDB/MySQL. You will create database objects that automate tasks and ensure data consistency.

1. Create a database named UniversityDB.

2. Create the following table:

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    score INT CHECK (score BETWEEN 0 AND 100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```
3. Student_audit

```sql

CREATE TABLE student_audit (
    audit_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    old_score INT,
    new_score INT,
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```

## Part 1: Implementing a Trigger

### Task:

- Create an audit table named student_audit to store changes in student scores.

- Implement a BEFORE UPDATE trigger that logs old and new scores whenever a student’s score is updated.

### Requirements:

- The student_audit table should store student_id, old_score, new_score, and changed_at (timestamp of the change).

- The trigger should ensure that every score change is logged.

```sql
CREATE TRIGGER before_score_update
BEFORE UPDATE ON students
FOR EACH ROW
INSERT INTO student_audit (student_id, old_score, new_score)
VALUES (OLD.student_id, OLD.score, NEW.score);

```

## Part 2: Implementing a Scheduled Event

### Task:

- Create an event that automatically removes students who haven’t updated their score for one year.

### Requirements:

- The event should run once per day.

```sql
SET GLOBAL event_scheduler = ON;
```

- Ensure that event scheduling is enabled in MariaDB/MySQL.

```sql
CREATE EVENT remove_inactive_students
ON SCHEDULE EVERY 1 DAY
DO
DELETE FROM students WHERE created_at < NOW() - INTERVAL 1 YEAR;
```


## Part 3: Implementing a Stored Procedure

### Task:

- Create a stored procedure named UpdateStudentScore that allows updating a student's score while logging the change in the student_audit table.

### Requirements:

- The procedure should accept student ID and new score as parameters.

- It should first retrieve the current score, update it, and log the change.

```sql
DELIMITER //

CREATE PROCEDURE UpdateStudentScore(
    IN studentID INT,
    IN newScore INT
)
BEGIN
    DECLARE oldScore INT;
    
    -- Fetch the current score
    SELECT score INTO oldScore FROM students WHERE student_id = studentID;

    -- Update the student's score
    UPDATE students SET score = newScore WHERE student_id = studentID;

    -- Log the change
    INSERT INTO student_audit (student_id, old_score, new_score)
    VALUES (studentID, oldScore, newScore);
END //

DELIMITER ;

```

📂 Submission Guidelines

1. Write your SQL queries for each part and execute them in MariaDB/MySQL.

2. Capture screenshots of:

  - Table structures

  - Trigger execution

  - Event execution

  - Stored procedure execution

3. Compile your SQL scripts and screenshots into a single PDF document.

4. Submit the PDF on Moodle under the designated assignment section.
