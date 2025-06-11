# 🧱 Arrays, Sets, Dictionaries & Enumerations
<br/>

## 📚 Arrays

Arrays are data types with the ability to store multiple items.

```swift
var pets = ["Murphy", "Hiro", "Milkshakes", "Sasha"]
```
### ✨ Array Tricks

#### 1. Add an item
```swift
pets.append("Amanda Trash Panda") // ➡️ adds to end
pets[0]                           // ➡️ returns "Murphy"
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
letters.sorted()      // ➡️  ["a", "b", "c", "d", "e"]
```

#### 6. Reverse array
```swift
letters.reversed()    // ➡️  ReversedCollection(["c", "a", "e", "b", "d"])
```
:bulb: Creates a reversed collection without modifying original.

#### 7. Empty arrays
```swift
var vehicles = [String]()       //  valid
var vehicles = Array<String>()  //  valid
var vehicles: [String] = []     //  valid
```
<br/>



## 🟢 Sets

```swift
var colors: Set<String> = ["red", "green", "blue"]
```
### ✨ Set Tricks

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

#### 5. Convert array to set
```swift
let array = ["a", "b", "a"]
let setFromArray = Set(array) // ➡️  {"a", "b"}
```

#### 6. Empty set
```swift
var emptySet = Set<String>()  //  valid
```
<br/>



## 📒 Dictionaries

```swift
let employee = [
    "name": "Taylor Swift",
    "job": "Singer",
    "location": "Nashville"
]
```
### ✨ Dictionary Tricks

#### 1. Access values
```swift
employee["name"]                   // ➡️  Optional("Taylor Swift")
print(employee["name"])           // ➡️  Optional("Taylor Swift")
print(employee["age"])            // ❌  nil (no key "age")
print(employee["name", default: "Unknown"]) // ➡️  "Taylor Swift"
```

#### 2. Create empty dictionary
```swift
var employee2 = [String: String]()       //  valid

employee2["name"] = "Grant"
employee2["favorite color"] = "Green"
```

#### 3. Read values
```swift
employee2["favorite color"]       // ➡️  "Green"
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


