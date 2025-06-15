# 🏗️ Structs, Computed Properties & Property Observers  
<br/>

## 🏗️ Structs

A `struct` defines a custom data type with stored properties.

```swift
struct Person {
    var name: String
    var age: Int
}

var user = Person(name: "Alex", age: 30)
print(user.name) // ➡️ :arrow_right: "Alex"
user.age = 31    // :green_check_mark: mutable because `age` is a `var`
```

- Use `let` to make an entire struct instance immutable.  
- Structs get a **memberwise initializer** by default.

<br/>

---

## ⚙️ Computed Properties

Computed properties calculate a value on the fly—you don’t store it directly.

```swift
struct Rectangle {
    var width: Double
    var height: Double

    var area: Double {
        return width * height
    }

    var perimeter: Double {
        2 * (width + height) // shorthand `return`
    }
}

let rect = Rectangle(width: 5, height: 10)
print(rect.area)      // ➡️ :arrow_right: 50.0
print(rect.perimeter) // ➡️ :arrow_right: 30.0
```

- Computed properties can be **read-only** (no `set`) or **read-write** (with `get` and `set`).  
- Example read-write:

```swift
struct Circle {
    var radius: Double
    var diameter: Double {
        get {
            return radius * 2
        }
        set {
            radius = newValue / 2
        }
    }
}
```

<br/>

---

## 👀 Property Observers

Use `willSet` and `didSet` to run code before or after a property changes.

```swift
struct StepCounter {
    var steps: Int = 0 {
        willSet {
            print("About to set steps to \(newValue)") // ➡️ :arrow_right: prints newValue
        }
        didSet {
            if steps > oldValue {
                print("Added \(steps - oldValue) steps") // ➡️ :arrow_right: prints difference
            }
        }
    }
}

var counter = StepCounter()
counter.steps = 100
// ➡️ :arrow_right: "About to set steps to 100"
// ➡️ :arrow_right: "Added 100 steps"

counter.steps = 150
// ➡️ :arrow_right: "About to set steps to 150"
// ➡️ :arrow_right: "Added 50 steps"
```

- `willSet` provides `newValue`.  
- `didSet` provides `oldValue`.  
- Observers are **not** called during initialization.

<br/>

---

✅ **Practice:**  
- Create a `struct` `BankAccount` with a `balance` property that logs deposits and withdrawals using `didSet`.  
- Add a computed property `isOverdrawn: Bool`.  
- Test depositing and withdrawing to see your observers in action.  
