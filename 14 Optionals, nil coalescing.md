```swift
var myVar: Int? = 1

if let unwrapped = myVar {
    print("Run if myVar has a value inside")
}

guard let unwrapped = myVar else {
    print("Run if myVar doesn't have a value inside")
}
```


# 💭 Optionals & Nil Coalescing in Swift  
<br/>

## 🧠 What Is an Optional?

An **optional** represents a value that **may be present** or **may be nil** (no value).

```swift
var name: String? = "Alice"   // Optional String containing "Alice"
var age: Int? = nil           // Optional Int containing nil
```

- `?` makes the type optional.  
- Internally, Swift wraps the value in `.some(value)` or `.none`.

<br/>

## 🔓 Unwrapping Optionals

### 1. Forced Unwrap

```swift
let forcedName = name!       // ➡️ :arrow_right: "Alice" (crashes if nil)
```
⚠️ Use **only** when you’re **sure** it isn’t nil.

### 2. Optional Binding

```swift
if let unwrappedName = name {
    print(unwrappedName)      // ➡️ :arrow_right: "Alice"
} else {
    print("No name provided") // ➡️ :arrow_right: fallback
}
```

### 3. Guard Statement

```swift
func greet(_ name: String?) {
    guard let name = name else {
        print("No name!")      // ➡️ :arrow_right: if nil
        return
    }
    print("Hello, \(name)!")  // ➡️ :arrow_right: if non‑nil
}
```

<br/>

## 💡 Nil Coalescing Operator `??`

Provide a **default value** if optional is nil.

```swift
let displayName = name ?? "Guest"
print(displayName)           // ➡️ :arrow_right: "Alice" or "Guest"
```

- `a ?? b` returns `a!` if non‑nil, otherwise `b`.

<br/>

## 🔍 Optional Chaining

Safely call properties or methods on an optional:

```swift
struct User { var petName: String? }
let user: User? = User(petName: "Buddy")

let pet = user?.petName       // Optional("Buddy")
let length = user?.petName?.count  // Optional(5)
```

- Returns nil if any link in chain is nil.

<br/>

## 🚫 Common Pitfalls

```swift
let s: String! = nil
print(s.count)                // ❌ :X: runtime crash
```

- Implicitly unwrapped optionals (`!` in type) can crash if nil.  
- Prefer safe unwrapping (`if let` / `guard let`).

<br/>

## ✅ Good to Know

| Feature                   | Description                                 |
|---------------------------|---------------------------------------------|
| `?`                       | Declare optional type                       |
| `!`                       | Forced unwrap (risky)                       |
| `if let` / `guard let`    | Safe unwrapping                             |
| `??`                      | Provide default for nil                     |
| `someOptional?.property`  | Optional chaining                           |

<br/>

---

**Practice:**  
1. Write a function `describe(_ number: Int?) -> String` that returns `"Number is X"` or `"No number"` using nil coalescing.  
2. Use optional chaining to get the first character of a `String?` safely.
