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
                NavigationLink("Next page") { PageTwo(person: $person, newName: $newName) }
            }
        }
    }
}

//@Observable
struct Person {
    var name: String = "Grant"
}

struct PageTwo: View {
    @Binding var person: Person
    
    @Binding var newName: String
    var body: some View {
        Form {
            Text(person.name)
            TextField("Name:", text: $newName)
            Button("Submit") {
                person.name = newName
            }
        }
    }
}
```


> If I want my @State variable to be connected to another variable in another view, use @binding in conjunction with a $. Now, when I pass my value into the second view, I can change it from both locations and it will look in memory at the same location.

> `@Observable` monitors the classes content for changes.
