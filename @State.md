# Structs in Swift

Structs contain properties, methods, and *mutating functions*. When a struct is initialized, all properties must have a value. var means a value can be modified. When a struct is created with a let constant *everything* downstream is locked.

## 1. @State

```swift
struct ClassesAndStructs: View {
    @State var person = Person()
//    let person = Person()
    
    @State var newName = ""
    
    var body: some View {
        NavigationView {
            Form {
                Text(person.name)
                TextField("Name:", text: $newName)
                Button("Submit") {
                    person.name = newName
                }
                NavigationLink("Next page") { PageTwo(person: person) }
            }
        }
    }
}

//@Observable
struct Person {
    var name: String = "Grant"
}
```

> Because a struct can be created with a let constant, variables inside could potentially be locked in and not freely modified. @State is a special container that stores the values outside of the struct, so that it may be modified. 

---

```swift
@Observable
class User {
    var name = "Grant"
}

struct ContentView: View {
    @State var user = User()
    
    var body: some View {
        Form {
            Text(user.name)
            TextField("Name", text: $user.name)
        }
    }
}
```
<img width="150" alt="Screenshot 2025-08-17 at 12 53 57 PM" src="https://github.com/user-attachments/assets/89a4864f-6520-4b18-955e-30427b5d235f" />

> State monitors changes in the User type. Technically, the User class isn't changing. The variables are. If i want my `@State` variable to watch my class, I need to add @Observable. 

> `@Observable` monitors the classes content for changes.
