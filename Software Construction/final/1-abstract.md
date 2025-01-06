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


```bash
using System;

// Abstract Class
public abstract class Animal
{
    // Abstract Method (no implementation)
    public abstract void Speak();
    
    // Regular Method (can be implemented in base class or derived class)
    public void Eat()
    {
        Console.WriteLine("This animal is eating.");
    }
}

// Subclass (Inheriting from Animal class)
public class Dog : Animal
{
    // Implementing abstract method
    public override void Speak()
    {
        Console.WriteLine("The dog barks.");
    }
}

// Abstract Data Type: Stack (Example of ADT)
public abstract class StackADT<T>
{
    public abstract void Push(T item);
    public abstract T Pop();
    public abstract bool IsEmpty();
}

public class IntStack : StackADT<int>
{
    private int[] stack = new int[10];
    private int top = -1;

    public override void Push(int item)
    {
        if (top < stack.Length - 1)
        {
            stack[++top] = item;
            Console.WriteLine($"{item} pushed to stack.");
        }
        else
        {
            Console.WriteLine("Stack overflow.");
        }
    }

    public override int Pop()
    {
        if (top >= 0)
        {
            int item = stack[top--];
            Console.WriteLine($"{item} popped from stack.");
            return item;
        }
        else
        {
            Console.WriteLine("Stack underflow.");
            return -1; // Return a default value
        }
    }

    public override bool IsEmpty()
    {
        return top == -1;
    }
}

class Program
{
    static void Main()
    {
        // Abstract Class Example
        Animal myDog = new Dog();
        myDog.Speak();  // Output: The dog barks.
        myDog.Eat();    // Output: This animal is eating.

        // Abstract Data Type Example (Stack)
        IntStack stack = new IntStack();
        stack.Push(10);  // Output: 10 pushed to stack.
        stack.Push(20);  // Output: 20 pushed to stack.
        stack.Pop();     // Output: 20 popped from stack.
        stack.Pop();     // Output: 10 popped from stack.
    }
}

```
