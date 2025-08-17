```swift
@Observable
class User {
    var name = "Grant"
}

struct ContentView: View {
    @State var user = User()
    
    var body: some View {
        Form {
            Text(user.name)
            TextField("Name", text: $user.name)
        }
    }
}
```
<img width="150" alt="Screenshot 2025-08-17 at 12 53 57 PM" src="https://github.com/user-attachments/assets/89a4864f-6520-4b18-955e-30427b5d235f" />

> State monitors changes in the User type. Technically, the User class isn't changing. The variables are. If i want my `@State` variable to watch my class, I need to add @Observable. 
