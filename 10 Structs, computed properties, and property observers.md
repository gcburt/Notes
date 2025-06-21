# Structs in Swift

Structs are user-made, custom data types. They can include variables, functions, and *mutating functions*.

## 1. Syntax & Terminology

```swift
struct Person {
    let name: String
    var age: Int
    var dickLength: Double
    
    func greeting() {
        print("sup nerds")
    }
    
    mutating func seeGirl() {
        dickLength += 1
    }
}

var me = Person(name: "Grant", age: 32, dickLength: 3.5) // ➡️ The syntax is almost identical to a function. This is called an **initializer**.
me.seeGirl() // ➡️ 4.5
```

> 

---

## Stored vs Computed Properties

### Stored Properties

```swift
struct EmployeeStored {
    let name: String
    var vacationRemaining = 14
    
    mutating func employeeVacation(days: Int) {
        if days <= vacationRemaining {
            vacationRemaining -= days
        } else {
            print("Sorry Bozo")
        }
    }
}

var grantB = EmployeeStored(name: "Grant")   // ⚠️ 14 is default vacationRemaining
grantB.employeeVacation(days: 3)             // ➡️ vacationRemaining = 11
```

> When the employeeVacation method is called, it subtracts 3 from 14. 11 is the new **stored value** for vacation remaining. However, now there is no way to tell how much vacation was originally assigned.

**Terminology:**
- Constants and variables inside a struct are called **properties** (e.g., `name`, `vacationRemaining`).
- Functions inside a struct are called **methods** (e.g., `employeeVacation`).
- When we create a var/let from a struct, it’s called an **instance** (e.g., `grantB`).
- The code used to create the instance is the **initializer**.

---

### Computed Properties

```swift
struct EmployeeComputed {
    let name: String
    var vacationAllocated = 14
    var vacationTaken = 0
    
    var vacationRemaining: Int {
        vacationAllocated - vacationTaken
    }
}
```

> Now we can read vacation remaining without losing the initial 14 day allocation. This is probably the best way to write this struct.

---

### get/set

```swift
struct EmployeeComputedContinued {
    let name: String
    var vacationAllocated = 14
    var vacationTaken = 0
    
    var vacationRemaining: Int {
        get {
            vacationAllocated - vacationTaken
        }
        set {
            vacationAllocated = vacationTaken + newValue
        }
    }
}

var employeeExample = EmployeeComputedContinued(name: "grant")
employeeExample.vacationTaken = 7
employeeExample.vacationRemaining = 10
employeeExample.vacationAllocated // 17
```

> I dont think this is a great example, but now we can edit the vacationAllocated with the vacationRemaining method.
> `get` reads data. `set` writes data. 
> No `mutating` keyword is required with get/set.

---

## `willSet` and `didSet`

```swift
struct Game {
    var score = 0 {
        willSet {
            print("score is \(score)")      // 0
            newValue                        // 2
        }
        didSet {
            print("Score is now \(score)")  // 2
            oldValue                        // 0
        }
    }
}

var newGame = Game()
newGame.score = 2
```

> `willSet` runs **before** the value changes.  
> `didSet` runs **after** the value changes.

---

## Custom Initializers

```swift
struct Player {
    let name: String
    let number: Int
    
    init(name: String) {
        self.name = name
        number = Int.random(in: 1...99)
    }
}

let player = Player(name: "Grant")
```

> This is a **custom initializer**. All properties must be assigned values.  
> Swift also provides a **memberwise initializer** by default.

---

## Access Control: `private`

```swift
struct BankAccount {
    private var funds = 0
    
    mutating func deposit(_ amount: Int) {
        funds += amount
    }
    
    mutating func withdraw(_ amount: Int) {
        funds -= amount
    }
}
```

> The `private` keyword prevents direct access to `funds`. Before funds -= 100..... would work.

**Access Control Options:**
- `private`: Only accessible inside the struct.
- `fileprivate`: Only accessible within the current file.
- `public`: Accessible anywhere.
- `private(set)`: Readable from outside, writable only within the struct.

---

## Static Properties and Methods

```swift
struct AppData {
    static let version = "1.3 beta 2"
    static let saveFilename = "settings.json"
    static let homeURL = "https://www.hackingwithswift.com"
}

AppData.version // ➡️ "1.3 beta 2"

struct Employee {
    let username: String
    let password: String

    static let example = Employee(username: "cfederighi", password: "hairforceone")
}

Employee.example // ➡️ returns example employee. I will use this to make default profiles for designing.
```

> Use `static` for shared constants, examples, or utility methods.

---

## Practice Example: Car Struct

```swift
struct Car {
    let make: String
    let model: String
    let seats: Int
    private(set) var gear = 0 {
        didSet {
            print("Gear is now \(gear)")
        }
    }
    
    mutating func shiftUp() {
        if gear < 7 {
            gear += 1
        } else {
            print("hhhkkkkrrrrrrrssssccrratccchhhhh")
        }
    }
    
    mutating func shiftDown() {
        if gear > 0 {
            gear -= 1
        } else {
            print("that was expensive")
        }
    }
}

var myCar = Car(make: "Porsche", model: "987", seats: 2)
myCar.shiftDown()
myCar.shiftUp()
```
