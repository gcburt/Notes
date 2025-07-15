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

## DatePicker

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
# Better Sleep
```swift
import CoreML
import SwiftUI

struct ContentView: View {
    @State private var wakeUp = defaultWakeTime
    @State private var sleepAmount = 8.0
    @State private var coffeeAmount = 1
    
    @State private var alertTitle = ""
    @State private var alertMessage = ""
    @State private var showingAlert = false
    
    static var defaultWakeTime: Date {
        var components = DateComponents()
        components.hour = 7
        components.minute = 0
        return Calendar.current.date(from: components) ?? .now
    }
    
    func calculateBedTime() {
        do {
            let config = MLModelConfiguration()
            let model = try SleepCalculator(configuration: config)
            
            let components = Calendar.current.dateComponents([.hour, .minute], from: wakeUp)
            let hour = (components.hour ?? 0) * 3600 // converting from seconds to hours w/ a nil c
            let minute = (components.minute ?? 0) * 60
            
            let prediction = try model.prediction(wake: Double(hour + minute), estimatedSleep: sleepAmount, coffee: Double(coffeeAmount))
            
            let sleepTime = wakeUp - prediction.actualSleep // actualSleep came from the SleepCalculator class
            
            alertTitle = "Bedtime is"
            alertMessage = sleepTime.formatted(date: .omitted, time: .shortened)
        } catch {
            alertTitle = "Error"
            alertMessage = "Try again"
        }
        
        showingAlert = true
    }
    
    var body: some View {
        NavigationStack {
            VStack {
                Text("When do you want to wake up?")
                DatePicker("Please enter a time", selection: $wakeUp, displayedComponents: .hourAndMinute)
                    .labelsHidden()
                Text("How much sleep do you want?")
                Stepper("\(sleepAmount.formatted()) hours", value: $sleepAmount)
                Text("How much coffee do you drink?")
                Stepper("^[\(coffeeAmount) cup](inflect: true)", value: $coffeeAmount)
            }
            .navigationTitle("Better Sleep")
            .toolbar {
                Button("Enter", action: calculateBedTime)
            }
            .alert(alertTitle, isPresented: $showingAlert) {
                Button("OK") {}
            } message: {
                Text(alertMessage)
            }
        }
    }
}
```
> There were a lot of new concepts in this one. The two biggest ones were CoreML/CreateML and the Date struct. Some key takeaways.
1. static let/var is a property assigned to the ContentView struct itself. It doesn't require outside input and is not going to be an initialized value. The non-static property *wakeUp* accesses the static property *defaultWakeTime*.
2. Date is a struct that contains many optional values. The struct calls them components. When you don't include them, they come back nil. Nil coalescence becomes pretty important using them.
3. CreateML is used to make a CoreML class. Watch the video if you start needing it.
4. `Stepper("^[\(coffeeAmount) cup](inflect: true)", value: $coffeeAmount)` This syntax makes cup(s) work
