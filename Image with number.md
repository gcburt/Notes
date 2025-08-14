```swift
struct ContentView: View {
    var number = 5
    var name = "Grant"
    
    var body: some View {
        HStack {
            Image(systemName: "\(number).circle")
            Text(name)
        }
    }
}
```
