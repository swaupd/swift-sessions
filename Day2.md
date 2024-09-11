### Strings, Collections, Structs, and Classes in Swift

These are fundamental concepts in Swift that are essential for writing powerful and efficient code. Let's break each of these down and explain them:

---

## 1. **Strings**
Strings in Swift are a collection of characters. They can represent text, and Swift strings are Unicode-compliant, meaning they handle characters from various languages.

### **Declaring Strings:**
```swift
let name: String = "Alice"
var greeting = "Hello"
```

- `let` defines a constant string that cannot be changed.
- `var` defines a variable string that can be modified.

### **String Interpolation:**
You can embed variables or expressions inside a string using `\()`.

```swift
let age = 25
let message = "I am \(age) years old."  // Outputs: I am 25 years old.
```

### **String Concatenation:**
You can join two strings together using the `+` operator.

```swift
let firstName = "John"
let lastName = "Doe"
let fullName = firstName + " " + lastName
```

### **Common String Methods:**
- `.isEmpty`: Check if a string is empty.
- `.count`: Get the number of characters.
- `.uppercased() / .lowercased()`: Convert to uppercase or lowercase.

```swift
let text = "Swift"
print(text.isEmpty)            // false
print(text.count)              // 5
print(text.uppercased())       // SWIFT
print(text.lowercased())       // swift
```

---

## 2. **Collections**
Swift provides three main collection types: **Arrays**, **Dictionaries**, and **Sets**. These are used to group values together.

### **Arrays**:
Arrays are ordered collections of values, where each value is of the same type.

**Creating an Array:**
```swift
var fruits: [String] = ["Apple", "Banana", "Cherry"]
var numbers = [1, 2, 3, 4, 5]  // Type inference
```

**Array Operations:**
- Add an element: `fruits.append("Orange")`
- Access an element: `fruits[0]`  // Apple
- Modify an element: `fruits[1] = "Blueberry"`
- Remove an element: `fruits.remove(at: 2)`

**Iteration:**
```swift
for fruit in fruits {
    print(fruit)
}
```

---

### **Dictionaries**:
Dictionaries store key-value pairs, where each key is unique and maps to a value.

**Creating a Dictionary:**
```swift
var studentGrades: [String: Int] = ["Alice": 90, "Bob": 85, "Charlie": 78]
```

**Dictionary Operations:**
- Access a value: `studentGrades["Alice"]`  // Optional(90)
- Add or modify a value: `studentGrades["David"] = 88`
- Remove a key-value pair: `studentGrades.removeValue(forKey: "Bob")`

### **Sets**:
Sets are unordered collections of unique values.

**Creating a Set:**
```swift
var uniqueNumbers: Set<Int> = [1, 2, 3, 3, 4]  // No duplicates
print(uniqueNumbers)  // {1, 2, 3, 4}
```

**Set Operations:**
- Add an element: `uniqueNumbers.insert(5)`
- Remove an element: `uniqueNumbers.remove(1)`
- Check if a set contains a value: `uniqueNumbers.contains(3)`

---

## 3. **Structs**
A **struct** is a custom data type that allows you to encapsulate related properties and behavior. Structs are **value types**, meaning they are copied when passed around.

### **Defining a Struct:**
```swift
struct Book {
    let title: String
    let author: String
    var isRead: Bool

    // Method (behavior)
    func description() -> String {
        return "\(title) by \(author)"
    }
    
    // Mutating method
    mutating func markAsRead() {
        isRead = true
    }
}
```

### **Using a Struct:**
```swift
var book1 = Book(title: "1984", author: "George Orwell", isRead: false)
print(book1.description())  // 1984 by George Orwell

book1.markAsRead()
print(book1.isRead)  // true
```

### Key Points:
- **Immutable Properties:** If you declare properties with `let`, you cannot modify them after initializing the struct.
- **Value Types:** When a struct is passed to a function or assigned to another variable, it is **copied**, not shared.

---

## 4. **Classes**
Classes are similar to structs, but they are **reference types**, meaning they are passed by reference and not copied when assigned or passed around.

### **Defining a Class:**
```swift
class Car {
    var brand: String
    var year: Int
    var isRunning: Bool

    init(brand: String, year: Int) {
        self.brand = brand
        self.year = year
        self.isRunning = false
    }
    
    // Method (behavior)
    func start() {
        isRunning = true
        print("\(brand) has started.")
    }

    func stop() {
        isRunning = false
        print("\(brand) has stopped.")
    }
}
```

### **Using a Class:**
```swift
let myCar = Car(brand: "Tesla", year: 2022)
myCar.start()  // Tesla has started.
myCar.stop()   // Tesla has stopped.
```

### **Reference Types:**
Classes are passed by **reference**, meaning if you assign one class instance to another variable, they both reference the same object.

```swift
let car1 = Car(brand: "Ford", year: 2020)
let car2 = car1  // car2 refers to the same Car instance as car1

car2.start()
print(car1.isRunning)  // true, because car2 and car1 refer to the same object
```

### **Inheritance:**
Classes support inheritance, allowing one class to inherit properties and methods from another.

```swift
class ElectricCar: Car {
    var batteryLevel: Int
    
    init(brand: String, year: Int, batteryLevel: Int) {
        self.batteryLevel = batteryLevel
        super.init(brand: brand, year: year)
    }
    
    func chargeBattery() {
        batteryLevel = 100
        print("Battery fully charged.")
    }
}
```

---

### **Summary of Key Differences Between Structs and Classes:**
| **Aspect**           | **Struct**                 | **Class**                |
|----------------------|----------------------------|--------------------------|
| **Type**             | Value Type                 | Reference Type           |
| **Inheritance**      | No                         | Yes                      |
| **Mutability**       | Immutable unless marked `var` | Can modify properties at will |
| **Copied or Shared** | Copied when passed or assigned | Shared (reference passed) |

---

### **Practical Example Combining Structs and Collections:**

```swift
struct Movie {
    let title: String
    let director: String
}

var movies: [Movie] = [
    Movie(title: "Inception", director: "Christopher Nolan"),
    Movie(title: "Parasite", director: "Bong Joon-ho")
]

for movie in movies {
    print("\(movie.title) directed by \(movie.director)")
}
```

This example shows how to create an array of custom `Movie` objects, and then iterate over them using a `for` loop.

---

