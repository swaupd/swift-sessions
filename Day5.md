### **Guard Statements**

In Swift, `guard` statements provide a way to conditionally exit early from a function, loop, or closure if a certain condition is not met. They allow you to "guard" your code by checking for invalid states at the beginning and exiting early if needed, keeping the rest of your code cleaner and less nested.

---

#### **Why Use `guard`?**

The primary use of a `guard` statement is for **early exits**. If a condition isn't met, you can exit the current block (function, loop, etc.) immediately, avoiding deeply nested `if` statements and improving readability.

**Key points:**
- `guard` statements must always exit the scope when the condition fails (with `return`, `continue`, `break`, `throw`, or even `fatalError`).
- The variables unwrapped or initialized in a `guard` statement are available in the rest of the function or scope, unlike in an `if let` statement, where they are only accessible within the `if` block.

---

#### **Syntax of `guard`**

```swift
guard condition else {
    // Exit the scope (return, break, continue, throw, etc.)
}
```

If the `condition` evaluates to `false`, the code inside the `else` block is executed, and the current scope is exited. If the condition is `true`, execution continues beyond the `guard`.

---

#### **Using `guard` for Optional Binding**

One common use case of `guard` is optional binding. You can use `guard let` to unwrap an optional and safely use it throughout the rest of the function.

```swift
func greet(person: String?) {
    guard let name = person else {
        print("No name provided.")
        return
    }
    print("Hello, \(name)!")
}
```

In this example:
- If `person` is `nil`, the `guard` block exits early, and the function doesn’t continue.
- If `person` is not `nil`, `name` is unwrapped and can be used throughout the function.

---

#### **Multiple Conditions with `guard`**

You can use multiple conditions in a single `guard` statement by separating them with commas.

```swift
func process(user: String?, age: Int?) {
    guard let username = user, let userAge = age, userAge > 18 else {
        print("Invalid user or age.")
        return
    }
    print("\(username) is \(userAge) years old and can proceed.")
}
```

Here, multiple conditions are checked:
- Both `user` and `age` are unwrapped.
- The `userAge` must be greater than 18.
- If any condition fails, the function exits early.

---

#### **Guard in Loops**

You can use `guard` inside loops to skip iterations that don't meet certain criteria.

```swift
for number in 1...10 {
    guard number % 2 == 0 else {
        continue  // Skip odd numbers
    }
    print("\(number) is even.")
}
```

In this example, the loop skips odd numbers using `continue` when the `guard` condition fails.

---

#### **Comparison of `guard` and `if let`**

`guard let` and `if let` both handle optional unwrapping, but their usage differs:

- `if let` is typically used when the logic splits based on whether the optional contains a value.
- `guard let` is used to exit early, allowing you to avoid unnecessary nesting and keep the main logic of your function more readable.

Example comparison:

```swift
// Using if let (nested logic)
func greet(person: String?) {
    if let name = person {
        print("Hello, \(name)!")
    } else {
        print("No name provided.")
    }
}

// Using guard let (early exit)
func greet(person: String?) {
    guard let name = person else {
        print("No name provided.")
        return
    }
    print("Hello, \(name)!")
}
```

In the second example, `guard` avoids the nested structure, making the code more readable.

---

### **Constant and Variable Scope**

In Swift, the **scope** of a constant or variable defines where it can be accessed within the program. Scope is determined by the block (or context) in which the variable is declared. Blocks in Swift include functions, loops, conditionals, and global or file-level code.

---

#### **1. Global Scope**

Constants and variables declared at the top level of a Swift file (outside of any functions or classes) are in the **global scope**. They can be accessed from anywhere in the file and sometimes across other files if they are not marked private.

```swift
let globalConstant = "I'm accessible everywhere in this file"

func printGlobal() {
    print(globalConstant)
}
```

Here, `globalConstant` is declared globally and can be accessed within the `printGlobal` function.

---

#### **2. Function Scope**

Variables declared within a function are accessible only within that function. Once the function ends, the variables go out of scope, and their memory is deallocated.

