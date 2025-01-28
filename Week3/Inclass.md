# **Answers**

---

## **Part 1: Understanding Concurrency Challenges**

### **Potential Issues:**
1. **Dirty Reads:**  
   User C may see an inventory count modified by User A's transaction that hasn’t been committed yet. If User A’s transaction is rolled back, the data User C read was invalid.

2. **Non-Repeatable Reads:**  
   User B may see the inventory count change between two reads because User A’s transaction modified and committed the data in the meantime.

3. **Phantom Reads:**  
   If User C performs a query to count all available products, the result might include new rows added by User A’s transaction before it commits.

---

## **Part 2: Techniques for Managing Concurrency**

### **1. Locks (Pessimistic Concurrency Control)**

#### **SQL Example:**
```sql
LOCK TABLES inventory WRITE;

-- Reduce inventory for product_id = 1
UPDATE inventory
SET quantity = quantity - 1
WHERE product_id = 1;

UNLOCK TABLES;

````
## Discussion:
- Advantages: Ensures data consistency by preventing concurrent updates.
- Disadvantages: Reduces performance due to locking, potentially causing bottlenecks in high-traffic systems.

## 2. Multi-Version Concurrency Control (MVCC)

```sql
-- Transaction 1
START TRANSACTION;
SELECT quantity FROM inventory WHERE product_id = 1 FOR UPDATE;

-- Transaction 2 (reads without lock)
START TRANSACTION;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
SELECT quantity FROM inventory WHERE product_id = 1;

```
### Discussion:
- Advantages: Allows non-blocking reads while maintaining consistency.
- Disadvantages: May require more storage for versioned data.

## 3. Timestamp-Based Concurrency Control

```sql
-- Add a timestamp column to track updates
ALTER TABLE inventory ADD COLUMN last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;

-- Example query to compare timestamps
SELECT * FROM inventory
WHERE product_id = 1 AND last_updated < NOW();

```
### Discussion:
- Advantages: Helps resolve conflicts using clear rules based on timestamps.
- Disadvantages: May require frequent synchronization of timestamps across nodes in distributed systems.


## 4. Optimistic Concurrency Control

```sql
-- Add a timestamp column to track updates
ALTER TABLE inventory ADD COLUMN last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;

-- Example query to compare timestamps
SELECT * FROM inventory
WHERE product_id = 1 AND last_updated < NOW();


```
### Discussion:
- Advantages: Helps resolve conflicts using clear rules based on timestamps.
- Disadvantages: May require frequent synchronization of timestamps across nodes in distributed systems.

## 5. 5. Pessimistic Concurrency Control

```sql
START TRANSACTION;

-- Lock the row for reading and updating
SELECT quantity FROM inventory
WHERE product_id = 1 LOCK IN SHARE MODE;

-- Update after ensuring no conflict
UPDATE inventory
SET quantity = quantity - 1
WHERE product_id = 1;

COMMIT;

```
### Discussion:
- Advantages: Prevents conflicts by locking rows explicitly.
- Disadvantages: May reduce throughput due to extensive locking.

# Part 3: Extending the Scenario with Views
SQL to Create a View
```sql

CREATE VIEW available_inventory AS
SELECT product_name, quantity, last_updated
FROM inventory
WHERE quantity > 0;


```
Querying the View
```sql
SELECT * FROM available_inventory
WHERE product_name LIKE '%laptop%';
```
Ensuring Data Consistency
Use MVCC to provide consistent snapshots of data. Example:
```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

-- Query from the view within a transaction
START TRANSACTION;
SELECT * FROM available_inventory;
COMMIT;


```
# Questions Answered
1. How does the use of views help in managing concurrency?
- Views abstract data access, ensuring users see only relevant, consistent snapshots of the database. They help reduce direct access to underlying tables, minimizing concurrency issues.
2. What are the potential limitations of views in this context?
- Views rely on the underlying tables, so they may not solve all concurrency problems if the isolation level is improperly configured. Large views might also reduce query performance.
3. Impact of Isolation Levels on Views
- Higher isolation levels (e.g., REPEATABLE READ or SERIALIZABLE) provide consistent results but may reduce concurrency. Lower isolation levels (e.g., READ COMMITTED) improve concurrency but may allow inconsistent data in views.

# Deliverables
lock example
```sql
LOCK TABLES inventory WRITE;
UPDATE inventory SET quantity = quantity - 1 WHERE product_id = 1;
UNLOCK TABLES;

```
MVCC Example:

```sql
START TRANSACTION;
SELECT quantity FROM inventory WHERE product_id = 1 FOR UPDATE;
COMMIT;


```
Timestamp-Based Example:

```sql
ALTER TABLE inventory ADD COLUMN last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP;
SELECT * FROM inventory WHERE last_updated < NOW();
```
Optimistic Concurrency Example:
```sql
ALTER TABLE inventory ADD COLUMN version INT DEFAULT 1;
UPDATE inventory SET quantity = quantity - 1, version = version + 1 WHERE product_id = 1 AND version = 1;


```
View Example:
```sql
CREATE VIEW available_inventory AS
SELECT product_name, quantity, last_updated FROM inventory WHERE quantity > 0;


```
# Short Essay:
The techniques explored vary in complexity and suitability based on the use case. Pessimistic locking is simple but impacts performance, making it ideal for critical sections of code. MVCC balances performance and consistency, which is excellent for read-heavy workloads. Optimistic control is ideal when conflicts are rare, as retries are less frequent. Views further enhance concurrency management by abstracting direct table access, though careful configuration of isolation levels is necessary to maintain consistency.
