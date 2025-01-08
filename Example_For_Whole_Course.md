# Example used during the course
To create an example database that aligns with the outlined course topics, we can design a University Management System. 
This database is rich in relationships and concepts suitable for demonstrating various topics like temporal databases, query optimization, concurrency, advanced database features, and ORM with JPA.

## Week 1
- Week 1: Intro to Databases & Temporal Databases
- Goal: Introduce basic database operations and demonstrate temporal concepts.

```sql
-- Create temporal table for tracking enrollment history
CREATE TABLE Enrollments_History (
    enrollment_id INT,
    student_id INT,
    course_id INT,
    enrollment_date DATETIME,
    grade VARCHAR(2),
    valid_from DATETIME,
    valid_to DATETIME,
    PRIMARY KEY (enrollment_id, valid_from)
);

-- Insert initial enrollment
INSERT INTO Enrollments_History 
VALUES (1, 101, 201, '2025-01-08 10:00:00', NULL, '2025-01-08 10:00:00', '9999-12-31 23:59:59');

-- Query for current enrollments
SELECT student_id, course_id 
FROM Enrollments_History 
WHERE valid_to = '9999-12-31 23:59:59';

-- Update enrollment and archive old record
UPDATE Enrollments_History
SET valid_to = NOW()
WHERE enrollment_id = 1 AND valid_to = '9999-12-31 23:59:59';

INSERT INTO Enrollments_History
VALUES (1, 101, 201, '2025-01-08 10:00:00', 'A', NOW(), '9999-12-31 23:59:59');

```
## Week 2: 
- Week 2Query Optimization, Transactions & Isolation Levels
- Goal: Optimize queries and demonstrate transactions with isolation levels.

```sql
-- Optimize: Get all courses for a specific department
CREATE INDEX idx_department ON Courses(department);
SELECT * FROM Courses WHERE department = 'Computer Science';

-- Simulate transaction with seat availability check
START TRANSACTION;

-- Check seat availability
SELECT COUNT(*) AS enrolled FROM Enrollments WHERE course_id = 201;

-- Enroll student if seats are available
INSERT INTO Enrollments (student_id, course_id, enrollment_date) 
VALUES (101, 201, NOW());

COMMIT; -- Or ROLLBACK if constraints are violated

```
```sql
-- Optimize: Get all courses for a specific department
CREATE INDEX idx_department ON Courses(department);
SELECT * FROM Courses WHERE department = 'Computer Science';

-- Simulate transaction with seat availability check
START TRANSACTION;

-- Check seat availability
SELECT COUNT(*) AS enrolled FROM Enrollments WHERE course_id = 201;

-- Enroll student if seats are available
INSERT INTO Enrollments (student_id, course_id, enrollment_date) 
VALUES (101, 201, NOW());

COMMIT; -- Or ROLLBACK if constraints are violated


```
## Week 3
- Week 3: Locks & Versioning, Views
- Goal: Introduce row-level locks, versioning, and database views.

```sql
-- Use row-level locking to prevent concurrent updates
START TRANSACTION;

SELECT grade FROM Enrollments WHERE enrollment_id = 1 FOR UPDATE;

-- Update grade
UPDATE Enrollments SET grade = 'A' WHERE enrollment_id = 1;

COMMIT;

-- Create a view for active students and their courses
CREATE VIEW ActiveStudentsCourses AS
SELECT s.student_id, s.first_name, s.last_name, e.course_id, c.course_name
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
JOIN Courses c ON e.course_id = c.course_id
WHERE s.status = 'active';

-- Query the view
SELECT * FROM ActiveStudentsCourses;


```

## Week 4
- Week 4: Triggers, Stored Procedures & Events
- Goal: Use triggers, stored procedures, and scheduled events for advanced logic.

```sql
-- Trigger: Update student status to 'graduated'
CREATE TRIGGER UpdateGraduationStatus AFTER UPDATE ON Enrollments
FOR EACH ROW
BEGIN
    DECLARE total_courses INT;
    DECLARE passed_courses INT;
    
    SELECT COUNT(*) INTO total_courses FROM Courses WHERE course_id IN (SELECT course_id FROM Enrollments WHERE student_id = NEW.student_id);
    SELECT COUNT(*) INTO passed_courses FROM Enrollments WHERE student_id = NEW.student_id AND grade IS NOT NULL AND grade >= 'C';
    
    IF total_courses = passed_courses THEN
        UPDATE Students SET status = 'graduated' WHERE student_id = NEW.student_id;
    END IF;
END;

-- Stored procedure: Calculate student GPA
DELIMITER //
CREATE PROCEDURE CalculateGPA(IN studentId INT)
BEGIN
    SELECT AVG(CASE 
                 WHEN grade = 'A' THEN 4 
                 WHEN grade = 'B' THEN 3 
                 WHEN grade = 'C' THEN 2 
                 ELSE 0 
               END) AS GPA
    FROM Enrollments
    WHERE student_id = studentId;
END //
DELIMITER ;

-- Event: Archive enrollments
CREATE EVENT ArchiveEnrollments
ON SCHEDULE EVERY 1 MONTH
DO
    INSERT INTO Enrollments_Archive SELECT * FROM Enrollments WHERE enrollment_date < DATE_SUB(NOW(), INTERVAL 1 YEAR);


```
## Week 5
- Week 5: ORM with JPA (Single Class & 1:M Associations)
- Goal: Map a single table and 1:M associations in JPA.

```java
@Entity
public class Student {
    @Id @GeneratedValue
    private Long id;
    private String firstName;
    private String lastName;
    private LocalDate dateOfBirth;

    @OneToMany(mappedBy = "student")
    private List<Enrollment> enrollments = new ArrayList<>();
}



```
```java
@Entity
public class Enrollment {
    @Id @GeneratedValue
    private Long id;

    @ManyToOne
    @JoinColumn(name = "student_id")
    private Student student;

    @ManyToOne
    @JoinColumn(name = "course_id")
    private Course course;

    private LocalDateTime enrollmentDate;
}


```

##  Week 6
- Week 6: ORM with JPA (M:N, 1:1, and Inheritance)
- Goal: Demonstrate advanced ORM mapping.

```java
@Entity
public class Course {
    @Id @GeneratedValue
    private Long id;
    private String name;

    @ManyToMany
    @JoinTable(
        name = "enrollment",
        joinColumns = @JoinColumn(name = "course_id"),
        inverseJoinColumns = @JoinColumn(name = "student_id")
    )
    private List<Student> students = new ArrayList<>();
}



```
Example for 1:1 Association:
```java
@Entity
public class Department {
    @Id @GeneratedValue
    private Long id;
    private String name;

    @OneToOne
    @JoinColumn(name = "head_of_department")
    private Instructor head;
}


```

## Week 7
- Week 7: JPQL, Criteria API, Converters, Concurrency
- Goal: Use advanced JPA querying and object-level concurrency control.
JPQL Example:
```java
@Query("SELECT s FROM Student s WHERE (SELECT AVG(e.grade) FROM Enrollment e WHERE e.student = s) > 3.0")
List<Student> findHighPerformingStudents();

```
Optimistic Locking:
```java
@Entity
@OptimisticLocking(type = OptimisticLockType.VERSION)
public class Enrollment {
    @Version
    private int version;
}


```

