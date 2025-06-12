# 🔀 If Statements in Swift
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

| Symbol | Meaning             | Example (`a = 5`, `b = 10`)        |
|--------|----------------------|------------------------------------|
| `==`   | equal to             | `a == 5` → ✅ :green_check_mark: true |
| `!=`   | not equal to         | `a != b` → ✅ :green_check_mark: true |
| `>`    | greater than         | `b > a` → ✅ :green_check_mark: true |
| `<`    | less than            | `a < b` → ✅ :green_check_mark: true |
| `>=`   | greater or equal     | `a >= 5` → ✅ :green_check_mark: true |
| `<=`   | less or equal        | `a <= 5` → ✅ :green_check_mark: true |

<br/>

## 🔗 Logical Operators

Use these to combine multiple conditions:

| Operator | Name       | Example                           |
|----------|------------|-----------------------------------|
| `&&`     | and        | `age >= 18 && citizen == true`    |
| `||`     | or         | `isStudent || isSenior`           |
| `!`      | not        | `!hasAccess` means "no access"    |

<br/>

## ✅ Good to Know

- Use `if` when you **want to check a condition** and run code **only sometimes**.
- Swift expects conditions to be `Bool` — you can’t write `if 1` or `if "hello"`.

```swift
let isLoggedIn = false

if !isLoggedIn {
    print("Please log in.")  // This runs
}
```

<br/>

---
