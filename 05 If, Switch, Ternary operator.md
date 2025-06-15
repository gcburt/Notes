# 🔀 If Statements 
<br/>

## 🔎 What is an If Statement?

An `if` statement lets your code make decisions.  
It checks whether a condition is true or false, and runs code **only if** the condition is true.

```swift
let age = 18

if age >= 18 {
    print("You can vote!")
}
```
➡️ :arrow_right: `"You can vote!"` is printed **only if** `age` is 18 or more.

<br/>

## 🪜 Optional `else`

Use `else` to handle the opposite case — when the condition is false.

```swift
let temperature = 45

if temperature > 60 {
    print("It's warm!")
} else {
    print("Bring a jacket.")
}
```

➡️ :arrow_right: Prints `"Bring a jacket."` if the temperature is not greater than 60.

<br/>

## 🔗 `else if` for multiple conditions

Use `else if` when you want to check **more than one** condition.

```swift
let score = 85

if score >= 90 {
    print("A")
} else if score >= 80 {
    print("B")
} else {
    print("Keep trying!")
}
```

➡️ :arrow_right: This allows one path to match based on priority (top-down).

<br/>

## 💡 Comparison Operators

| Symbol | Meaning             |
|--------|----------------------|
| `==`   | equal to             | 
| `!=`   | not equal to         | 
| `>`    | greater than         | 
| `<`    | less than            | 
| `>=`   | greater or equal     | 
| `<=`   | less or equal        | 

<br/>

## 🔗 Logical Operators

Use these to combine multiple conditions:

| Operator | Name       | Example                           |
|----------|------------|-----------------------------------|
| `&&`     | and        | `age >= 18 && citizen == true`    |
| `\/`     | or         | `isStudent \/ isSenior`           |
| `!`      | not        | `!hasAccess` means "no access"    |

---

<br/>

# 🔄 Switch Statements 
<br/>

## 🧠 What is a Switch Statement?

A `switch` lets you check **many possible values** of a variable and run different code for each one.

```swift
let weather = "sunny"

switch weather {
case "rainy":
    print("Bring an umbrella.")
case "sunny":
    print("Wear sunscreen.")
default:
    print("Check the forecast.")
}
```

➡️ Prints `"Wear sunscreen."`

<br/>

## 🧾 Why Use `switch`?

- Cleaner than a long chain of `if else if`
- Safer and more readable
- **Must be exhaustive** (must cover all cases or use `default`)

<br/>

## 🔢 Matching Ints

```swift
let score = 100

switch score {
case 0:
    print("Zero")
case 1..<100:
    print("Almost there")
case 100:
    print("Perfect score!")
default:
    print("Unknown score")
}
```

➡️ You can match exact numbers or ranges.

<br/>

## 🎨 Matching Multiple Cases

```swift
let pet = "dog" // or cat, or rabbit...

switch pet {
case "cat", "dog", "rabbit":
    print("It's a common pet.")
default:
    print("Exotic choice!")
}
```

➡️ Use commas to match multiple values in one case.

<br/>

## 🧱 Fallthrough (Rarely Used)

Use `fallthrough` to continue to the next case — even if the current one matched.

```swift
let number = 3

switch number {
case 3:
    print("Three")
    fallthrough
case 4:
    print("Four")
default:
    break
}
```

➡️ Prints both "Three" and "Four"

⚠️ `fallthrough` does **not** check the next case’s condition.

<br/>

## 💡 With Enums

`switch` works great with enums — and helps catch missing cases.

```swift
enum Direction {
    case north, south, east, west
}

let heading = Direction.east

switch heading {
case .north:
    print("Going up")
case .south:
    print("Going down")
case .east:
    print("Going right")
case .west:
    print("Going left")
}
```

✅ No need for `default` if you cover all enum cases.

<br/>

---

<br/>

# ⚖️ Ternary Conditional Operator in Swift
<br/>

## 🤔 **WTF** is the Ternary Operator?

The ternary operator is a **compact shortcut for `if/else`**. I'm probably not going to use it much.

```swift
let age = 20
let canVote = age >= 18 ? "Yes" : "No"
```

➡️ Returns `"Yes"` because the condition is true.

<br/>

```swift
let isSunny = true
let message = isSunny ? "Wear sunglasses" : "Bring an umbrella"
```

➡️ Returns `"Wear sunglasses"`

<br/>

```swift
let score = 85
let result = score >= 60 ? "Pass" : "Fail"
```

➡️ Returns `"Pass"`


