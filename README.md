# Swift Cheat Sheet

---

## 1. Variables & Constants

```swift
var name = "John"        // mutable
let pi = 3.14            // immutable (constant)

var x: Int = 5           // explicit type
var y: Double = 5        // must declare Double explicitly for decimals
var z: String = "hello"
```

---

## 2. Strings

```swift
let s = "hello world"

// Length
s.count                          // 11

// First / Last character
s.first                          // "h"
s.last                           // "d"

// Indexing (Swift uses Index, not Int)
let idx = s.index(s.startIndex, offsetBy: 3)
s[idx]                           // "l"  (4th character)

// Slicing - first N characters
let first3 = s.prefix(3)        // "hel"

// Slicing - last N characters
let last3 = s.suffix(3)         // "rld"

// Reversed
String(s.reversed())             // "dlrow olleh"
String(s.suffix(3).reversed())  // "dlr"

// Split into words
let words = s.split(separator: " ")   // ["hello", "world"]
words[1]                               // "world"

// String interpolation
let age = 25
let msg = "I am \(age) years old"

// Contains
s.contains("hello")              // true

// Replace
s.replacingOccurrences(of: "hello", with: "bye")
```

---

## 3. Optionals

```swift
var value: Int? = nil       // optional Int
var name: String? = "John"

// Unwrap with if let
if let unwrapped = name {
    print(unwrapped)
}

// Unwrap with guard
func greet(_ name: String?) {
    guard let name = name else { return }
    print("Hello \(name)")
}

// Nil coalescing
let result = name ?? "default"

// Force unwrap (use carefully)
print(name!)
```

---

## 4. Control Flow

```swift
// if / else
if x > 5 {
    print("big")
} else if x == 5 {
    print("five")
} else {
    print("small")
}

// switch (must be exhaustive)
switch x {
case 1:
    print("one")
case 2, 3:
    print("two or three")
case 4...10:
    print("four to ten")
default:
    print("other")
}

// Ternary
let label = x > 5 ? "big" : "small"
```

---

## 5. Loops

```swift
// for-in range
for i in 1...5 { print(i) }        // 1 2 3 4 5
for i in 1..<5 { print(i) }        // 1 2 3 4

// for-in array
let arr = [10, 20, 30]
for item in arr { print(item) }

// for-in with index
for (index, item) in arr.enumerated() {
    print("\(index): \(item)")
}

// while
var i = 0
while i < 5 { i += 1 }
```

---

## 6. Arrays

```swift
var arr: [Int] = [1, 2, 3]
var arr2 = ["a", "b", "c"]       // type inferred

arr.count                         // 3
arr[0]                            // 1  (first item)
arr[1]                            // 2  (second item)
arr.first                         // Optional(1)
arr.last                          // Optional(3)

// Add / Remove
arr.append(4)
arr.insert(0, at: 0)
arr.remove(at: 1)

// Search
arr.contains(2)                   // true
arr.firstIndex(of: 2)            // Optional(1)

// Sorting
arr.sorted()                      // ascending
arr.sorted(by: >)                 // descending

// Higher-order functions
arr.map { $0 * 2 }                // [2, 4, 6]
arr.filter { $0 > 1 }            // [2, 3]
arr.reduce(0) { $0 + $1 }       // sum = 6
arr.forEach { print($0) }
```

---

## 7. Dictionaries

```swift
var dict: [String: Int] = ["A": 1, "B": 2]
var dict2 = ["x": 10, "y": 20]       // type inferred

// Access (returns Optional)
dict["A"]                             // Optional(1)
dict["A"] ?? 0                        // 1 (with default)

// Add / Update
dict["C"] = 3
dict["A"] = 99

// Remove
dict.removeValue(forKey: "B")
dict["B"] = nil

// Iterate
for (key, value) in dict {
    print("\(key): \(value)")
}

// Keys and Values
dict.keys                            // ["A", "B", "C"]
dict.values                          // [1, 2, 3]

// Filter
let filtered = dict.filter { $0.value >= 2 }

// Mixed type dictionary
var mixed: [String: Any] = ["name": "John", "age": 25]
let name = mixed["name"] as? String  // cast back to String
```

---

## 8. Tuples

```swift
// Declaration
let point = (x: 0, y: 5)
let fraction = (1, 2)              // unnamed

// Access
point.x                            // 0
fraction.0                         // 1

// Return tuple from function
func minMax(arr: [Int]) -> (min: Int, max: Int) {
    return (arr.min()!, arr.max()!)
}
let result = minMax(arr: [1, 3, 5])
result.min                          // 1
result.max                          // 5
```

---

## 9. Functions

```swift
// Basic
func greet(name: String) -> String {
    return "Hello \(name)"
}
greet(name: "John")

// Argument label vs parameter name
func greet(to name: String) -> String {     // "to" is the label, "name" is internal
    return "Hello \(name)"
}
greet(to: "John")

// Omit label with underscore
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}
add(1, 2)

// Default parameter
func power(_ base: Int, exponent: Int = 2) -> Int {
    return Int(pow(Double(base), Double(exponent)))
}
power(3)          // 9
power(3, exponent: 3)   // 27

// Multiple return values (tuple)
func divide(_ a: Int, _ b: Int) -> (quotient: Int, remainder: Int) {
    return (a / b, a % b)
}
```

