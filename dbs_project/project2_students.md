# Course Management System (Backend Only)

## Objective

Students will work in pairs to develop a backend system using Hibernate, JPA, JPQL, and Criteria API to manage a course system. The focus is on demonstrating various associations (One-to-One, One-to-Many, Many-to-One, and Many-to-Many) and executing queries using JPQL and the Criteria API. The system will handle student enrollment, in-class assignments, home assignments, projects, and exams. The UI is not required.

## Technology Stack

- Java (JDK 17 or later)
- Hibernate
- JPA
- JPQL & Criteria API
- MariaDB
- Maven / Spring Boot (optional for easier setup)


## Project Requirements

### 1. Entities & Relationships

- **Student** (id, name, email, enrollmentDate)
- **Course** (id, name, description, startDate, endDate)
- **InClassAssignment** (id, title, description, dueDate, maxScore)
- **HomeAssignment** (id, title, description, dueDate, maxScore)
- **Project** (id, title, description, dueDate, maxScore)
- **Exam** (id, title, description, examDate, maxScore)
- **Grade** (id, score, feedback)

#### Relationships

- A **Student** can enroll in multiple **Courses**, and a **Course** can have multiple **Students** (Many-to-Many).
- A **Course** can have multiple **InClassAssignments**, **HomeAssignments**, **Projects**, and **Exams** (One-to-Many).
- Each **InClassAssignment**, **HomeAssignment**, **Project**, and **Exam** is associated with a single **Course** (Many-to-One).
- A **Grade** is associated with a **Student** and an **InClassAssignment**, **HomeAssignment**, **Project**, or **Exam** (Many-to-One for each).

### 2. Database Configuration

- Configure Hibernate to use MariaDB as the database.
- Define a `persistence.xml` file or
- use `application.properties` for Spring Boot setup (Optional).
- Enable Hibernate’s SQL logging to verify queries and transactions.

### 3. JPQL Queries

- Query to find all students enrolled in a specific course.
- Retrieve a list of all assignments (in-class and home) due in the next week.
- Fetch all grades for a specific student in a particular course.
- Calculate the average score of all students for a specific exam.

### 4. Criteria API Queries

- Retrieve all students who have not submitted a specific home assignment.
- Search for courses that contain a certain keyword in their description.
- List all students who scored above a certain threshold in a specific exam.

### 5. Additional Requirements

- Use proper JPA annotations such as `@Entity`, `@Table`, `@Id`, `@OneToMany`, `@ManyToOne`, and `@ManyToMany` where necessary.
- Implement cascading operations and fetch types appropriately.
- Organize the project using a service layer for business logic and a repository layer for data access.


## Evaluation Criteria

- Correct implementation of entity relationships ensuring data integrity.
- Proper use of JPA annotations to define mappings.
- Efficient querying using JPQL and Criteria API.
- Well-structured database schema and correct Hibernate configuration.
- Clean, readable code following best practices with proper layering.


## Bonus Challenges

- Implement a soft delete mechanism for **Course** (instead of physical deletion, mark a course as inactive using a status field).
- Use stored procedures in MariaDB for some operations to optimize performance.
- Implement pagination for listing students and courses efficiently to handle large datasets.

## Submission

1. **GitHub Repository**:
   - Push the entire project to a GitHub repository.
   - Ensure the repository is well-organized, with clear documentation in the `README.md` file.
   - Include instructions for setting up and running the project locally.

2. **15-Minute Presentation**:
   - Present the solution in class, demonstrating the following:
     - Overview of the project structure and design.
     - Explanation of entity relationships and JPA annotations.
     - Demonstration of JPQL and Criteria API queries.
     - Highlight any bonus challenges implemented.
   - Be prepared to answer questions from the instructor or classmates.

This project will give students hands-on experience with Hibernate and JPA, focusing on backend development, data persistence, and complex querying using JPQL and Criteria API.