```swift
func calculate() {
    let result = 42
    print("Result inside function: \(result)")
}

calculate()
print(result)  // Error: result is not accessible outside calculate()
```

Here, `result` is in the scope of the `calculate` function and is not accessible outside the function.

---

#### **3. Loop Scope**

Variables declared inside a loop are local to the loop and cannot be accessed outside of it.

```swift
for i in 1...3 {
    let temp = "Temp \(i)"
    print(temp)
}

print(temp)  // Error: temp is not accessible outside the loop
```

`temp` is declared inside the `for` loop, so it’s only accessible inside that loop.

---

#### **4. Conditional Scope**

Similarly, constants and variables declared inside conditional statements (`if`, `guard`, `switch`) are local to those blocks.

```swift
if true {
    let condition = "True"
    print(condition)
}

print(condition)  // Error: condition is not accessible outside the if block
```

The constant `condition` is scoped to the `if` block and cannot be accessed outside of it.

---

#### **Best Practices for Scope:**

1. **Use local variables whenever possible**: This limits their visibility and avoids potential conflicts with other variables in the program.
2. **Be cautious with global variables**: They are available throughout the program, which increases the chance of accidental modification from different parts of the code.
3. **Minimize the use of large function scope**: Declare variables close to where you need them to make the code more readable and reduce the chance of errors.
4. **Guard statements** are great for ensuring that a value exists early on in a function, keeping the core logic clean and safe from optional unwrapping errors.

---


### **Enumerations (Enums) in Swift**

Enums in Swift are a powerful feature that allows you to define a group of related values in a **type-safe** way. Enumerations are much more flexible in Swift compared to other languages, and they can be extended to have associated values, methods, computed properties, and even initializers.

---

### **Basic Enumeration Syntax**

In its simplest form, an enumeration in Swift defines a set of related values (usually cases that fall under a specific category).

```swift
enum CompassDirection {
    case north
    case south
    case east
    case west
}
```

Here, `CompassDirection` is the name of the enumeration, and it contains four possible values (`north`, `south`, `east`, `west`), referred to as **cases**.

---

#### **How to Use an Enum**

To use an enum value, you can assign it to a variable or constant and access the cases using the dot (`.`) notation:

```swift
var direction = CompassDirection.north

// Once the type is known, you can omit the enum name
direction = .west
```

Enums are **type-safe**, so `direction` can only hold values that are part of the `CompassDirection` enum.

---

### **Iterating Over Enum Cases**

To iterate over the cases of an enum, you can make the enum conform to the `CaseIterable` protocol, which automatically provides a collection of all the cases.

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice, water
}

for drink in Beverage.allCases {
    print(drink)
}
```

This will print:
```
coffee
tea
juice
water
```

---

### **Associated Values**

Enums in Swift can store **associated values**. This means each case can have additional data attached to it, which can be different for each case. This feature is useful when you want to associate specific data with certain enum cases.

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```

In the `Barcode` enum:
- The `upc` case has four `Int` values associated with it.
- The `qrCode` case has a `String` associated with it.

You can assign a value to an enum case with associated values like this:

```swift
var productCode = Barcode.upc(8, 85909, 51226, 3)
productCode = .qrCode("XYZ12345")
```

To retrieve the associated values, you can use a `switch` statement:

```swift
switch productCode {
case .upc(let numberSystem, let manufacturer, let product, let check):
    print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
case .qrCode(let code):
    print("QR Code: \(code)")
}
```

Using `let` (or `var`) with `switch` allows you to extract the associated values for each case.

---

### **Raw Values**

Enums can also have **raw values**, which are fixed values that each case has. These raw values must all be of the same type (such as `Int`, `String`, etc.), and Swift automatically assigns them if you don't provide a value explicitly.

#### **Example with Raw Values**

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

In this example:
- `mercury` is explicitly assigned the raw value `1`.
- The other planets automatically get the next values (`venus = 2`, `earth = 3`, etc.).

You can access the raw value like this:

