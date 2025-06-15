# 📜 Protocols & Extensions in Swift  
<br/>

## 🧩 Protocols

A **protocol** defines a blueprint of methods, properties, or requirements that suit a particular task or piece of functionality.

```swift
protocol Drivable {
    var speed: Double { get set }
    func drive()
}
```

- `var speed: Double { get set }` means **read/write** property.  
- `func drive()` must be implemented by conforming types.

### 📦 Conforming to a Protocol

```swift
struct Car: Drivable {
    var speed: Double = 0.0

    func drive() {
        print("Driving at \(speed) mph") // ➡️ :arrow_right: Driving at 0.0 mph
    }
}
```

- Use `: Drivable` after the type name.  
- Must implement all requirements exactly.

<br/>

## 🔄 Protocol with Default Implementation

You can provide a default in a **protocol extension**:

```swift
extension Drivable {
    func drive() {
        print("Default driving at \(speed) mph")
    }
}
```

- Types conforming to `Drivable` get `drive()` for free.  
- They can still **override** it.

<br/>

## 🧩 Extensions

An **extension** adds new functionality to an existing type—your own or from the standard library.

```swift
extension String {
    var reversedString: String {
        String(self.reversed())
    }

    func shout() {
        print(self.uppercased() + "!") // ➡️ :arrow_right: "hello!" → "HELLO!"
    }
}
```

- Adds a **computed property** `reversedString`.  
- Adds a **method** `shout()`.

<br/>

## ➕ Extending to Conform

You can use an extension to make a type conform to a protocol:

```swift
protocol Greetable {
    func greet()
}

extension Person: Greetable {
    func greet() {
        print("Hi, I'm \(name)") // ➡️ :arrow_right: "Hi, I'm Alex"
    }
}
```

- Keeps your original type definition separate.  
- Organizes code by functionality.

<br/>

## 💡 Common Uses

| Feature                  | Example                                                        |
|--------------------------|----------------------------------------------------------------|
| Add computed properties  | `extension Int { var isEven: Bool { self % 2 == 0 } }`         |
| Add methods              | `extension Array { func second() -> Element? { ... } }`       |
| Conform to protocols     | `extension URL: SomeProtocol { ... }`                          |
| Group code logically     | Use multiple extensions for different responsibilities         |

<br/>

---

**✅ Practice:**  
1. Define protocol `Payable` with `func calculateWage(hours: Double) -> Double`.  
2. Create `struct Employee` conforming to `Payable`.  
3. Write an extension on `Double` to add `var squared: Double`.  
```swift
let x = 3.0
print(x.squared) // ➡️ :arrow_right: 9.0
```  
