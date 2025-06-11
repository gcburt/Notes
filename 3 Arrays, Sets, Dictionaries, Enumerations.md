# 🧱 Arrays, Sets, Dictionaries & Enumerations
<br/>

## 📚 Arrays

```swift
var pets = ["Murphy", "Hiro", "Milkshakes", "Sasha"]
```

### 1. Add an item
```swift
pets.append("Amanda Trash Panda") // ➡️ :arrow_right: adds to end
pets[0]                           // ➡️ :arrow_right: returns "Murphy"
```

### 2. Remove item(s)
```swift
pets.remove(at: 0)    // ➡️ :arrow_right: removes "Murphy"
pets.removeAll()      // ➡️ :arrow_right: clears all items
```

### 3. Count items
```swift
pets.count            // ➡️ :arrow_right: returns number of items
```

### 4. Check if it contains something
```swift
pets.contains("Fido") // ❌ :X: false
```

### 5. Sort array
```swift
let letters = ["c", "a", "e", "b", "d"]
letters.sorted()      // ➡️ :arrow_right: ["a", "b", "c", "d", "e"]
```

### 6. Reverse array
```swift
letters.reversed()    // ➡️ :arrow_right: ReversedCollection(["c", "a", "e", "b", "d"])
```
:bulb: Creates a reversed collection without modifying original.

### 7. Empty arrays
```swift
var vehicles = [String]()       // :green_check_mark: valid
var vehicles = Array<String>()  // :green_check_mark: valid
var vehicles: [String] = []     // :green_check_mark: valid
```
<br/>

---

## 🟢 Sets

```swift
var colors: Set<String> = ["red", "green", "blue"]
```

### 1. Insert
```swift
colors.insert("yellow")       // ➡️ :arrow_right: adds if not present
```

### 2. Check for presence
```swift
colors.contains("green")      // ✅ :green_check_mark: true
colors.contains("purple")     // ❌ :X: false
```

### 3. Count
```swift
colors.count                  // ➡️ :arrow_right: number of unique items
```

### 4. Remove item
```swift
colors.remove("red")          // ➡️ :arrow_right: removes "red" if it exists
```

### 5. Convert array to set
```swift
let array = ["a", "b", "a"]
let setFromArray = Set(array) // ➡️ :arrow_right: {"a", "b"}
```

### 6. Empty set
```swift
var emptySet = Set<String>()  // :green_check_mark: valid
```
<br/>

---

## 📒 Dictionaries

```swift
let employee = [
    "name": "Taylor Swift",
    "job": "Singer",
    "location": "Nashville"
]
```

### 1. Access values
```swift
employee["name"]                   // ➡️ :arrow_right: Optional("Taylor Swift")
print(employee["name"])           // ➡️ :arrow_right: Optional("Taylor Swift")
print(employee["age"])            // ❌ :X: nil (no key "age")
print(employee["name", default: "Unknown"]) // ➡️ :arrow_right: "Taylor Swift"
```

### 2. Create empty dictionary
```swift
var employee2 = [String: String]()       // :green_check_mark: valid

employee2["name"] = "Grant"
employee2["favorite color"] = "Green"
```

### 3. Read values
```swift
employee2["favorite color"]       // ➡️ :arrow_right: "Green"
```
<br/>

---

## 🧩 Enumerations

```swift
enum Weekdays {
    case monday, tuesday, wednesday, thursday, friday
}

var day = Weekdays.monday
day = .tuesday
```

### Notes
- Enum types use **UpperCamelCase**
- Cases use **lowerCamelCase** by convention
- Shortens access: `.tuesday` is valid after `day` is declared as a `Weekdays`

<br/>

---
