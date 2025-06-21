# 🔒 Access Control, Static Properties & Methods  
<br/>

Unedited


## 🚧 Access Control Levels

Swift lets you restrict visibility of types and members:

| Level      | Description                                                |
|------------|------------------------------------------------------------|
| `private`  | Only within the **same** declaration (e.g., a struct/class) |
| `fileprivate` | Anywhere in the **same file**                             |
| `internal` | Anywhere in the **same module** (default)                  |
| `public`   | Any module **can see**, but **cannot subclass/override**   |
| `open`     | Any module **can see** and **subclass/override**           |

```swift
public struct BankAccount {
    private var balance: Double = 0.0

    fileprivate func log(_ message: String) {
        print("Log: \(message)") // ➡️ :arrow_right: internal use only
    }

    func deposit(_ amount: Double) {
        balance += amount       // ✅ :green_check_mark: allowed
        log("Deposited \(amount)")
    }
}
```

- No keyword = `internal` by default.  
- `open` is more permissive than `public` (only for classes/protocols).

<br/>

---

## 🏷️ `static` Properties & Methods

Use `static` to define properties or methods **on the type**, not on instances.

```swift
struct Math {
    static let pi = 3.14159      // type property

    static func square(_ x: Double) -> Double {
        return x * x             // ➡️ :arrow_right: 4 * 4 = 16
    }
}

let area = Math.pi * 5 * 5      // ➡️ :arrow_right: 78.53975
let sq   = Math.square(4)       // ➡️ :arrow_right: 16
```

- You **cannot** access `Math.pi` on an instance.  
- For classes, you can use `class func` instead of `static` to allow overrides.

```swift
class Vehicle {
    static var count = 0        // shared across all Vehicles

    init() {
        Vehicle.count += 1
    }

    class func makeNoise() {
        print("Vroom!")         // can be overridden by subclasses
    }
}

Vehicle.makeNoise()            // ➡️ :arrow_right: "Vroom!"
print(Vehicle.count)           // ➡️ :arrow_right: number of instances
```

<br/>

---

✅ **Practice:**  
1. Create a `Logger` struct with a `static var level: Int` and a `static func log(_:)` that only prints when a message’s level ≤ `Logger.level`.  
2. Experiment with making a helper method `private` vs. `fileprivate` and see where you can or cannot call it.  
