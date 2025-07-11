## Stepper

```swift
struct ContentView: View {
    @State private var steppingNumber: Double = 0.0
    
    var body: some View {
        Form {
            Stepper("\(steppingNumber.formatted())", value: $steppingNumber, in: 0...10, step: 1.25)
        }
    }
}
```
1. `formatted()` removes extra 0's
2. `value:` binds to a variable
3. `in:` is the range
4. `step:` is the interval.
<img width="150" alt="Screenshot 2025-07-09 at 2 52 29 PM" src="https://github.com/user-attachments/assets/4251f26a-b3d8-4bbf-9251-6de95f389c2e" />

## Time and date

```swift
struct ContentView: View {
    @State private var alarm = Date.now
    
    var body: some View {
        DatePicker("Alarm time", selection: $alarm)
    }
}
```
<img width="237" alt="Screenshot 2025-07-09 at 3 22 14 PM" src="https://github.com/user-attachments/assets/3857ac6c-905d-4167-9945-69bd9da05140" />

```swift
struct ContentView: View {
    @State private var alarm = Date.now
    
    var body: some View {
        DatePicker("Alarm time", selection: $alarm, displayedComponents: .hourAndMinute)
            .labelsHidden()
    }
}
```

<img width="229" alt="Screenshot 2025-07-09 at 3 23 06 PM" src="https://github.com/user-attachments/assets/f48250fe-36f2-4f93-8988-b5f7c27e9592" />

```swift
struct ContentView: View {
    @State private var alarm = Date.now
    
    var body: some View {
        DatePicker("Alarm time", selection: $alarm, in: Date.now..., displayedComponents: .date)
            .labelsHidden()
    }
}
```
- `in: Date.now...` provides a range starting now to infinity.
<img width="150" alt="Screenshot 2025-07-09 at 3 43 02 PM" src="https://github.com/user-attachments/assets/9c4c1c33-4fca-4134-a1ea-d9183b297745" />

```swift
func exampleDate() {
    let tomorrow = Date.now.addingTimeInterval(86400)
    let range = Date.now...tomorrow
}
```

- an example of `.addingTimeInterval(Int)` 86400 is the amount of seconds in a day.

  
