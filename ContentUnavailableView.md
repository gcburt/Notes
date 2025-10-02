> Not sure if this will be a view for launch or just a missing data screen. I'll use it during the onboarding process.

```swift
struct ContentUnavailable: View {
    var body: some View {
        ContentUnavailableView {
            Label("Rounds", systemImage: "swift")
        } description: {
            Text("Loading.")
        } actions: {
            Button("Do something") {
                // idk more stuff
            }
            .buttonStyle(.borderedProminent)
        }
    }
}
```
<img height="300" alt="Screenshot 2025-10-02 at 2 07 18 PM" src="https://github.com/user-attachments/assets/e8203bdd-375a-472a-9976-925e2c6badce" />
