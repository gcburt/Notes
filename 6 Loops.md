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
➡️ :arrow_right:  
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
➡️ :arrow_right:  
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
➡️ :arrow_right:  
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
➡️ :arrow_right:  
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
➡️ :arrow_right:  
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
➡️ :arrow_right:  
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
➡️ :arrow_right:  
```
1
3
5
7
9
```

<br/>
