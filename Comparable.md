## Comparable

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
