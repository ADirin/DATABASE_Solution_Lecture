# Exercise 3: Efficient Social Network Application (Backend Only)

## Objective

Students will develop a backend system for managing a social network application. The system will handle users, posts, comments, friendships, and notifications. The focus is on demonstrating entity relationships and querying using JPQL and Criteria API, while ensuring efficient data retrieval and storage.

## Entities & Relationships

- **User** (id, name, email, joinDate)
- **Post** (id, content, postDate, userId)
- **Comment** (id, content, commentDate, postId, userId)
- **Friendship** (id, user1Id, user2Id, status)
- **Notification** (id, message, notificationDate, userId)

### Relationships

- A **User** can create multiple **Posts**, and a **Post** belongs to a single **User** (One-to-Many).
- A **Post** can have multiple **Comments**, and a **Comment** belongs to a single **Post** and a single **User** (Many-to-One for both).
- A **User** can have multiple **Friendships**, and a **Friendship** connects two **Users** (Many-to-Many via **Friendship** entity).
- A **User** can receive multiple **Notifications**, and a **Notification** belongs to a single **User** (One-to-Many).

## JPQL Queries

- Find all posts created by a specific user.
- Retrieve all comments on a specific post.
- Calculate the total number of friends for a specific user.
- List all notifications received by a user in the last week.

## Criteria API Queries

- Retrieve all users who have commented on a specific post.
- Search for posts that contain a specific keyword in their content.
- List all users who have more than 100 friends.

## Bonus Challenges

- Implement a feature to recommend friends based on mutual connections.
- Add a system to track user activity (e.g., number of posts, comments, and likes).
- Use stored procedures to generate monthly activity reports.

## Submission

### GitHub Repository

- Push the entire project to a GitHub repository.
- Include a `README.md` file with setup instructions and project details.

### 15-Minute Presentation

- Present the solution in class, demonstrating:
  - Entity relationships and JPA annotations.
  - JPQL and Criteria API queries.
  - Unit tests and bonus challenges (if implemented).
- Be prepared to answer questions.

