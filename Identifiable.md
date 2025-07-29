Identifiable protocol

```swift
protocol Identifiable {
    associatedtype ID: Hashable
    var id: ID { get }
}

```

> Part of User creation. Identifiable is a protocol that requires some type of hashable ID value. You can make your own (usernames), or you can use a UUID.

```swift
struct User: Identifiable {
   let id = UUID()
   let name: String
}
```

> Now name can be repeated.
