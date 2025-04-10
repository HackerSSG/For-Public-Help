# Refactoring Explained

## What is Refactoring?

Refactoring is the process of restructuring existing code to make it easier to understand, maintain, and modify. It is done by applying small changes to the code, ensuring the functionality remains the same.

### Key Points:
- **Small changes:** You make small modifications step-by-step.
- **Code must still work:** The code should function as it did before.
- **Unit tests:** You should use unit tests to make sure the code still works after changes.

## Goals of Refactoring:
- **More loosely coupled code:** The different parts of the code should not depend too much on each other.
- **More cohesive modules:** Each part of the code should focus on one specific task.
- **More comprehensible code:** The code should be easier to understand.

## When to Refactor?
You should refactor the code when:
- **You see a better way to do things:** Making the code easier to understand and modify.
- **You can do so without breaking the code:** Refactoring should not cause any new issues.

### When NOT to Refactor:
- **Stable code:** If the code works and doesn't need to change.
- **Someone else's code:** Only refactor another person's code if they agree or it belongs to you.

## Refactoring Process:
1. **Make a small change.**
2. **Run all tests:** Make sure the code still works after the change.
3. **If it works:** Move on to the next change.
4. **If it doesn't work:** Fix the issue or undo the change, so the system stays functional.

## Code Smells
Code smells are signs that the code might need refactoring. These include:
- **Duplicate code**
- **Long methods**
- **Big classes**
- **Big switch statements**
- **Long navigations (e.g., a.b().c().d())**
- **Checking for null objects**
- **Data clumps (e.g., fields for address, phone, email in a single class)**
- **Data classes (classes with only fields and no methods)**
- **Un-encapsulated fields (public variables)**

### Example: Switch Statements
Switch statements can often be replaced with polymorphism (creating different classes for different cases). This makes the code easier to extend without changing existing code.

## Common Refactoring Techniques:

### 1. Rename Method
If a method's name doesn't describe what it does, rename it to something more meaningful.

### 2. Extract Class
If a class does too much, split it into two classes to adhere to the Single Responsibility Principle.

### 3. Extract Interface
Create a smaller, specialized interface from a large one to follow the Interface Segregation Principle.

### 4. Extract Method
If a method is doing too much, split it into smaller methods to make it easier to understand and reuse.

### 5. Extract Subclass
If a class has attributes or methods that are only useful in specific situations, create a subclass for them.

### 6. Extract Superclass
If multiple classes share similar features, move those features to a common superclass.

### 7. Form Template Method
If two methods in subclasses perform the same steps but in different ways, create a method in the base class to hold the common steps.

### 8. Move Method
If a method is used more in another class than where it is defined, move it to the other class.

### 9. Introduce Null Object
If you are using `null` to represent default behavior, create a Null Object instead.

### 10. Replace Error Code with Exception
Instead of returning error codes, throw exceptions to indicate problems.

### 11. Replace Exception with Test
If you are catching exceptions that could be handled by a simple condition, use an `if` statement instead.

### 12. Nested Conditional with Guard Clauses
If there are too many nested conditions, use guard clauses to make the code clearer.

### 13. Replace Parameter with Explicit Method
If a method runs different code based on an enum parameter, create a separate method for each case.

### 14. Replace Temp with Query
If you use temporary variables, extract the expression into a method to make the code cleaner.

## Tools for Refactoring:
- **NetBeans** and **Visual Studio** offer built-in tools for refactoring.
- **RefactorIt** and **JRefactory** are additional tools for Java code.
- **Visual Studio** offers refactoring for actions like encapsulating fields and extracting methods.

