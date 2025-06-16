# 🔗 Closures & Passing Functions in Swift  
<br/>

## 🧠 What Is a Closure?

> "Closures are self-contained blocks of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and to lambdas in other programming languages."

🔍 In simple terms: **Closures are unnamed functions.**

```swift
let greetClosure = {
    print("Hello, User!")
}
```

You can also assign regular functions to variables using type annotations:

```swift
func greetFunction() {
    print("Hello, User!")
}

var greetTypeAnnotation: () -> Void = greetFunction
```

- `greetFunction` takes no parameters and returns nothing.  
- `print()` outputs to console but doesn’t return a value.  
- `() -> Void` describes a function that returns no value.

<br/>

## 📬 Assigning a Function to a Variable

```swift
func getUserData(for id: Int) -> String {
    if id == 1989 {
        return "Taylor Swift"
    } else {
        return "anonymous"
    }
}

let data: (Int) -> String = getUserData
```

📝 Note:  
- There's **no `()`** after `getUserData` — we are assigning the **function**, not calling it.  
- The name `for id` is ignored in the closure type. Only the data types matter.

<br/>

## 🔃 Using Closures for Custom Sorting

```swift
let names = ["Grant", "Hunter", "Amanda", "Scott", "Julie"]

func meFirstSorted(name1: String, name2: String) -> Bool {
    if name1 == "Grant" {
        return true
    } else if name2 == "Grant" {
        return false
    }
    return name1 < name2
}

let sortedNames = names.sorted(by: meFirstSorted(name1:name2:)) // valid
let sortedNames2 = names.sorted(by: meFirstSorted)              // also valid
```

You can also rewrite that same logic as an **inline closure**:

```swift
let meFirstSortedClosure = names.sorted(by: { (name1: String, name2: String) -> Bool in
    if name1 == "Grant" {
        return true
    } else if name2 == "Grant" {
        return false
    }
    return name1 < name2
})
```

<br/>

### 📦 Breakdown

1. `names.sorted` — We are calling the `sorted()` method on the `names` array.  
2. `(by: ___)` — The method takes a **closure** as a parameter.  
3. `{ (name1: String, name2: String) -> Bool in ... }` — This is the full closure being passed in.  
4. `in` — Separates the parameters from the closure body.  
5. The body logic is identical to what was defined in the named function earlier.

---

✅ **Practice:**  
- Rewrite the sorting closure using shorthand: `$0` and `$1`.  
- Try assigning a closure that takes two numbers and returns their product.



<br/>
<br/>
<br/>
<br/>
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
