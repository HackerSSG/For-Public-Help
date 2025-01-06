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
