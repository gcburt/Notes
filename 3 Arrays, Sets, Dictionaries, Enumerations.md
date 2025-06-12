# 🧱 Arrays, Sets, Dictionaries & Enumerations
<br/>

## 📚 Arrays

Arrays are data types with the ability to store multiple items. They are ordered and can contain duplicates.

```swift
var pets = ["Murphy", "Hiro", "Milkshakes", "Sasha"]
pets[0]    // ➡️ returns "Murphy"
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

#### 7. Empty arrays
```swift
var vehicles = [String]()     
var vehicles = Array<String>()  
var vehicles: [String] = []     
```
<br/>



## 🟢 Sets

Sets are unordered collections of elements that do not contain duplicates. 

```swift
var colors: Set<String> = ["red", "green", "blue"]
```

#### Creating empty sets

```swift
var emptySet = Set<String>() // Type inferance
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

#### Assigning values to a key
```swift
employee["hair"] = "blonde"
```

#### Create empty dictionaries

```swift
var emptyDictionary = [String: String]() // Type inferance
var emptyDictionary: [Int: Int] = [:]    // Type annotation   
```

<br/>

### 🧰 Toolbox: Dictionaries

#### 1. Count 
```swift
employee.count // ➡️ 3
```

#### 2. Remove
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

