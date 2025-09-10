## currency

```swift
struct ContentView: View {
    @State private var money: Int = 0
    
    var body: some View {
        Form {
            TextField("Money", value: $money, format: .currency(code: Locale.current.currency? .identifier ?? "USD"))
                .keyboardType(.decimalPad)
        }
    }
}
```

- This `TextField` uses a currency. Not only is it not a string, it's a special intiger. The format is `.currency(code: "USD")`
- Locale is a struct with many paramers.
- `.current.currency? .identifier` returns the current currency three letter identifier.
- `?? "USD"` is the nil coalescing operator.

<img width="200" alt="Screenshot 2025-07-02 at 11 41 28 PM" src="https://github.com/user-attachments/assets/91ddbac7-e573-4e1c-a400-21a0727141bc" />


## Reusable shorthand

```swift
let code = Locale.current.currency?.identifier ?? "USD"
Text(money, format: .currency(code: code))
```

## Decimal

> Whenever working with money, use the `Decimal` type instead of Int, Double, Float, etc. It doesn't round at all.
