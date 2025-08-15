```swift
public enum Result<Success, Failure> where Failure: Error {
    case success(Success)
    case failure(Failure)
}

var result: Result<Void, Error>?
```
`<Success, Failure>` are placeholder types. They could be intigers, strings, (), whatever.
My variable assigns the placeholders types values of Void and Error.

```swift
if let result {
    switch result {
        case .success:
            Text("Check your inbox.")
        case .failure:
            Text("Something went wrong")
    }
}
```

If i add my switch statement, I can now add functionality to my enum.

```swift
if let result {
    switch result {
        case .success:
            Text("Check your inbox.")
        case .failure(let someError):
            Text(someError.localizedDescription).foregroundStyle(.red)
    }
}
```

I can go even further by assigning the .faliure value to a constant. 
