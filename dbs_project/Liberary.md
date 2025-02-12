# Library Management System (Backend Only)

## Objective

Students will work in pairs to develop a backend system using Hibernate, JPA, JPQL, and Criteria API to manage a library. The focus is on demonstrating various associations (One-to-One, One-to-Many, Many-to-One, and Many-to-Many) and executing queries using JPQL and the Criteria API. The UI is not required.

## Technology Stack

- Java (JDK 17 or later)
- Hibernate
- JPA
- JPQL & Criteria API
- MariaDB
- Spring Boot (optional for easier setup)
- Maven or Gradle
- JUnit (for testing)

## Project Requirements

### 1. Entities & Relationships

- **Book** (id, title, author, ISBN, publishedYear)
- **Member** (id, name, email, membershipDate)
- **Loan** (id, loanDate, returnDate)
- **Category** (id, name)
- **Librarian** (id, name, email)

#### Relationships

- A **Book** belongs to one **Category** (Many-to-One)
- A **Category** can have multiple **Books** (One-to-Many)
- A **Member** can borrow multiple **Books**, and a **Book** can be borrowed by multiple **Members** (Many-to-Many via **Loan** entity)
- A **Loan** is associated with a single **Librarian** (Many-to-One)

### 2. Database Configuration

- Configure Hibernate to use MariaDB as the database.
- Define a `persistence.xml` file or use `application.properties` for Spring Boot setup.
- Enable Hibernate’s SQL logging to verify queries and transactions.

### 3. JPQL Queries

- Query to find all books borrowed by a specific member.
- Retrieve a list of all overdue books based on the `returnDate`.
- Fetch all books that belong to a specific category.
- Count the number of books borrowed by each member.

### 4. Criteria API Queries

- Retrieve all members who have borrowed books in the last month.
- Search for books that contain a certain keyword in their title.
- List all librarians who have processed loans in the past year.

### 5. Additional Requirements

- Use proper JPA annotations such as `@Entity`, `@Table`, `@Id`, `@OneToMany`, `@ManyToOne`, and `@ManyToMany` where necessary.
- Implement cascading operations and fetch types appropriately.
- Organize the project using a service layer for business logic and a repository layer for data access.
- Write unit tests using JUnit to validate core functionalities.

## Evaluation Criteria

- Correct implementation of entity relationships ensuring data integrity.
- Proper use of JPA annotations to define mappings.
- Efficient querying using JPQL and Criteria API.
- Well-structured database schema and correct Hibernate configuration.
- Clean, readable code following best practices with proper layering.
- Demonstration of automated tests to ensure functionality.

## Bonus Challenges

- Implement a soft delete mechanism for **Book** (instead of physical deletion, mark a book as inactive using a status field).
- Use stored procedures in MariaDB for some operations to optimize performance.
- Implement pagination for listing books efficiently to handle large datasets.

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
     - Showcase unit tests and their results.
     - Highlight any bonus challenges implemented.
   - Be prepared to answer questions from the instructor or classmates.

This project will give students hands-on experience with Hibernate and JPA, focusing on backend development, data persistence, and complex querying using JPQL and Criteria API.
