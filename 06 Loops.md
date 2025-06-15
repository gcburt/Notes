# 🔁 For Loops in Swift  
<br/>

## 🧩 What is a For Loop?

A `for` loop repeats a block of code **for each element** in a sequence (arrays, ranges, dictionaries, etc.).

```swift
let names = ["Alice", "Bob", "Charlie"]

for name in names {
    print(name)
}
```
➡️ ➡️  
```
Alice
Bob
Charlie
```

<br/>

## 🔢 Looping Over a Range

```swift
for i in 1...5 {
    print(i)
}
```
➡️ ➡️  
```
1
2
3
4
5
```

- Use `1..<5` to go from 1 **up to** 4 (exclusive upper bound).

<br/>

## 📚 Looping with Indices

```swift
let fruits = ["🍎", "🍌", "🍇"]

for index in fruits.indices {
    print("\(index): \(fruits[index])")
}
```
➡️ ➡️  
```
0: 🍎
1: 🍌
2: 🍇
```

- `fruits.indices` yields valid index values (0…count‑1).

<br/>

## 🔍 Enumerated Loop

Get both **index** and **value** in one go:

```swift
for (index, fruit) in fruits.enumerated() {
    print("\(index + 1). \(fruit)")
}
```
➡️ ➡️  
```
1. 🍎
2. 🍌
3. 🍇
```

<br/>

## 🏃‍♂️ Stride

Skip by steps:

```swift
// from 0 to 10, stepping by 2
for i in stride(from: 0, through: 10, by: 2) {
    print(i)
}
```
➡️ ➡️  
```
0
2
4
6
8
10
```

- Use `to:` instead of `through:` to **exclude** the end value.

<br/>

## 🗺️ Looping Dictionaries

Iterate key/value pairs:

```swift
let ages = ["Alice": 30, "Bob": 25]

for (name, age) in ages {
    print("\(name) is \(age) years old.")
}
```
➡️ ➡️  
```
Alice is 30 years old.
Bob is 25 years old.
```

- Order is **undefined** for dictionaries.

<br/>

## 💡 Tips & Tricks

- You **cannot** mutate the sequence you’re looping over (e.g., remove items from the array) during a `for` loop.  
- Use `break` to **exit** early.  
- Use `continue` to **skip** to the next iteration.  

```swift
for i in 1...10 {
    if i % 2 == 0 {
        continue    // skip even numbers
    }
    print(i)
}
```
➡️ ➡️  
```
1
3
5
7
9
```

<br/>

---

<br/>

# 🔄 While Loops in Swift  
<br/>

## 🧠 What is a While Loop?

A `while` loop repeats a block of code **as long as** a condition remains true.

```swift
var count = 1

while count <= 5 {
    print(count)
    count += 1
}
```
➡️ ➡️  
```
1
2
3
4
5
```

<br/>

## 🔁 Structure

```swift
while condition {
    // code runs while condition is true
}
```

- **Check** the condition **before** each iteration.  
- If the condition is initially false, the body **never** runs.

<br/>

## 🔄 `repeat-while` Loop

A `repeat-while` loop runs the code **at least once**, then checks the condition:

```swift
var num = 1

repeat {
    print(num)
    num += 1
} while num <= 3
```
➡️ ➡️  
```
1
2
3
```

- Checks the condition **after** each iteration.

<br/>

## 🚧 Common Pitfalls

- **Infinite loop** if condition never becomes false:  
  ```swift
  var x = 0
  while x < 3 {
      print(x)
      // x never changes → infinite loop!
  }
  ```
- Always ensure you **modify** a variable in the loop to eventually break out.

<br/>

## 🛠️ Break & Continue

- `continue` *skips* the current step.
- `break` *exits* the loop entirely.

```swift
var i = 0
while i < 5 {
    i += 1
    if i == 3 {
        continue  // skips printing 3
    }
    if i == 5 {
        break     // exits loop when i == 5
    }
    print(i)
}
```
➡️ ➡️  
```
1
2
4
```

<br/>

## ✅ Good to Know

- Use `while` when you **don’t know** in advance how many iterations you need.  
- Use `for-in` when you have a **fixed** sequence or range.  
- `repeat-while` is useful when you need **at least one** execution.

<br/>

---
