## Lists
> Lists make, well... lists. 
```swift
struct ContentView: View {
    var body: some View {
        List {
            Text("One")
            Text("Two")
            Text("Three")
            
            ForEach(0...5, id: \.self) {
                Text("\($0)")
            }
        }
        .listStyle(.grouped)
    }
}
```
1. `.listStyle()` has a bunch of modifiers. They're subtle.
   
<img width="150" height="355" alt="Screenshot 2025-07-15 at 3 21 24 PM" src="https://github.com/user-attachments/assets/771e28c8-554d-4704-b618-e23b8d9a3dd7" />

```swift
struct ContentView: View {
    var body: some View {
        List(1...5, id: \.self) {
            Text("Test box")
            
            Text("\($0)")
        }
    }
}
```
> Unlike Form, Lists can create their own lines without ForEach. This also works on arrays.
<img width="150" height="355" alt="Screenshot 2025-07-15 at 3 27 47 PM" src="https://github.com/user-attachments/assets/144411f1-de1a-447d-bffd-b6beb1f86321" />

## Loading files from a bundle

```swift
struct ContentView: View {
    var body: some View {}
    
    func testBundle() {
        if let fileURL = Bundle.main.url(forResource: "somefile", withExtension: "txt") {
            if let fileContents = try? String(contentsOf: fileURL, encoding: .utf8) {
                // we loaded the file into a String
            }
        }
    }
}
```
> I have no idea
