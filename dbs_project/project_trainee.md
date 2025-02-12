# Trainee Placement System (Backend Only)

## Objective

Students will work in pairs to develop a backend system using Hibernate, JPA, JPQL, and Criteria API to manage a trainee placement system. The system will handle student applications, trainee positions, and company details. The focus is on demonstrating various associations (One-to-One, One-to-Many, Many-to-One, and Many-to-Many) and executing queries using JPQL and the Criteria API. The UI is not required.

## Technology Stack

- Java (JDK 17 or later)
- Hibernate
- JPA
- JPQL & Criteria API
- MariaDB
- Spring Boot (optional for easier setup)
- Maven or Gradle


## Project Requirements

### 1. Entities & Relationships

- **Student** (id, name, email, skills, GPA)
- **Company** (id, name, industry, description)
- **TraineePosition** (id, title, description, requiredSkills, location)
- **Application** (id, applicationDate, status)

#### Relationships

- A **Student** can apply to multiple **TraineePositions**, and a **TraineePosition** can receive applications from multiple **Students** (Many-to-Many via **Application** entity).
- A **TraineePosition** is associated with a single **Company** (Many-to-One).

### 2. Database Configuration

- Configure Hibernate to use MariaDB as the database.
- Define a `persistence.xml` file
- or use `application.properties` for Spring Boot setup (optional).
- Enable Hibernate’s SQL logging to verify queries and transactions.

### 3. JPQL Queries

- Query to find all students who applied to a specific trainee position.
- Retrieve a list of all trainee positions in a specific industry.
- Fetch all applications with a status of "Pending".
- Count the number of applications for each trainee position.

### 4. Criteria API Queries

- Retrieve all students who have applied to trainee positions requiring a specific skill.
- Search for trainee positions that match a student's skills.
- List all companies that have posted trainee positions in the last month.

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
- Demonstration of automated tests to ensure functionality.

## Bonus Challenges

- Implement a soft delete mechanism for **TraineePosition** (instead of physical deletion, mark a position as inactive using a status field).
- Use stored procedures in MariaDB for some operations to optimize performance.
- Implement pagination for listing students and trainee positions efficiently to handle large datasets.
- Add a feature to notify students about new trainee positions that match their skills via email.

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


