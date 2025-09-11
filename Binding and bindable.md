## Bindable

> `@bindable` is used in conjjunction with the @Observable macro. It is ised to pass entire classes around.

> `@Binding` is used to pass around simple variables.

```swift
struct ContentView: View {
    @State private var rememberMe = false
    
    var body: some View {
        Toggle("Remember me", isOn: $rememberMe)
            .padding()
        PushButton(title: "Remember Me", isOn: $rememberMe)
        
    }
}

struct PushButton: View {
    let title: String
    @Binding var isOn: Bool
    
    var onColors = [Color.red, Color.yellow]
    var offColors = [Color(white: 0.6), Color(white: 0.4)]
    
    var body: some View {
        Button(title) {
            isOn.toggle()
        }
        .padding()
        .background(LinearGradient(colors: isOn == true ? onColors : offColors, startPoint: .top, endPoint: .bottom))
        .foregroundStyle(.white)
        .clipShape(.capsule)
        .shadow(radius: isOn ? 0 : 5)
    }
}
```

> Both buttons are connected via @Binding. 
<img height="300" alt="Screenshot 2025-09-11 at 9 58 11 AM" src="https://github.com/user-attachments/assets/4f4ed8af-20ec-4fcf-8d2f-c13ca441cb45" />
<img height="300" alt="Screenshot 2025-09-11 at 9 58 25 AM" src="https://github.com/user-attachments/assets/9d2c8942-540f-463d-8332-b0a7737cc930" />

