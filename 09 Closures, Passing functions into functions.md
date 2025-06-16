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

### 🧾 Function Types

```swift
func greetFunction() {
    print("Hello, User!")
}

var greetTypeAnnotation: () -> Void = greetFunction
```

🧠 `greetFunction` takes no variables and returns no new values.  
Technically, `print()` isn't returning a string.

```swift
func getUserData(for id: Int) -> String {
    if id == 1989 {
        return "Taylor Swift"
    } else {
        return "anonymous"
    }
}

let data: (Int) -> String = getUserData // ➡️  no () — not calling, only assigning
```

🧠 When it comes to closures, the names of the parameters don’t matter.  
Only the **types** do. `for id` is ignored in the closure’s type annotation.

### 🔢 Sorting Function

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

let sortedNames = names.sorted(by: meFirstSorted(name1:name2:)) // or
let sortedNames = names.sorted(by: meFirstSorted)              
```

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

### 🧵 Breakdown

1. `names.sorted`  
   The **sorted()** function is being called on the **names** array.

2. `(by: ___)`  
   The **sorted()** function has a parameter.

3. `{ (name1: String, name2: String) -> Bool in ... }`  
   The parameter is a custom closure.

4. `})`  
   Pay attention to where the parameter and closure begin.

5. Everything after `in`  
   is just code from before.

<br/>

## ✂️ Shortening Closures

```swift
let meFirstSortedClosureNoParameterTypes = names.sorted(by: { name1, name2 in
    if name1 == "Grant" {
        return true
    } else if name2 == "Grant" {
        return false
    }

    return name1 < name2
})
```

💡 `sorted()` is an Apple-defined function. It takes two `String` and returns a `Bool`. Stating it is redundant. String, String and Bool can be removed

```swift
(name1: String, name2: String) -> Bool in  // ➡️ Before
name1, name2 in                            // ➡️ After
```


## ⬇️ Trailing Closure Syntax

```swift
let meFirstTrailingClosureSyntax = names.sorted { name1, name2 in
    if name1 == "Grant" {
        return true
    } else if name2 == "Grant" {
        return false
    }

    return name1 < name2
}
```

✅ When one function **accepts another function** as its last parameter, you can get rid of the `(by: )`.


## ⚡ Shorthand Syntax

```swift
let meFirstShorthandSyntax = names.sorted {
    if $0 == "Grant" {
        return true
    } else if $1 == "Grant" {
        return false
    }

    return $0 < $1
}
```

🧠 Why not go crazy with it? $0 and $1 replace string 1 and 2 respectively.


## 🛠️ Common Functions That Accept Closures

- `.sorted` — for ordering values  
- `.filter` — for keeping only items that match a condition  
- `.map` — for transforming each item in a collection  


## Accepting functions as parameters

```swift
func makeArray(size: Int, using generator: () -> Int) -> [Int] {
    var numbers = [Int]()

    for _ in 0..<size {
        let newNumber = generator()
        numbers.append(newNumber)
    }

    return numbers
}

let rolls = makeArray(size: 5) {
    Int.random(in: 1...20)
}
```
