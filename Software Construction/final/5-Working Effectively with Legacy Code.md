# Working Effectively with Legacy Code

## What is Legacy Code?

- **"Legacy Code is code without tests"**
- **"Piece of code which is maintained by someone other than its original author"**

## The Challenge with Changing Legacy Code

When working with legacy code, the primary challenge is to **preserve the existing behavior** while making changes. The difficulty arises when the code is not tested, as it's hard to know whether you broke anything.

### First, Add Tests, Then Make Changes

Before making changes, it’s important to have automated tests in place. Tests provide the **feedback** needed to know if you’ve altered the behavior of the code. 

Your goal is to **get to the point where you have tests** so that you can safely change and refactor the code.

## The Legacy Code Dilemma

Before making any changes, you should have tests in place. But, to write tests, you need to make changes to the code. This creates a **vicious cycle**.

### How to Break the Cycle

- **Minimal Safe Refactoring:** Change as little code as possible to get the tests in place. 
- **Identify Change Points (Seams):** Identify places where you can break dependencies and add tests without altering the code.
- **Write the Tests:** Once you have the tests in place, you can confidently proceed with refactoring.
- **Make Changes & Refactor:** After writing tests, you are safe to make changes and improve the code.

### The Key Steps:
1. **Identify Seams**
2. **Break Dependencies**
3. **Write Tests**
4. **Make Changes**
5. **Refactor**

## Seams: Identifying Points to Break Dependencies

One of the biggest challenges when adding tests to legacy code is that the code wasn’t designed with testability in mind. 

- **Dependency Problem:** Code often relies on external resources like databases, third-party servers, or complex parameters. This makes testing difficult.
- **Seams:** A **Seam** is a point in the code where you can alter the behavior of the code without changing the source code.

### Types of Seams

In **Object-Oriented Programming**, an object can often serve as a Seam. For instance, a problematic method like `connect()` could be tested by extending the class in the test environment to mock its behavior, avoiding interaction with the actual database.

## Unit Tests: Fast and Reliable

There’s often debate around what type of tests to prioritize. Should you focus on **unit tests** or **integration tests**? 

### Definition of a "Unit Test"

A **unit test** should:
- Run **fast** (less than 100ms).
- Not interact with external **infrastructure** like databases, file systems, or the network.

Unit tests are preferred for their speed and reliability.

### The Challenge of Writing Tests for Legacy Code

Sometimes, legacy code is hard to understand, making it difficult to write meaningful tests. In such cases, a good approach is:

### Characterization Tests

- **Characterization tests** are used to capture the **current behavior** of the code. These tests don’t try to define how the code should behave but instead ensure that the code behaves in the same way it currently does.
- This technique is also called **Approval Testing** or **Snapshot Testing**.

Characterization tests help you **cover legacy code quickly** and create a safety net for future changes.

### Steps for Characterization Testing
1. **Generate Output:** Capture the current behavior of the code.
2. **Test Coverage:** Ensure all input combinations are covered.
3. **Mutations:** Use mutations to verify your snapshots.

## Use Sprout & Wrap Techniques for Quick Changes

### The Sprout Technique

If you need to add new code but don’t have time for full refactoring, you can create the new code elsewhere, unit test it, and then **insert it** into the legacy code.

#### Example:
- You need to **deduplicate** some entries but cannot refactor the `postEntries()` method.
- **Sprout** a new method, e.g., `uniqueEntries()`, and test it.
- Then, **call** `uniqueEntries()` from the existing method with minimal changes.

### The Wrap Technique

When the change must occur before or after existing code, you can **wrap** the existing code:
- **Rename** the old method you want to wrap.
- Create a new method with the same name and signature.
- Put your new logic before or after the existing method call.

This technique allows you to test the new logic while maintaining the old code intact.

## Scratch Refactoring: Familiarizing Yourself with the Code

When faced with opaque legacy code, it can feel overwhelming. In such cases, you can use **scratch refactoring** to explore the code without the pressure to clean it up immediately.

### Scratch Refactoring Steps
1. **Explore:** Make changes to understand the code (e.g., extract functions, rename variables).
2. **Revert Changes:** Once you’re familiar with the code, revert your changes and start the proper testing process.

## Avoid Direct Dependency on Libraries

It's important not to litter your code with **direct calls to library classes**. When you use libraries, **wrap them** in your own abstractions to prevent your code from becoming tightly coupled to them.

### Why This Matters

- Libraries evolve and may have breaking changes in the future.
- If your code directly depends on them, you might find it difficult to upgrade or replace them later.

By wrapping libraries in abstractions, you maintain **control** over your dependencies, making future refactoring and upgrades easier.

