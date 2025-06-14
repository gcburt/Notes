# 🚨 Error Handling in Swift
<br/>

## 🧠 What Are Errors?

Swift uses **error handling** to respond to **unexpected conditions**.  
Errors are values that conform to the `Error` protocol.

```swift
enum DataError: Error {
    case fileNotFound
    case unreadable
    case encodingFailed
}
```

<br/>

## ⚙️ Writing a Throwing Function

Add `throws` to the function signature and use `throw` inside:

```swift
func loadFile(named name: String) throws -> String {
    guard let path = Bundle.main.path(forResource: name, ofType: nil) else {
        throw DataError.fileNotFound
    }
    let contents = try String(contentsOfFile: path)
    return contents
}
```

- `throws` marks that the function **can throw** an error.  
- Use `throw` to send an error value.

<br/>

## 🔍 Calling a Throwing Function

### 1️⃣ `do-catch` block

```swift
do {
    let text = try loadFile(named: "notes.txt")
    print(text)
} catch DataError.fileNotFound {
    print("File not found.")   // ➡️ :arrow_right: prints this if missing
} catch {
    print("Unexpected error: \(error).")
}
```

- Wrap calls with `try`.  
- Handle specific errors first, then a general `catch`.

### 2️⃣ Optional `try?`

```swift
let text = try? loadFile(named: "notes.txt")
print(text)  // ➡️ :arrow_right: Optional("file contents") or nil
```

- Converts **thrown error** into `nil`.

### 3️⃣ Forced `try!`

```swift
let text = try! loadFile(named: "notes.txt")
print(text)
```

- Crashes at runtime if an error is thrown.  
- Use only when you’re sure it won’t fail.

<br/>

## 💡 Throwing Initializers

Initializers can throw too:

```swift
struct User {
    let id: Int
    init(idString: String) throws {
        guard let id = Int(idString) else {
            throw DataError.encodingFailed
        }
        self.id = id
    }
}

do {
    let user = try User(idString: "42")
    print(user.id)      // ➡️ :arrow_right: 42
} catch {
    print("Invalid ID.") // ❌ :X: if conversion fails
}
```

<br/>

## ⚠️ Rethrowing Functions

A function that **takes** a throwing closure can itself `rethrows`:

```swift
func perform(operation: () throws -> Void) rethrows {
    try operation()
}
```

- `rethrows` means it only throws if the passed-in closure throws.

<br/>

## ✅ Good to Know

- Use **specific error cases** to distinguish failures.  
- Always handle errors in production code.  
- Prefer `do-catch` for detailed handling, `try?` for quick attempts.  
- Avoid `try!` unless absolutely safe.

<br/>

---

**Practice:** Write a `divide(_:by:) throws -> Double` function that throws a `.divideByZero` error if the divisor is zero, otherwise returns the quotient.  

