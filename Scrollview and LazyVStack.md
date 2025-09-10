## ScrollView (vertical)

```swift
struct ContentView: View {
    var body: some View {
        ScrollView {
            VStack(spacing: 10) {
                ForEach(0..<100) {
                    Text("\($0)")
                }
            }
            .frame(maxWidth: .infinity)
        }
    }
}
```

> Makes a scrolling view. When views are added, they're rendered immediately, regardless of whether or not the user can see them. If you upload 1000 profiles, that could be an issue.
> `.frame(maxWidth: .infinity` is not `.frame(width: .infinity`. Width requires a specific CGFloat to work.
> 
<img width="150" alt="Screenshot 2025-08-22 at 3 33 45 PM" src="https://github.com/user-attachments/assets/6e26a6ef-9cfe-4135-b4ce-607304f39e1b" />

## ScrollView (horizontal)

```swift
struct ContentView: View {
    var body: some View {
        ScrollView(.horizontal) {
            HStack(spacing: 10) {
                ForEach(0..<100) {
                    Text("\($0)")
                }
            }
        }
    }
}
```

> Horizontal scrollviews require the `.horizontal` parameter.

<img width="150" alt="Screenshot 2025-08-22 at 3 32 08 PM" src="https://github.com/user-attachments/assets/3c4a45dd-b932-4de7-b18c-4f0e232491a8" />

## .basedOnSize

```swift
.scrollBounceBehavior(.basedOnSize)
```

> Add this modifier to disable scrollview when the view fits inside the screen.

## LazyVStack

```swift
struct ContentView: View {
    var body: some View {
        ScrollView {
            LazyVStack(spacing: 10) {
                ForEach(0..<100) {
                    Text("\($0)")
                }
            }
//            .frame(maxWidth: .infinity)
        }
    }
}
```

> - LazyVStacks only render what is shown. Far better for optimization in certain cases.
> - Note that the .frame isn't used. Lazy VStack(s) take up all available space. It makes sense. What if the new views get progressively larger? It would look weird.

<img width="150" alt="Screenshot 2025-08-22 at 3 34 36 PM" src="https://github.com/user-attachments/assets/08127923-1b02-490a-a91c-d87780a8efa5" />
