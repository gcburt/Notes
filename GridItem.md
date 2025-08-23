## GridItem and LazyVGrid

```swift
struct ContentView: View {
    let layout = [
        GridItem(.fixed(80)),
        GridItem(.fixed(80)),
        GridItem(.fixed(80))
    ]
    var body: some View {
        ScrollView {
            LazyVGrid(columns: layout) {
                ForEach(0..<200) {
                    Text("\($0)")
                }
            }
        }
    }
}
```

> Pretty simple concept. The layout is fixed at 80 CGPoint(s)

<img width="150" alt="Screenshot 2025-08-22 at 4 17 12 PM" src="https://github.com/user-attachments/assets/d31af96e-4e25-459e-a39f-06359646d3a5" />

## Adaptive modifier

```swift
struct ContentView: View {
    let layout = [
        GridItem(.adaptive(minimum: 80))
    ]
    var body: some View {
        ScrollView {
            LazyVGrid(columns: layout) {
                ForEach(0..<200) {
                    Text("\($0)")
                }
            }
        }
    }
}
```

> `.adaptive` allows swift to modify the columns as needed. You can set minimum, maximum or both ranges. Especially useful for larger screens or landscape mode.
 
<img width="150" alt="Screenshot 2025-08-22 at 4 19 56 PM" src="https://github.com/user-attachments/assets/3064e406-fb9b-4c55-8caa-d8a0895fd4d6" />

## Horizontal

```swift
struct ContentView: View {
    let layout = [
        GridItem(.adaptive(minimum: 80))
    ]
    var body: some View {
        ScrollView(.horizontal) {
            LazyHGrid(rows: layout) {
                ForEach(0..<200) {
                    Text("\($0)")
                }
            }
        }
    }
}
```

> .horizontal, LazyHGrid, and (rows: ) are the required changes

<img width="150" alt="Screenshot 2025-08-22 at 4 24 44 PM" src="https://github.com/user-attachments/assets/263b6829-3101-47c7-a6dd-634f53deeea1" />

