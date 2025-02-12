# Exercise 2: Fitness Center Management System
Objective
Students will develop a backend system for managing a fitness center. The system will handle members, trainers, workout plans, and attendance records. The focus is on demonstrating entity relationships and querying using JPQL and Criteria API.

Entities & Relationships
Member (id, name, email, joinDate)

Trainer (id, name, specialization)

WorkoutPlan (id, name, description, duration)

Attendance (id, date, status)

Membership (id, startDate, endDate)

Relationships
A Member can have one Membership, and a Membership belongs to a single Member (One-to-One).

A Trainer can create multiple WorkoutPlans, and a WorkoutPlan is associated with a single Trainer (Many-to-One).

A Member can attend multiple workout sessions, and each Attendance record is associated with a Member and a WorkoutPlan (Many-to-Many).

JPQL Queries
Find all workout plans created by a specific trainer.

Retrieve attendance records for a specific member.

Calculate the total number of active members.

List all members whose membership has expired.

Criteria API Queries
Retrieve all trainers who specialize in a specific workout type (e.g., yoga, weightlifting).

Search for members who joined in the last month.

List all workout plans with a duration longer than 60 minutes.

Bonus Challenges
Implement a feature to automatically renew memberships.

Add a system to track member progress (e.g., weight loss, muscle gain).

Use stored procedures to generate monthly attendance reports.

Submission for Both Exercises
GitHub Repository:

Push the entire project to a GitHub repository.

Include a README.md file with setup instructions and project details.

15-Minute Presentation:

Present the solution in class, demonstrating:

Entity relationships and JPA annotations.

JPQL and Criteria API queries.

Unit tests and bonus challenges (if implemented).

Be prepared to answer questions.
