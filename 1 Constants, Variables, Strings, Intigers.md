# Constant/Variables/Strings/Intigers

## Constants
are *immutable*. They are fixed.

```swift
let myName = "Grant"
```

```swift 
let age = 25
age = 30 // ❌ Error: Cannot change a constant
```

## Variables 
are *mutable*, or able to be changed.

```swift
var myJob = "Pilot"
```

## Strings


### Some tricks   

1. Quotes inside a string
   
```swift
let review = "My favorite movie is \"The Martian\".
```

2. Multiple line string
   
```swift
let haiku = """
I like poems
but I'm not very
good at them.
"""
```

3. String interpolation

```swift
let greeting = "Hi, my name is \(myName)."
```

4. Count characters. (Includes spaces)
```swift
let myName = "Grant"
myName.count // ➡️ returns 5
```

5. Read prefix/suffix
```swift
let dinosaur = "velociraptor"
dinosaur.hasPrefix("Veloci") // ❌ false (V != v)
dinosaur.hasSuffix("raptor") // ✅ true 
```

## 🔢 Intigers



An integer (or Int) is a whole number — meaning it has no decimals.

Examples:
-5, 0, 42, 100000

### Some tricks

1. Common operations
```swift
let a = 10
let b = 3

let sum = a + b       // 13
let difference = a - b // 7
let product = a * b    // 30
let quotient = a / b   // 3
let remainder = a % b  // 1
```

2. Multiples
```swift
let number = 9
number.isMultiple(of:3) ✅ true
```

3. Random number
```swift
let randomNumber = Int.random(in: 1...100)
```
