```swift
struct ContentView: View {
    @State private var tapCount = UserDefaults.standard.integer(forKey: "Tap")
    
    var body: some View {
        Button("Tap Count: \(tapCount)") {
            tapCount += 1
            
            UserDefaults.standard.set(tapCount, forKey: "Tap")
        }
    }
}
```

`UserDefaults.standard.set(tapCount, forKey: "Tap")` gets attached to a button. It's linked to my variable.

```swift
struct ContentView: View {
    @AppStorage("AnyName") private var tapCount = 0
    
    var body: some View {
        Button("Tap Count: \(tapCount)") {
            tapCount += 1
        }
    }
}
```

`@AppStorage("AnyName")` Property wrappers work too. Single line of code.
