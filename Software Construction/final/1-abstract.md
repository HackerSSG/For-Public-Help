# Abstract Class, Abstract Methods, and Abstract Data Types

## Abstract Class
An **abstract class** is a class that cannot be instantiated directly. It serves as a blueprint for other classes. You can think of it as a class that provides a common structure for its subclasses but doesn't implement all of its methods.

- **Purpose:** To define common properties or methods that should be shared by multiple subclasses.

## Abstract Methods
An **abstract method** is a method that is declared in an abstract class but doesn't have an implementation. Subclasses of the abstract class are required to implement these methods.

- **Purpose:** To enforce subclasses to provide specific behavior for that method.

## Abstract Data Types (ADT)
An **abstract data type (ADT)** is a data structure that is defined by its behavior (operations) rather than its implementation. The details of how it works internally are hidden, and only the operations available to the user are exposed.

- **Purpose:** To define data structures where the details of how they work are hidden from the user.

### Example Summary
- **Abstract Class**: A class that cannot be instantiated.
- **Abstract Method**: A method that has no body and must be implemented by subclasses.
- **Abstract Data Type**: A data structure defined by operations, not implementation.
