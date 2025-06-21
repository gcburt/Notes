
## Classes


```swift
class Employee {
    let hours: Int
    
    init(hours: Int) {
        self.hours = hours
    }
    
    func hoursWorked() {
        print("i work \(hours) hours")
    }
}

class Manager: Employee {
    func work() -> String {
        "Managing..."
    }
}

final class Developer: Employee {
    func code() -> String {
        "Coding..."
    }
    
    override func hoursWorked() {
        print("i work \(hours) hours \(code())")
    }
}

let grant = Developer(hours: 160)
grant.hoursWorked()
```

**Breakdown:**

- 1. class looks identical to a struct.  
- 2. It requires an initializer.  
- 3. The function hoursWorked() is in the master class. It is inherited into the child classes  
- 4. The developer class contains an override to hoursWorked(). It will run instead.  
- 5. The developer class is *final*. Making classes final by default leads to performnce increases. Individual methods can also be marked final.

---

## Class initializers

```swift
class Vehicle {
    let isElectric: Bool
    
    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}

class Car: Vehicle {
    let isConvertible: Bool
    
    init(isElectric: Bool, isConvertable: Bool) {
        self.isConvertible = isConvertable // Format: type name = parameter // let isConvertable = true
        super.init(isElectric: isElectric)
    }
}
```

**Breakdown:**

- 1. The Car class has an additional property, isConvertable.  
- 2. It doesn't have a default value, so it must be initialized.  
- 3. Because it requires an initializer, super.init is required to inherit the master class's init.

---

## Copying classes

```swift
class UserProfile {
    var username = "Anonymous"
}

var user1 = UserProfile() // This is an initializer. It requires ().
var user2 = user1

user2.username =  "Swift"
user1.username // "Swift"

// Swift is updated everywhere.
```

```swift
class UserProfileCopy {
    var username = "Anonymous"
    
    func copy() -> UserProfileCopy {
        let user = UserProfileCopy()
        user.username = username
        return user
    }
}
```

// This allows us to create unique Users on the fly.

---

## Deinitialization

```swift
class UserDeinitialized {
    let id: Int

    init(id: Int) {
        self.id = id
        print("User \(id): I'm alive!")
    }

    deinit {
        print("User \(id): I'm dead!")
    }
}

for i in 1...3 {
    let user = UserDeinitialized(id: i)
    print("User \(user.id): I'm in control.")
}
```

```text
// User 1: I'm alive!
// User 1: I'm in control.
// User 1: I'm dead!
// User 2: I'm alive!
// User 2: I'm in control.
// User 2: I'm dead!
// User 3: I'm alive!
// User 3: I'm in control.
// User 3: I'm dead!
```

```swift
var users = [UserDeinitialized]()

for i in 1...3 {
    let user = UserDeinitialized(id: i)
    print("User \(user.id): I'm in control!")
    users.append(user)
}

print("Loop is finished!")
users.removeAll()
print("Array is clear!")
```

```text
// User 1: I'm alive!
// User 1: I'm in control!
// User 2: I'm alive!
// User 2: I'm in control!
// User 3: I'm alive!
// User 3: I'm in control!
// Loop is finished!
// User 1: I'm dead!
// User 2: I'm dead!
// User 3: I'm dead!
// Array is clear!
```

