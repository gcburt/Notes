# 🔗 Closures & Passing Functions in Swift  
<br/>

## 🧠 What Is a Closure?

A **closure** is a self‑contained block of functionality you can pass around and use in your code.  
Closures in Swift are similar to **anonymous functions** or **lambdas** in other languages.

```swift
// Closure assigned to a variable
let greet = { (name: String) -> String in
    return "Hello, \(name)!"
}

print(greet("Taylor")) // ➡️ :arrow_right: "Hello, Taylor!"
```

<br/>

## ✂️ Closure Syntax

```swift
{ (parameters) -> ReturnType in
    // code
}
```

| Part            | Description                               |
|-----------------|-------------------------------------------|
| `(parameters)`  | Input values, like a function signature   |
| `-> ReturnType` | What the closure returns                  |
| `in`            | Separator between signature and body      |

<br/>

## 🔄 Trailing Closure

When the last parameter of a function is a closure, you can write it **outside** the parentheses:

```swift
let numbers = [1, 2, 3, 4]

let doubled = numbers.map { number in
    number * 2
}
print(doubled) // ➡️ :arrow_right: [2, 4, 6, 8]
```

<br/>

## 💨 Shorthand Argument Names

Swift lets you omit parameter lists and use `$0`, `$1`, etc.:

```swift
let sorted = numbers.sorted { $0 > $1 }
print(sorted) // ➡️ :arrow_right: [4, 3, 2, 1]
```

<br/>

## 🔗 Passing Functions Into Functions

Functions and closures are **first‑class**: you can pass them as arguments.

```swift
func performOperation(_ a: Int, _ b: Int, using operation: (Int, Int) -> Int) -> Int {
    return operation(a, b)
}

func add(_ x: Int, _ y: Int) -> Int {
    x + y
}

let result = performOperation(4, 5, using: add)
print(result) // ➡️ :arrow_right: 9
```

You can also pass a closure directly:

```swift
let product = performOperation(4, 5) { $0 * $1 }
print(product) // ➡️ :arrow_right: 20
```

<br/>

## 🛠️ Common Higher‑Order Functions

| Function | Description                               | Example                            |
|----------|-------------------------------------------|------------------------------------|
| `map`    | Transforms each element                  | `numbers.map { $0 * 3 }`           |
| `filter` | Keeps elements that satisfy a condition  | `numbers.filter { $0 % 2 == 0 }`   |
| `reduce` | Combines elements into one value         | `numbers.reduce(0, +)`             |
| `sorted` | Sorts with a closure comparator          | `names.sorted { $0 < $1 }`         |

<br/>

---

**Practice:**  
1. Write a closure that takes a `String` and returns its length.  
2. Use `filter` with a trailing closure to keep only even numbers in an array.  
3. Call `performOperation` to subtract two values using a closure.  
