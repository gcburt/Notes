## Comparable

### Important!
> Equatable is a completely different protocol. TBD

```swift
struct User: Comparable {
    var firstName: String
    var lastName: String
    
    static func <(lhs: User, rhs: User) -> Bool {
        lhs.lastName < rhs.lastName
    }
}
```

> In order for this struct to conform to comparable, the static function `<` is required. lhs/rhs (left/right hand side) are coding conventions.

```swift
struct ContentView: View {
    let users: [User] = [
        User(firstName: "Grant", lastName: "Burton"),
        User(firstName: "Amanda", lastName: "Watson"),
        User(firstName: "Julie", lastName: "Dean")
    ].sorted()
    
    var body: some View {
        List(users) { user in
            Text("\(user.lastName), \(user.firstName)")
        }
    }
}
```

> To call it, just use the built in sorted function on the array.

<img width="336" height="708" alt="Screenshot 2025-11-19 at 9 46 19 AM" src="https://github.com/user-attachments/assets/e3efa110-cfae-4b5d-a6cf-ef55054a8a4b" />
