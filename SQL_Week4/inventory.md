# **Database Exercise: Triggers, Events, and Stored Procedures**

## **Objective**  
Students will demonstrate their ability to create **triggers, events, and stored procedures** by modifying an inventory management system. The task involves writing SQL scripts and providing screenshots of execution results.

---

## **Instructions**  

### 1. Create the Inventory Table  
- Execute the given SQL script to create and populate the `inventory` table.

```sql
CREATE TABLE inventory (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(255) NOT NULL,
    quantity INT NOT NULL DEFAULT 0,
    price DECIMAL(10, 2) NOT NULL,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    version INT DEFAULT 1
);

-- Step 2: Populate the inventory table with sample data
INSERT INTO inventory (product_name, quantity, price) VALUES
('Laptop', 50, 999.99),
('Smartphone', 100, 699.99),
('Tablet', 75, 399.99),
('Headphones', 150, 49.99),
('Smartwatch', 60, 199.99),
('Camera', 30, 499.99),
('Printer', 40, 89.99),
('Monitor', 25, 149.99),
('Keyboard', 200, 29.99),
('Mouse', 300, 19.99);

```


### 2. Create a Trigger  
- Create a **BEFORE UPDATE** trigger on the `inventory` table that increments the `version` column each time the row is updated.
- Name the trigger `before_inventory_update`.

### 3. Create a Stored Procedure  
- Write a stored procedure named `update_inventory` that:
  - Takes `product_id`, `new_quantity`, and `new_price` as parameters.
  - Updates the respective product’s quantity and price in the `inventory` table.
  - Automatically updates the `last_updated` timestamp.

### 4. Create an Event  
- Write an event named `daily_inventory_check` that:
  - Runs **every day at midnight**.
  - Checks if any product has a quantity of **less than 10** and logs it in a new table called `low_stock_alerts`.

### 5. Create the Low Stock Alerts Table  
- Design a new table called `low_stock_alerts` with:
  - `alert_id` (Primary Key, Auto Increment).
  - `product_id` (Foreign Key referencing `inventory`).
  - `product_name`.
  - `quantity`.
  - `alert_time` (Timestamp of when the event runs).

### 6. Demonstrate Execution  
- Update a product's quantity using `update_inventory` and show how the trigger works.
- Force an event execution manually and display the logged low-stock products.
- Take **screenshots** of the SQL code execution and upload them as a **PDF** on Moodle.

---

## **Submission Guidelines**  
- **Format:** Upload a single **PDF** file containing screenshots of your SQL scripts and execution results.  
- **Deadline:** *[Insert Due Date]*  
- **Submission Platform:** *Moodle*  

---

## **Expected Outcome**  
By completing this exercise, students will understand how to implement:  
✔ Triggers for automatic updates  
✔ Stored procedures for managing updates  
✔ Events for scheduled database tasks  

**Happy coding! 🚀**
