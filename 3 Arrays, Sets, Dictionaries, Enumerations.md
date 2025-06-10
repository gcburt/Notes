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

