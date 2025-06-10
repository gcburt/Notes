# 🧠 Constants, Variables, Strings & Integers in Swift
<br/><br/>

## 🔐 Constants  
Constants are **immutable** — once set, their value **cannot be changed**.

```swift
let myName = "Grant"
```

```swift
let age = 25
age = 30 // ❌ Error: Cannot change a constant
```
<br/>

## 🔁 Variables  
Variables are **mutable** — their value **can change** over time.

```swift
var myJob = "Pilot"
myJob = "Captain"
```
<br/><br/>

## 🧵 Strings  
Strings are used to store **text values** like words or sentences.



### ✨ String Tricks

#### 1. Quotes inside a string
```swift
let review = "My favorite movie is \"The Martian\"."
```

#### 2. Multiline strings
```swift
let haiku = """
I like poems
but I'm not very
good at them.
"""
```

#### 3. String interpolation
```swift
let greeting = "Hi, my name is \(myName)."
```

#### 4. Count characters (includes spaces)
```swift
let myName = "Grant"
myName.count // ➡️ returns 5
```

#### 5. Read prefix and suffix
```swift
let dinosaur = "velociraptor"
dinosaur.hasPrefix("Veloci") // ❌ false (V ≠ v)
dinosaur.hasSuffix("raptor") // ✅ true
```
<br/><br/>

## 🔢 Integers

An **integer** (or `Int`) is a whole number — no decimals.

Examples:  
`-5`, `0`, `42`, `100000`



### 🧮 Integer Tricks

#### 1. Common operations
```swift
let a = 10
let b = 3

let sum = a + b         // 13
let difference = a - b  // 7
let product = a * b     // 30
let quotient = a / b    // 3
let remainder = a % b   // 1
```

#### 2. Check for multiples
```swift
let number = 9
number.isMultiple(of: 3) // ✅ true
```

#### 3. Generate a random number
```swift
let randomNumber = Int.random(in: 1...100)
```