## Additional Resources:
- [Refactoring Catalog](http://www.refactoring.com/catalog)

# BAD CODE
```java
public class Customer {
    private String name;
    private String address;
    private String phone;
    private String email;
    private boolean isGoldMember;

    public String getDiscount() {
        if (isGoldMember) {
            return "Gold member discount";
        } else {
            return "Regular member discount";
        }
    }

    public String getCustomerDetails() {
        if (address == null || phone == null || email == null) {
            return "Incomplete details";
        }
        return name + ", " + address + ", " + phone + ", " + email;
    }

    public String getSkin() {
        if (isGoldMember) {
            return "Golden skin";
        } else {
            return "Regular skin";
        }
    }

    public void printDiscountDetails() {
        System.out.println(getDiscount());
        System.out.println(getSkin());
    }

    // Getter and Setter methods for all fields...
}

```
# GOOD CODE
```java
// 1. **Rename Method**: Methods are renamed to make their purpose clearer
public class Customer {
    private String name;
    private String address;
    private String phone;
    private String email;
    private MembershipType membershipType; // 2. **Extract Method**: Extracted logic for discount and skin to a method inside an enum class

    // 3. **Extract Class**: Created MembershipType as a separate class (enum)
    public enum MembershipType {
        GOLD {
            @Override
            public String getDiscount() {
                return "Gold member discount";
            }

            @Override
            public String getSkin() {
                return "Golden skin";
            }
        },
        REGULAR {
            @Override
            public String getDiscount() {
                return "Regular member discount";
            }

            @Override
            public String getSkin() {
                return "Regular skin";
            }
        };

        public abstract String getDiscount();
        public abstract String getSkin();
    }

    // 4. **Encapsulate Field**: Using setter methods for address, phone, and email
    public void setAddress(String address) {
        this.address = address;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setMembershipType(MembershipType membershipType) {
        this.membershipType = membershipType;
    }

    // 5. **Extract Method**: Extracted "details incomplete" check to a separate method
    public String getCustomerDetails() {
        if (isDetailsIncomplete()) {
            throw new IllegalArgumentException("Incomplete details");
        }
        return name + ", " + address + ", " + phone + ", " + email;
    }

    private boolean isDetailsIncomplete() {
        return address == null || phone == null || email == null;
    }

    // 6. **Extract Subclass**: Moved MembershipType logic to an enum (as done above).
    // 7. **Extract Superclass**: Could create a superclass `CustomerBase` if we need more types of customers.

    // 8. **Form Template Method**: Using template methods in MembershipType for discount and skin logic
    // This isn't fully required in this refactor because enum handles the abstraction.

     //9. **Move Method**: Moved logic for skin and discount into the enum instead of inside Customer class

    public String getDiscount() {
        return membershipType.getDiscount();
    }

    public String getSkin() {
        return membershipType.getSkin();
    }

    // 10. **Introduce Null Object**: MembershipType enum eliminates null checks by defining default behaviors for both types (GOLD and REGULAR).
    // If a null MembershipType is set, it defaults to "REGULAR" by adding an UNDEFINED type (optional).

    // 11. **Replace Error Code with Exception**: If customer details are incomplete, throw an exception instead of just returning an error code string.
    public String getCustomerDetails() {
        if (isDetailsIncomplete()) {
            throw new IllegalArgumentException("Incomplete details");
        }
        return name + ", " + address + ", " + phone + ", " + email;
    }

    // 12. **Replace Exception with Test**: We aren't catching exceptions unnecessarily; we check the condition before throwing.
    // If details are incomplete, we throw an exception as an explicit test rather than relying on a return code.

    // 13. **Nested Conditional with Guard Clauses**: The `isDetailsIncomplete()` method is used for an early exit check before throwing exceptions.
    // This eliminates nested conditionals and makes code more readable.

    // 14. **Replace Parameter with Explicit Method**: We use the `getDiscount()` and `getSkin()` methods for clear access to logic instead of raw parameters.
}

```


# Paper Refactoring Question
### Before Refactoring
```csharp
Code: 
using System; 
using System.Collections.Generic; 
 
namespace classes 
{ 
    public class Program 
    { 
        public decimal Amount = 10000; 
        public DateTime Date DateTme.Now(); 
        public string Notes = “”;  
        public string Data= “”; 
        public List<Transaction> allTransactions = new List<Transaction>(); 
        public int accountNumberSeed = 1234567890; 
        public decimal Balance = 213123; 
        public string Number = “2222”; 
        public string Owner = “Ali”; 
        public char op = Convert.ToChar(Console.ReadLine()); 
        switch(op){ 
                case "a": 
                    Number = accountNumberSeed.ToString(); 
                    accountNumberSeed++; 
                    Owner = name; 
 
                    break; 
 
                case "b": 
                    Number = accountNumberSeed.ToString(); 
                    accountNumberSeed++; 
                    Owner = name; 
                    Balance = Balance + amount; 
                    allTransactions.Add(deposit); 
                    break; 
 
                case "c": 
                    Number = accountNumberSeed.ToString(); 
                    accountNumberSeed++; 
                    Owner = name; 
                    Balance = Balance - amount; 
                    allTransactions.Add(withdraw); 
                    break; 
 
                               default: 
                    break; 
            }  } }
```
# Refactored BankAccount Class



### Refactoring Steps:

1. **Encapsulation**: The `Balance`, `AccountNumber`, and `Owner` fields are now private and managed via public properties and methods.
2. **Class Responsibility**: The logic related to user interaction (`Console.ReadLine()`) is separated from the core functionality of the `BankAccount` class.
3. **Transaction Handling**: Introduced a `Transaction` class to better manage transactions.
4. **Improved Readability**: Cleaned up hard-coded values and made the code more reusable and extendable.

### Refactored Code:

```csharp
using System;
using System.Collections.Generic;

namespace BankApp
{
    public class BankAccount
    {
        // Properties of BankAccount
        public int AccountNumber { get; private set; }
        public string Owner { get; private set; }
        public decimal Balance { get; private set; }

        private static int accountNumberSeed = 1234567890;
        private List<Transaction> allTransactions = new List<Transaction>();

        // Constructor
        public BankAccount(string owner, decimal initialBalance)
        {
            AccountNumber = accountNumberSeed++;
            Owner = owner;
            if (initialBalance > 0)
            {
                Balance = initialBalance;
            }
            else
            {
                throw new ArgumentException("Initial balance must be positive");
            }
        }

        // Deposit Method
        public void Deposit(decimal amount)
        {
            if (amount <= 0)
            {
                throw new ArgumentException("Deposit amount must be positive");
            }

            Balance += amount;
            allTransactions.Add(new Transaction(TransactionType.Deposit, amount));
        }

        // Withdraw Method
        public void Withdraw(decimal amount)
        {
            if (amount <= 0)
            {
                throw new ArgumentException("Withdrawal amount must be positive");
            }

            if (Balance - amount < 0)
            {
                throw new InvalidOperationException("Insufficient funds for this withdrawal");
            }

            Balance -= amount;
            allTransactions.Add(new Transaction(TransactionType.Withdrawal, amount));
        }

        // Get account information
        public string GetAccountInfo()
        {
            return $"Account Number: {AccountNumber}, Owner: {Owner}, Balance: {Balance:C}";
        }
    }

    // Transaction class to track individual transactions
    public class Transaction
    {
        public TransactionType Type { get; private set; }
        public decimal Amount { get; private set; }
        public DateTime Date { get; private set; }

        public Transaction(TransactionType type, decimal amount)
        {
            Type = type;
            Amount = amount;
            Date = DateTime.Now;
        }
    }

    // Enum for transaction types
    public enum TransactionType
    {
        Deposit,
        Withdrawal
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            // Example of using BankAccount
            BankAccount account = new BankAccount("Ali", 1000);
            Console.WriteLine(account.GetAccountInfo());

            // Simulate a deposit
            account.Deposit(500);
            Console.WriteLine(account.GetAccountInfo());

            // Simulate a withdrawal
            account.Withdraw(200);
            Console.WriteLine(account.GetAccountInfo());

            // Trying to withdraw more than balance (error case)
            try
            {
                account.Withdraw(2000);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
-------------------------------------------------------------------------------------------------------------------------------------------------------------

# Key Refactoring Improvements

## BankAccount Class:
1. **Encapsulation**: 
   - `Balance`, `AccountNumber`, and `Owner` are now private fields with public properties. This means that these fields are hidden from the outside, and access is provided through methods or properties to ensure better control over the data.
   
2. **Deposit() and Withdraw() Methods**: 
   - These methods ensure valid operations and modify the account balance. The `Deposit()` method adds money to the balance, while the `Withdraw()` method ensures that the withdrawal doesn't result in a negative balance.

## Transaction Class:
- A `Transaction` class has been introduced to track individual transactions (deposit and withdrawal). This makes the code more modular and easier to extend in the future. Each transaction stores its type (deposit or withdrawal), amount, and date.

## Error Handling:
- Exception handling ensures proper validation of inputs and raises appropriate errors for invalid operations. For example, if the withdrawal amount is greater than the balance, an exception is thrown, preventing the operation from completing and ensuring the system behaves as expected.

## Use of Enums:
- The `TransactionType` enum helps distinguish between deposit and withdrawal transactions for better clarity. It makes the code more readable and self-explanatory, as we use meaningful names instead of arbitrary values for transaction types.

## User Interaction:
- The `Program` class handles user input and interaction with the bank account. The `BankAccount` class is responsible for all the operations related to the account itself (like deposits, withdrawals, and balance management). This separation ensures that the logic for account management is independent of user input, improving the overall maintainability of the code.




