# 🏛️ Classes & Inheritance in Swift  
<br/>

## 🏗️ Defining a Class

```swift
class Animal {
    var name: String

    init(name: String) {
        self.name = name
    }

    func speak() {
        print("\(name) makes a sound")
    }
}
```

- `class` keyword defines a reference type.  
- Use `init` for initialization.  
- Methods and properties belong to instances.

<br/>

## 🚶‍♂️ Creating & Using Instances

```swift
let creature = Animal(name: "Fido")
creature.speak()   // ➡️ :arrow_right: "Fido makes a sound"
```

- Classes are **reference types**: multiple variables can reference the same instance.

```swift
let pet1 = creature
pet1.name = "Rex"
print(creature.name) // ➡️ :arrow_right: "Rex" (both refer to same object)
```

<br/>

## 🧬 Inheritance

```swift
class Dog: Animal {
    var breed: String

    init(name: String, breed: String) {
        self.breed = breed
        super.init(name: name)   // call superclass initializer
    }

    override func speak() {
        print("\(name) barks")    // overrides parent method
    }
}

let dog = Dog(name: "Buddy", breed: "Beagle")
dog.speak()        // ➡️ :arrow_right: "Buddy barks"
```

- Subclass with `class Subclass: Superclass`.  
- Use `override` to change inherited methods.  
- Call `super` to access parent behavior.

<br/>

## 🔒 Preventing Inheritance

```swift
final class Cat: Animal {
    override func speak() {
        print("\(name) meows")
    }
}

// class BigCat: Cat {} // ❌ :X: cannot inherit from final class 'Cat'
```

- `final` stops other classes from subclassing.

<br/>

## 🚀 Overriding Properties

```swift
class Rectangle {
    var width: Double
    var height: Double

    init(w: Double, h: Double) {
        width = w; height = h
    }

    var area: Double {
        return width * height
    }
}

class Square: Rectangle {
    override var area: Double {
        return width * width   // specialized computation
    }
}

let square = Square(w: 4, h: 4)
print(square.area)  // ➡️ :arrow_right: 16
```

- You can override **computed** properties with `override var`.

<br/>

## 🛠️ Deinitializers

```swift
class Tracker {
    let id: Int

    init(id: Int) {
        self.id = id
        print("Tracker \(id) created")
    }

    deinit {
        print("Tracker \(id) destroyed")
    }
}

for i in 1...2 {
    let t = Tracker(id: i)
}
// ➡️ :arrow_right: "Tracker 1 created"
// ➡️ :arrow_right: "Tracker 2 created"
// ➡️ :arrow_right: "Tracker 2 destroyed"
// ➡️ :arrow_right: "Tracker 1 destroyed"
```

- `deinit` runs when an instance is deallocated (reference count hits zero).

<br/>

## 🔍 Type Checking & Casting

```swift
if dog is Animal {
    print("Dog is an Animal")           // ➡️ :arrow_right: true
}

if let someAnimal = dog as? Animal {
    someAnimal.speak()                 // ➡️ :arrow_right: "Buddy barks"
}
```

- Use `is` to check type.  
- Use `as?` for conditional downcast.  
- Use `as!` for forced downcast (crashes if invalid).

<br/>

---

✅ **Practice:**  
- Create a base class `Vehicle` with `speed` and `drive()` method.  
- Subclass `Car` and `Bicycle`, override `drive()` with custom behavior.  
- Experiment with `final` and observe deinitializer calls.  
