#### Base list

```swift
struct ContentView: View {
    @State private var numbers = [Int]()
    @State private var currentNumber = 1

    var body: some View {
        VStack {
            List {
                ForEach(numbers, id: \.self) {
                    Text("Row \($0)")
                }
            }

            Button("Add Number") {
                numbers.append(currentNumber)
                currentNumber += 1
            }
        }
    }
}
```
<img width="150" alt="Screenshot 2025-08-18 at 1 19 01 PM" src="https://github.com/user-attachments/assets/e4b38674-e743-4b36-be6f-9b35a61e4347" />

> First, start with a basic list. ForEach is required to remove rows. Quirk of the language.

### Deleting rows

```swift
struct ContentView: View {
    @State private var numbers = [Int]()
    @State private var currentNumber = 0
    
    var body: some View {
        NavigationStack {
            VStack {
                List {
                    ForEach(numbers, id: \.self) {
                        Text("\($0)")
                    }
                    .onDelete(perform: removeRows)
                }
                Button("Add") {
                    numbers.append(currentNumber)
                    currentNumber += 1
                }
            }
            .toolbar {
                EditButton()
            }
        }
    }
    
    func removeRows(at offsets: IndexSet) {
        numbers.remove(atOffsets: offsets)
    }
}
```
<img width="150" alt="Screenshot 2025-08-18 at 1 19 51 PM" src="https://github.com/user-attachments/assets/ac05b215-b897-4b5f-b1a7-126c15b6e94a" />

1. `.onDelete(perform: removing function)` is a modifier that goes on the end of the ForEach.
2. `func removeRows(at offsets: IndexSet)` is a function that removes rows at the IndexSet. IndexSet is similar to a regular Set, but it's ordered.
3. `EditButton()` is a swift provided function that adds the edit button to the top. Not required.
