### Intro to Swift: Session Breakdown

**1. Introduction to Swift**  
Swift is a modern, powerful, and easy-to-learn programming language developed by Apple for iOS, macOS, watchOS, and tvOS development. Swift is fast, safe, and expressive, and it aims to make it easier for developers to write clean and efficient code.

#### Key Swift Features:
- Type-safe and memory-managed.
- Combines object-oriented and functional programming paradigms.
- Interoperable with Objective-C (for legacy code).

---
### 2. Basics of Swift: Key Concepts

#### Constants and Variables:
Start by introducing **constants** and **variables**, explaining the difference between the two.

- **Constants**: Declared with `let`. Once a constant is assigned a value, it can't be changed.
- **Variables**: Declared with `var`. Variables can be modified after being assigned a value.

**Example:**
```swift
let name = "John"  // This is a constant, its value cannot be changed.
var age = 30       // This is a variable, its value can be updated.
```

To explain this:
- A **constant** is useful for data you know won’t change (like a fixed value or label).
- A **variable** is used when the data can change, like a user’s input or calculation result.

**Hands-on Exercise:**
- Declare a constant for your name.
- Declare a variable for age and update it.

#### Data Types:
Swift is strongly typed, which means it enforces the data type for variables and constants. 

Common types:
- `String` (text)
- `Int` (whole numbers)
- `Double` (decimal numbers)
- `Bool` (true/false)

You can either declare types explicitly or allow Swift to infer them:
```swift
var score: Int = 100  // Explicitly declaring type
var message = "Hello" // Swift infers the type (String)
```

---
### 3. Operations

**Basic Operations:**
Swift allows common arithmetic operations on numbers: `+`, `-`, `*`, `/`, and `%` (modulo).

Example:
```swift
let sum = 5 + 3   // Adds two numbers
let difference = 10 - 4  // Subtracts 4 from 10
let product = 2 * 3  // Multiplies 2 and 3
let quotient = 8 / 2  // Divides 8 by 2
```

**Comparison Operators:**
Explain how comparison operators are used to compare values:
- `==` (equal to)
- `!=` (not equal to)
- `<`, `<=`, `>`, `>=`

Example:
```swift
let isEqual = (5 == 5)  // true
let isGreater = (8 > 5) // true
```

---
### 4. Control Flow

Control flow allows you to define conditions and execute code based on them.

#### **If-Else Statements:**
Used to run code based on certain conditions.

Example:
```swift
let score = 75

if score > 90 {
    print("You got an A")
} else if score > 75 {
    print("You got a B")
} else {
    print("You need to improve")
}
```

#### **Switch Statements:**
Another way to manage conditional logic, used for multiple possible values.

Example:
```swift
let grade = "A"

switch grade {
case "A":
    print("Excellent")
case "B":
    print("Good")
default:
    print("Needs Improvement")
}
```

---
### 5. Loops

Explain the two main types of loops used in Swift: `for` loops and `while` loops.

#### **For Loops:**
Used when the number of iterations is known ahead of time.

Example:
```swift
for i in 1...5 {
    print("This is loop number \(i)")
}
```
Explain the use of ranges (`1...5`), where the loop runs from 1 to 5 inclusive.

### While Loops in Swift

A `while` loop is used to repeatedly execute a block of code as long as a specified condition is true. Swift has two types of `while` loops:

1. **While Loop**: Checks the condition before running the code inside the loop.
2. **Repeat-While Loop**: Runs the code inside the loop at least once before checking the condition, then continues as long as the condition is true.

---

### **1. While Loop**
The `while` loop continues to execute as long as the condition evaluates to `true`.

**Syntax:**
```swift
while condition {
    // code to be executed
}
```

**Example:**
```swift
var counter = 1

while counter <= 5 {
    print("Counter is \(counter)")
    counter += 1  // Increment counter by 1
}
```

- The loop runs while `counter` is less than or equal to 5.
- Once the condition becomes false (when `counter` is greater than 5), the loop stops.

---

### **2. Repeat-While Loop**
A `repeat-while` loop first runs the code inside the loop and then checks the condition. This ensures that the loop is executed **at least once** even if the condition is false initially.

**Syntax:**
```swift
repeat {
    // code to be executed
} while condition
```

**Example:**
```swift
var number = 5

repeat {
    print("Number is \(number)")
    number -= 1
} while number > 0
```

- In this case, the loop prints the value of `number` starting from 5 and decrements it after each iteration.
- The loop runs until `number` is no longer greater than 0.

### Difference Between `while` and `repeat-while`:
- In a `while` loop, the condition is checked **before** the loop executes, so if the condition is false initially, the loop won’t run at all.
- In a `repeat-while` loop, the code block is executed **before** the condition is checked, ensuring that the loop executes at least once.

---


Let’s write a simple program that ensures the user enters a positive number:

```swift
var userInput: Int

repeat {
    print("Enter a positive number:")
    userInput = Int(readLine()!)!  // Taking input from user (assuming it's a number)
} while userInput <= 0

print("You entered a positive number: \(userInput)")
```

- The loop asks the user for input.
- Even if the user enters an invalid number initially (less than or equal to 0), the prompt will repeat until a valid positive number is entered.

---