```swift
let planet = Planet.earth
print(planet.rawValue)  // Prints: 3
```

#### **Initializing from a Raw Value**

You can create an enum instance from a raw value using an initializer:

```swift
let possiblePlanet = Planet(rawValue: 5)
print(possiblePlanet)  // Prints: Optional(Planet.jupiter)
```

Since this initializer returns an optional (because the raw value might not correspond to a valid case), it’s important to check whether the value was successfully converted:

```swift
if let somePlanet = Planet(rawValue: 9) {
    print(somePlanet)
} else {
    print("No such planet exists.")
}
```

---

### **Methods and Properties in Enums**

Enums in Swift can also have instance methods, computed properties, and initializers. This allows enums to encapsulate functionality, similar to structs or classes.

#### **Enum with Methods**

```swift
enum TrafficLight {
    case red, yellow, green

    func action() -> String {
        switch self {
        case .red:
            return "Stop"
        case .yellow:
            return "Caution"
        case .green:
            return "Go"
        }
    }
}
```

Here, the `TrafficLight` enum has an `action()` method that provides a message depending on the current light color:

```swift
let light = TrafficLight.red
print(light.action())  // Prints: Stop
```

---

### **Enum with Computed Properties**

You can also add computed properties to enums, just like you can with structs or classes.

```swift
enum Vehicle {
    case car, bicycle, airplane

    var description: String {
        switch self {
        case .car:
            return "A car has 4 wheels."
        case .bicycle:
            return "A bicycle has 2 wheels."
        case .airplane:
            return "An airplane flies in the sky."
        }
    }
}

let myVehicle = Vehicle.bicycle
print(myVehicle.description)  // Prints: A bicycle has 2 wheels.
```

---

### **Enum with Initializers**

Enums can also have **initializers**, which allows you to control how an enum instance is created.

```swift
enum Temperature {
    case celsius(Double)
    case fahrenheit(Double)

    init(fromKelvin kelvin: Double) {
        if kelvin < 0 {
            self = .celsius(0)
        } else {
            self = .celsius(kelvin - 273.15)
        }
    }
}

let temperature = Temperature(fromKelvin: 300)
print(temperature)  // Prints: celsius(26.850000000000023)
```

---

### **Enums as Type-safe Flags**

One interesting use case for enums is representing type-safe flags. For example, when you have several distinct states or modes for a system, enums can help prevent invalid states and clarify intent.

```swift
enum NetworkConnection {
    case connected, disconnected, connecting
}

var connectionStatus = NetworkConnection.connected
connectionStatus = .connecting  // This is valid

// Using an enum ensures invalid states (like connectionStatus = "Lost") don't occur.
```

Enums offer a **type-safe** alternative to using simple integers or strings to represent states, preventing invalid values from being assigned.

---

### **Mutating Methods in Enums**

By default, enums in Swift are value types (like structs), so their cases cannot be changed from within their methods. However, if you mark a method with the `mutating` keyword, you can modify the enum’s case inside the method.

```swift
enum ToggleSwitch {
    case on, off

    mutating func toggle() {
        self = (self == .on) ? .off : .on
    }
}

var switchState = ToggleSwitch.off
switchState.toggle()
print(switchState)  // Prints: on
```

Here, the `toggle` method changes the enum's case from `.on` to `.off` and vice versa.

---

### **Recap of Key Features:**

1. **Basic Enums**: Define a list of related cases.
2. **Associated Values**: Store additional information per case.
3. **Raw Values**: Cases can store a fixed raw value of a specified type.
4. **Methods & Properties**: Enums can have instance methods, computed properties, and initializers.
5. **Mutating Methods**: Modify an enum's case from within a method.
6. **Type-safe Flags**: Enums prevent invalid states and ensure type safety.

---

### **Enums in Swift: Powerful and Flexible**

Swift enums are more than just simple collections of related values. They provide significant flexibility, allowing you to associate values, define methods, compute properties, and encapsulate logic. This makes enums in Swift more expressive and powerful compared to enums in many other programming languages.
