# Swift Exam Cheat Sheet

---

## Variables & Types
```swift
var x = 5               // mutable
let y = 10              // constant
var d: Double = 1.2
var s: String = "hello"
```

---

## String Basics
```swift
let s = "my string"
s.count                          // 9
s.first                          // "m"
s[s.index(s.startIndex, offsetBy: 3)]  // 4th char = "s"
s.prefix(3)                      // "my "
s.suffix(3)                      // "ing"
String(s.suffix(3).reversed())  // "gni"
s.split(separator: " ")[1]      // "string" (2nd word)
"\(x) and \(s)"                 // interpolation
s.contains("my")                // true
```

---

## Arrays
```swift
var arr = ["a", "b", "c"]
arr.count                        // 3
arr[1]                           // "b"
arr.append("d")
arr.contains("a")                // true
arr.firstIndex(of: "b")         // Optional(1)
arr.sorted()
arr.map { $0.uppercased() }     // ["A", "B", "C"]
arr.filter { $0 != "a" }        // ["b", "c"]
arr.reduce(0) { $0 + $1 }      // sum (for Int arrays)
```

---

## Dictionaries
```swift
var dict: [String: Int] = ["A": 1, "B": 2]

dict["A"]                        // Optional(1)
dict["A"] ?? 0                   // 1
dict["C"] = 3                    // add
dict["A"] = nil                  // remove

for (key, value) in dict { }

// Filter
dict.filter { $0.value >= 2 }

// Count with default
var freq: [Int: Int] = [:]
freq[n, default: 0] += 1

// Mixed type
var d: [String: Any] = ["name": "John", "score": 10]
d["name"] as? String             // cast back
d["score"] as? Int
```

---

## Control Flow
```swift
if x > 5 { } else { }

switch x {
case 1:       print("one")
case 2, 3:    print("two or three")
default:      print("other")
}

for i in 1...5 { }              // 1 to 5
for i in 1..<5 { }             // 1 to 4
for item in arr { }
for (i, item) in arr.enumerated() { }
while x > 0 { x -= 1 }
```

---

## Functions
```swift
// label + name + type -> return
func removeLow(from dict: [String: Int], threshold: Int) -> [String: Int] {
    return dict.filter { $0.value >= threshold }
}

// No label with _
func add(_ a: Int, _ b: Int) -> Int { return a + b }
add(1, 2)

// Tuple return
func frac() -> (Int, Int) { return (1, 2) }
```

---

## Enums
```swift
enum Direction { case north, south, east, west }

// Raw value
enum CoinType: Int {
    case penny = 1
    case nickel = 5
    case quarter = 25
}
CoinType.quarter.rawValue        // 25

// Associated value
enum Shape {
    case circle(radius: Double)
    case square(side: Double)
}

// Use in switch
switch dir {
case .north: print("North")
case .south: print("South")
case .east:  print("East")
case .west:  print("West")
}

switch shape {
case .circle(let r): print(Double.pi * r * r)
case .square(let s): print(s * s)
}
```

---

## Tuples
```swift
var location = (x: 0, y: 0)
location.x += 1
location.y -= 1

let fraction = (1, 2)           // numerator, denominator
fraction.0                       // 1
fraction.1                       // 2
```

---

## Classes
```swift
class User {
    var nickname: String
    var email: String

    init() {                     // default
        nickname = ""
        email = ""
    }

    init(nickname: String, email: String) {
        self.nickname = nickname
        self.email = email
    }
}
```

---

## Extensions
```swift
extension String {
    func vowels() -> String {
        return self.filter { "aeiou".contains($0) }
    }
}
"hello".vowels()                 // "eo"

extension Array where Element == Int {
    func sum() -> Int { return self.reduce(0, +) }
}
[1,2,3].sum()                   // 6

extension Array where Element == String {
    func totalCharacterCount() -> Int {
        return self.reduce(0) { $0 + $1.count }
    }
}
```

---

## map / filter / reduce / sorted
```swift
let nums = [1, 2, 3, 4, 5]

nums.map { $0 * 2 }             // [2,4,6,8,10]
nums.filter { $0 > 2 }         // [3,4,5]
nums.reduce(0, +)               // 15
nums.sorted(by: >)              // [5,4,3,2,1]
nums.forEach { print($0) }

// On structs
people.max(by: { $0.age < $1.age })
people.sorted { $0.salary > $1.salary }
people.map { $0.nickname }      // ["alice", "bob"]
```

---

## joined
```swift
["a", "b", "c"].joined()               // "abc"
["a", "b", "c"].joined(separator: ", ") // "a, b, c"

// map + joined (very common)
[1, 2, 3].map { String($0) }.joined(separator: " ")  // "1 2 3"
dict.map { "\($0.key): \($0.value)" }.joined(separator: ", ")
```

---

## Type Casting
```swift
mixed["name"] as? String        // Optional("John")
mixed["score"] as? Int          // Optional(10)
Double(5)                       // 5.0
Int(3.9)                        // 3
String(42)                      // "42"
Int("42")                       // Optional(42)
```

---

## Useful Patterns

```swift
// Frequency count
var freq: [Int: Int] = [:]
for n in numbers { freq[n, default: 0] += 1 }
freq.sorted { $0.key < $1.key }  // sorted by key

// Average
let avg = Double(arr.reduce(0, +)) / Double(arr.count)

// Max by value in dict
freq.max { $0.value < $1.value }

// Merge dicts (add values for shared keys)
for (key, val) in d2 { d1[key, default: 0] += val }

// Filter dict below threshold
dict.filter { $0.value >= threshold }

// String encode with dict
let encoded = message.map { code[String($0)] ?? String($0) }.joined()
```
