```
struct ContentView: View {
    @AppStorage("notes") private var notes = ""
    
    var body: some View {
        Form {
            TextEditor(text: $notes)
        }
    }
}
```
> @State works too. TextEditor is for big blocks of text with multiple lines. Make sure to wrap it inside a form or navstack. 
<img width="150" alt="Screenshot 2025-09-11 at 10 33 50 AM" src="https://github.com/user-attachments/assets/475172d9-2fa3-4413-9496-3b2257e33db7" />

```swift
struct ContentView: View {
    @State private var notes = ""
    
    var body: some View {
        Form {
            TextField("Enter text", text: $notes, axis: .vertical)
        }
    }
}
```

> If you want to use a textfield that grows with typing, add an axis.
