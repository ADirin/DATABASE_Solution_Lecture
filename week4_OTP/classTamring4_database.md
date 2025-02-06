## Step 1: Create the Inventory Table

```sql

CREATE TABLE inventory (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(255) NOT NULL,
    quantity INT NOT NULL DEFAULT 0,
    price DECIMAL(10, 2) NOT NULL,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    version INT DEFAULT 1
);

```

Step 2: Insert Sample Data
```sql
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

## Step 3: Create trigger 
Create a BEFORE UPDATE trigger to increment the version column on updates.
```sql
DELIMITER $$

CREATE TRIGGER before_inventory_update
BEFORE UPDATE ON inventory
FOR EACH ROW
BEGIN
    SET NEW.version = OLD.version + 1;
END$$

DELIMITER ;

```
## Step 4: Create a Stored Procedure
A stored procedure update_inventory to update quantity and price.
```sql

DELIMITER $$

CREATE PROCEDURE update_inventory(
    IN p_product_id INT, 
    IN p_new_quantity INT, 
    IN p_new_price DECIMAL(10,2)
)
BEGIN
    UPDATE inventory 
    SET quantity = p_new_quantity, 
        price = p_new_price
    WHERE product_id = p_product_id;
END$$

DELIMITER ;


```


```sql
CALL update_inventory(1, 45, 950.99);

```
## Step 6: Create an Event
An event daily_inventory_check that runs daily to check low stock products.

```sql
DELIMITER $$

CREATE EVENT daily_inventory_check
ON SCHEDULE EVERY 1 DAY
STARTS CURRENT_TIMESTAMP
DO
BEGIN
    INSERT INTO low_stock_alerts (product_id, product_name, quantity)
    SELECT product_id, product_name, quantity 
    FROM inventory 
    WHERE quantity < 10;
END$$

DELIMITER ;


```
