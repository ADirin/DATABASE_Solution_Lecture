# **Java Assignment: JUnit Testing & Code Coverage_Week4**

## **Objective**  
The purpose of this assignment is to:  
- Implement a **BankAccount** class with basic banking operations.  
- Write **JUnit test cases** to verify functionality.  
- Measure **code coverage** using a tool like **JaCoCo**.  

---

## **Problem Statement**  
You need to develop a **BankAccount** class that supports the following operations:  
- **Deposit**: Adds an amount to the account balance.  
- **Withdraw**: Deducts an amount from the balance if sufficient funds are available.  
- **Check Balance**: Returns the current balance.  

Additionally, write JUnit test cases to ensure the correctness of your implementation. Finally, generate a code coverage report and ensure at least **80% coverage**.  

---

## **Step 1: Implement the `BankAccount` Class**  
Create a Java class named **`BankAccount`** with the following specifications:  

```java
public class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        if (initialBalance < 0) {
            throw new IllegalArgumentException("Initial balance cannot be negative");
        }
        this.balance = initialBalance;
    }

    public void deposit(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Deposit amount must be positive");
        }
        balance += amount;
    }

    public void withdraw(double amount) {
        if (amount > balance) {
            throw new IllegalArgumentException("Insufficient funds");
        }
        if (amount <= 0) {
            throw new IllegalArgumentException("Withdrawal amount must be positive");
        }
        balance -= amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

---

## **Step 2: Write JUnit Test Cases**  
Create a **JUnit test class** named **`BankAccountTest`** to test all methods.  

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class BankAccountTest {
    private BankAccount account;

    @BeforeEach
    void setUp() {
        account = new BankAccount(100.0); // Initial balance of $100
    }

    @Test
    void testDeposit() {
        account.deposit(50.0);
        assertEquals(150.0, account.getBalance());
    }

    @Test
    void testWithdraw() {
        account.withdraw(30.0);
        assertEquals(70.0, account.getBalance());
    }

    @Test
    void testWithdrawInsufficientFunds() {
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            account.withdraw(200.0);
        });
        assertEquals("Insufficient funds", exception.getMessage());
    }

    @Test
    void testNegativeDeposit() {
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            account.deposit(-10.0);
        });
        assertEquals("Deposit amount must be positive", exception.getMessage());
    }

    @Test
    void testNegativeWithdraw() {
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            account.withdraw(-5.0);
        });
        assertEquals("Withdrawal amount must be positive", exception.getMessage());
    }
}
```

---

## **Step 3: Run JUnit Tests**  
To run the JUnit tests, you can use **JUnit 5** with **Maven** or **Gradle**:  
1. Add the JUnit dependency to `pom.xml` (for Maven projects):  

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.8.1</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.8.1</version>
    </dependency>
</dependencies>
```

2. Run the tests using:  
   ```
   mvn test
   ```

---

## **Step 4: Measure Code Coverage using JaCoCo**  
JaCoCo is a Java code coverage tool that helps visualize test coverage.  

### **1. Add JaCoCo to `pom.xml`**  

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.8</version>
            <executions>
                <execution>
                    <goals>
                        <goal>prepare-agent</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

### **2. Generate Coverage Report**  
Run:  
```
mvn test jacoco:report
```
The report will be generated in:  
```
target/site/jacoco/index.html
```
Open `index.html` in a browser to view coverage details.  

---

## **Step 5: Submission Requirements**  
Students should submit:  
1. **BankAccount.java** (Implementation)  
2. **BankAccountTest.java** (JUnit Test Cases)  
3. **JaCoCo Report Screenshots** (Code coverage must be at least **80%**)  

---

## **Assessment Criteria**  
| Criteria | Description | Marks |
|----------|------------|-------|
| Functionality | Implementation of `BankAccount` class | 30% |
| JUnit Tests | Correctness & completeness of test cases | 30% |
| Code Coverage | At least 80% using JaCoCo | 20% |
| Code Quality | Proper use of OOP, exceptions, and best practices | 20% |

---

## **Bonus Task (Optional - Extra 10%)**  
Enhance the `BankAccount` class by adding:  
- **Transaction History**: Store each deposit/withdrawal.  
- **Interest Calculation**: Apply a monthly interest rate.  
- Write JUnit tests for these features.  

---
