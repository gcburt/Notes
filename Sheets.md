### Sheet

```swift
struct ContentView: View {
    @State var showSheet = false
    
    var body: some View {
        Text("First view")
        Button("Show sheet") {
            showSheet.toggle()
        }
        .sheet(isPresented: $showSheet) {
            SecondView()
        }
    }
}

struct SecondView: View {
    var body: some View {
        Text("Second view")
    }
}
```
<img width="150" alt="Screenshot 2025-08-17 at 1 27 45 PM" src="https://github.com/user-attachments/assets/d791cfd9-d693-4777-8bd3-6c9d082e5b96" />

> I have created a sheet. It stacks on top of the first view. It is a modifier on my button.

### Using @Environment to dismiss

```swift
struct ContentView: View {
    @State var showSheet = false
    
    var body: some View {
        Text("First view")
        Button("Show sheet") {
            showSheet.toggle()
        }
        .sheet(isPresented: $showSheet) {
            SecondView()
        }
    }
}

struct SecondView: View {
    @Environment(\.dismiss) var dismiss
    
    var body: some View {
        Text("Second view")
        Button("Dismiss") {
            dismiss()
        }
    }

}
```
<img width="150" alt="Screenshot 2025-08-17 at 1 32 25 PM" src="https://github.com/user-attachments/assets/8cbaba98-4cd3-4cf1-a567-faec13255277" />

> This one is weird. Dismiss is somehow a function.
