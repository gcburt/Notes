# 🚨 Error Handling in Swift
<br/>

## 🧠 What Are Errors?

Swift uses **error handling** to respond to **unexpected conditions**.  
Errors are values that conform to the `Error` protocol.

```swift
enum PasswordError: Error {
    case short, obvious
}
```

<br/>

## ⚙️ Writing a Throwing Function

Add `throws` to the function signature and use `throw` inside:

```swift
func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    }

    if password == "12345" {
        throw PasswordError.obvious
    }

    if password.count < 8 {
        return "OK"
    } else if password.count < 10 {
        return "Good"
    } else {
        return "Excellent"
    }
}
```

- `throws` marks that the function **can throw** an error.  
- Use `throw` to send an error value.

<br/>

## 🔍 Calling a Throwing Function

### 1️⃣ `do-catch` block

```swift
let string = "12345"

do {
    let result = try checkPassword(string)
    print("Password rating: \(result)")
} catch PasswordError.short {
    print("Please use a longer password.")
} catch PasswordError.obvious {
    print("I have the same combination on my luggage!")
} catch {
    print("There was an error.")
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
    print(user.id)      // ➡️  42
} catch {
    print("Invalid ID.") // ❌  if conversion fails
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

