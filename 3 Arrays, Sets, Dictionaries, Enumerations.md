# Arrays, Sets, Dictionaries and Enumerations
<br/>

## Arrays



```swift
var pets = ["Murphy", "Hiro", "Milkshakes", "Sasha"]
```
#### 1. Add an item
```swift
pets.append("Amanda Trash Panda")
pets[0]
```
The position of an item in an array is commonly called its *index*.
- .append adds "Amanda" to the end.
- [0] calls "Murphy" because he is at the 0 index.

#### 2. Remove item(s)

```swift
pets.remove(at:0) // ➡️ removes Murphy
prets.removeAll()
```

#### 3. Count

```swift
pets.count // ➡️ 5 or number of items in array
```

#### 3. Contains

```swift
pets.contains("Fido") // ❌ false
``` 

#### 4. Sorted

```swift
let letters = ["c", "a", "e", "b", "d"]
letters.sorted() // ➡️ ["a", "b", "c", "d", "e"]
```

#### 5. Reversed

```swift
letters.reversed() // ➡️ ReversedCollection<Array<String>>(_base: ["c", "a", "e", "b", "d"])
```

- Makes the colllection on the fly. 
#### 6. Empty arrays

```swift
var vehicles = [String]()
var vehicles = Array<String>()
var vehicles: [String] = []
```
- Makes an empty Array.
- Dont forget the () on the type inferance examples.
<br/>
  
## Sets


## Dictionaries
## Enumerations

```swift
enum Weekdays {   // ⚠️ Notice the UpperCamelCase
case monday, tuesday, wednesday, thursday, friday
}

var day = Weekdays.monday
day = .tuesday
```

