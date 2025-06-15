# 🧠 Constants, Variables, Strings & Integers in Swift
<br/>

## 🔐 Constants  
Constants are **immutable** — once set, their value **cannot be changed**.

```swift
let myName = "Grant"
```

```swift
let age = 25
age = 30 // ❌ Error: Cannot change a constant
```
<br/>

## 🔁 Variables  
Variables are **mutable** — their value **can change** over time.

```swift
var myJob = "Pilot"
myJob = "Captain"
```
<br/>

## 🧵 Strings  
Strings are used to store **text values** like words or sentences.



### ✨ String Tricks

#### 1. Quotes inside a string
```swift
let review = "My favorite movie is \"The Martian\"."
```

#### 2. Multiline strings
```swift
let haiku = """
I like poems
but I'm not very
good at them.
"""
```

#### 3. String interpolation
```swift
let greeting = "Hi, my name is \(myName)."
```

#### 4. Count characters (includes spaces)
```swift
let myName = "Grant"
myName.count // ➡️ returns 5
```

#### 5. Read prefix and suffix
```swift
let dinosaur = "velociraptor"
dinosaur.hasPrefix("Veloci") // ❌ false (V ≠ v)
dinosaur.hasSuffix("raptor") // ✅ true
```
<br/>

## 🔢 Integers

An **integer** (or `Int`) is a whole number — no decimals.

Examples:  
`-5`, `0`, `42`, `100000`



### 🧮 Integer Tricks

#### 1. Common operations
```swift
let a = 10
let b = 3

let sum = a + b         // 13
let difference = a - b  // 7
let product = a * b     // 30
let quotient = a / b    // 3
let remainder = a % b   // 1
```

#### 2. Check for multiples
```swift
let number = 9
number.isMultiple(of: 3) // ✅ true
```

#### 3. Generate a random number
```swift
let randomNumber = Int.random(in: 1...100)
```
<br/>

# Booleans
<br/>

## Booleans
store true/false conditions.

```swift
let isAwake = true
isAwake.toggle() // ➡️ false
```
<br/>

# 🧱 Arrays, Sets, Dictionaries & Enumerations
<br/>

## 📚 Arrays

Arrays are data types with the ability to store multiple items. They are ordered and can contain duplicates.

```swift
var pets = ["Murphy", "Hiro", "Milkshakes", "Sasha"]
pets[0]    // ➡️ returns "Murphy"
```
#### Empty arrays

```swift
var vehicles = [String]()     
var vehicles = Array<String>()  
var vehicles: [String] = []     
```
<br/>

### 🧰 Toolbox: Arrays

#### 1. Add an item
```swift
pets.append("Amanda Trash Panda") // ➡️ adds to end
```

#### 2. Remove item(s)
```swift
pets.remove(at: 0)    // ➡️  removes "Murphy"
pets.removeAll()      // ➡️  clears all items
```

#### 3. Count items
```swift
pets.count            // ➡️  returns number of items
```

#### 4. Check if it contains something
```swift
pets.contains("Fido") // ❌  false
```

#### 5. Sort array
```swift
let letters = ["c", "a", "e", "b", "d"]
letters.sorted() // ➡️  ["a", "b", "c", "d", "e"]
```

#### 6. Reverse array
```swift
letters.reversed()    // ➡️  ReversedCollection(["c", "a", "e", "b", "d"])
```
💡 Creates a reversed collection without modifying original.

<br/>



## 🟢 Sets

Sets are unordered collections of elements that do not contain duplicates. 

```swift
var colors: Set<String> = ["red", "green", "blue"]
```

#### Empty sets

```swift
var emptySet = Set<String>() // Type inference
var emptySet: Set<Int> = []  // Type annotation
```
<br/>

### 🧰 Toolbox: Sets

#### 1. Insert
```swift
colors.insert("yellow")       // ➡️  adds if not present
```

#### 2. Check for presence
```swift
colors.contains("green")      // ✅  true
colors.contains("purple")     // ❌  false
```

#### 3. Count
```swift
colors.count                  // ➡️  number of unique items
```

#### 4. Remove item
```swift
colors.remove("red")          // ➡️  removes "red" if it exists
```

#### 5. Sort
```swift
colors.sorted()               // ➡️ ["blue", "green", "red"]
```

#### 5. Convert array to set
```swift
let array = ["a", "b", "a"]
let setFromArray = Set(array) // ➡️  {"a", "b"}
```

<br/>

## 📒 Dictionaries

Dictionaries have the ability to contain multiple values. They are called with the dictionary *key*.

```swift
let employee = [
    "name": "Taylor Swift",
    "job": "Singer",
    "location": "Nashville"
]

employee["name"]                              // ➡️  Taylor Swift
print(employee["name"])                       // ➡️  Optional("Taylor Swift")
print(employee["age"])                        // ❌  nil (no key "age")
print(employee["name", default: "Unknown"])   // ➡️  "Taylor Swift"
```
- When name is called by a function, there is no guarantee that a value exists. It is an *optional*. The default values guarantees a value to the key.

#### Empty dictionaries

```swift
var emptyDictionary = [String: String]() // Type inference
var emptyDictionary: [Int: Int] = [:]    // Type annotation   
```

<br/>

### 🧰 Toolbox: Dictionaries

#### 1. "Inserting" assigning values to a key
```swift
employee["hair"] = "blonde"
```

#### 2. Count 
```swift
employee.count // ➡️ 3
```

#### 3. Remove
```swift
employee.removeAll()
```
<br/>

## 🧩 Enumerations

```swift
enum Weekdays {
    case monday, tuesday, wednesday, thursday, friday
}

var day = Weekdays.monday
day = .tuesday
```

#### Notes
- Enum types use **UpperCamelCase**
- Cases use **lowerCamelCase** by convention
- Shortens access: `.tuesday` is valid after `day` is declared as a `Weekdays`

<br/>
