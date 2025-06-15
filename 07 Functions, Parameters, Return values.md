# 🛠️ Functions in Swift  
<br/>

## 📝 Defining a Function

```swift
func greet() {
    print("Hello, World!")
}
```
- `func` keyword starts a function.  
- `greet()` is the function name and empty parameter list.  
- Body enclosed in `{}`.

## ▶️ Calling a Function

```swift
greet()   // ➡️ ➡️ prints "Hello, World!"
```

<br/>

## ➡️ Parameters & Return Values

```swift
func square(_ number: Int) -> Int {
    return number * number
}
```
- `_ number: Int` means **unnamed** external parameter, internal name `number`.  
- `-> Int` indicates it **returns** an `Int`.  
- Must use `return` to send value back.

```swift
let result = square(5)  // ➡️ ➡️ result = 25
```

<br/>

## 🎨 External vs Internal Parameter Names

```swift
func greet(person name: String) {
    print("Hello, \(name)!")
}

greet(person: "Taylor") // ➡️ ➡️ prints "Hello, Taylor!"
```
- `person` is the **external** name used at call site.  
- `name` is the **internal** name used inside the function.

<br/>

## ⚙️ Default Parameter Values

```swift
func greet(_ name: String, withGreeting greeting: String = "Hi") {
    print("\(greeting), \(name)!")
}

greet("Alice")                    // ➡️ ➡️ "Hi, Alice!"
greet("Bob", withGreeting: "Hey") // ➡️ ➡️ "Hey, Bob!"
```
- Provide defaults so the caller can omit arguments.

<br/>

## 🔣 Variadic Parameters

```swift
func sum(_ numbers: Int...) -> Int {
    return numbers.reduce(0, +)
}

sum(1, 2, 3, 4) // ➡️ ➡️ 10
```
- `Int...` allows zero or more `Int` arguments in an array.

<br/>

## 🔄 In-Out Parameters

```swift
func increment(_ value: inout Int) {
    value += 1
}

var x = 10
increment(&x)
print(x) // ➡️ ➡️ 11
```
- `inout` lets function modify external variable.  
- Pass with `&`.

<br/>

## 💡 Returning Multiple Values

Use a tuple:

```swift
func getUser() -> (firstName: String, lastName: String) {
    (firstName: "Taylor", lastName: "Swift")
}

let user = getUser()
let firstName = user.firstName ➡️ Taylor
let lastName = user.lastName   ➡️ Swift

print("Name: \(firstName) \(lastName)") ➡️ prints "Taylor Swift"
```

<br/>

## ✅ Good to Know

- Functions are **first-class**: can assign to variables or pass as arguments.  
- You can nest functions inside other functions.  
- Use `guard` for early exits in functions with return values.

<br/>

---


