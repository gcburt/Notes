## .disabled

```swift
struct ContentView: View {
    @State private var name = ""
    
    var body: some View {
        Form {
            TextField("Enter name", text: $name)
            Button("Enter") {}
                .disabled(name.isEmpty)
        }
    }
}
```
> You could make a conputed property with a bunch of stuff too.
<img height="300" alt="Screenshot 2025-09-09 at 11 25 54 AM" src="https://github.com/user-attachments/assets/31261659-30b2-43f9-8620-a2ae454e8277" />
<img height="300" alt="Screenshot 2025-09-09 at 11 26 04 AM" src="https://github.com/user-attachments/assets/feb81c7f-2311-4f25-8f8f-097e380e2a5f" />