---

## 10. Closures

```swift
// Full syntax
let square: (Int) -> Int = { (n: Int) -> Int in
    return n * n
}

// Shorthand
let square2: (Int) -> Int = { $0 * $0 }

// As argument
[1, 2, 3].map { $0 * 2 }           // [2, 4, 6]
[1, 2, 3].filter { $0 > 1 }       // [2, 3]
[1, 2, 3].sorted { $0 > $1 }      // [3, 2, 1]
```

---

## 11. Enums

```swift
// Basic enum
enum Direction {
    case north, south, east, west
}
let dir = Direction.north

// Enum in switch
switch dir {
case .north: print("Going north")
case .south: print("Going south")
case .east:  print("Going east")
case .west:  print("Going west")
}

// Raw values
enum CoinType: Int {
    case penny = 1
    case nickel = 5
    case dime = 10
    case quarter = 25
}
CoinType.dime.rawValue             // 10

// Associated values
enum Shape {
    case circle(radius: Double)
    case square(side: Double)
}
let s = Shape.circle(radius: 5.0)

switch s {
case .circle(let r):  print("Circle: \(Double.pi * r * r)")
case .square(let s):  print("Square: \(s * s)")
}
```

---

## 12. Classes & Structs

```swift
// Struct (value type)
struct Person {
    var name: String
    var age: Int
}
var p = Person(name: "John", age: 30)
p.name                              // "John"

// Class (reference type)
class User {
    var nickname: String
    var email: String
    var password: String

    // Default initializer
    init() {
        self.nickname = ""
        self.email = ""
        self.password = ""
    }

    // Custom initializer
    init(nickname: String, email: String, password: String) {
        self.nickname = nickname
        self.email = email
        self.password = password
    }

    // Method
    func describe() -> String {
        return "\(nickname) (\(email))"
    }
}

let user = User(nickname: "johnny", email: "j@gmail.com", password: "1234")
```

---

## 13. Extensions

```swift
// Extend a built-in type
extension String {
    func vowels() -> String {
        return self.filter { "aeiouAEIOU".contains($0) }
    }
}
"Hello".vowels()                   // "eo"

// Extend Array with constraint
extension Array where Element == Int {
    func sum() -> Int {
        return self.reduce(0, +)
    }

    func toStringArray() -> [String] {
        return self.map { String($0) }
    }
}
[1, 2, 3].sum()                    // 6
[1, 2, 3].toStringArray()         // ["1", "2", "3"]

// Extend Array with any Element
extension Array {
    func totalCharacterCount() -> Int where Element == String {
        return self.reduce(0) { $0 + $1.count }
    }
}
```

---

## 14. Higher-Order Functions (map / filter / reduce / sorted)

```swift
let nums = [1, 2, 3, 4, 5]

// map - transform each element
nums.map { $0 * 2 }                // [2, 4, 6, 8, 10]

// filter - keep matching elements
nums.filter { $0 % 2 == 0 }       // [2, 4]

// reduce - combine to single value
nums.reduce(0, +)                  // 15
nums.reduce(0) { $0 + $1 }       // 15

// sorted
nums.sorted()                      // [1, 2, 3, 4, 5]
nums.sorted(by: >)                 // [5, 4, 3, 2, 1]

// Chaining
nums.filter { $0 > 2 }.map { $0 * 10 }   // [30, 40, 50]

// forEach
nums.forEach { print($0) }

// compactMap - map + remove nils
let strs = ["1", "two", "3"]
strs.compactMap { Int($0) }       // [1, 3]

// max / min with keyPath on structs
struct Person { var name: String; var age: Int }
let people = [Person(name: "A", age: 30), Person(name: "B", age: 25)]
people.max(by: { $0.age < $1.age })?.name    // "A"
```

---

## 15. Date

```swift
import Foundation

let now = Date()

// Extension to get year
extension Date {
    var year: Int {
        return Calendar.current.component(.year, from: self)
    }
}
now.year       // e.g. 2025
```

---

## 16. Useful Patterns

```swift
// Frequency count
let arr = [1, 2, 2, 3, 3, 3]
var freq: [Int: Int] = [:]
for n in arr {
    freq[n, default: 0] += 1
}
// freq = [1: 1, 2: 2, 3: 3]

// Sort dictionary by key
freq.sorted(by: { $0.key < $1.key })

// Max in dictionary by value
freq.max(by: { $0.value < $1.value })

// Merge two dictionaries
var d1 = ["A": 1, "B": 2]
let d2 = ["B": 3, "C": 4]
for (key, value) in d2 {
    d1[key, default: 0] += value
}
// d1 = ["A": 1, "B": 5, "C": 4]

// Average of array
let ratings = [8, 9, 10]
let avg = Double(ratings.reduce(0, +)) / Double(ratings.count)
```
