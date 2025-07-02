```swift
import SwiftUI

struct ContentView: View {
    
    @State private var inputValue: Double = 0
    @State private var measurementType: MeasurementType = .fahrenheit
    
    enum MeasurementType {
        case fahrenheit
        case celsius
        case kelvin
    }
    
    var fahrenheit: Double {
        if measurementType == .fahrenheit {
            return inputValue
        } else if measurementType == .celsius {
            return inputValue * 9 / 5 + 32
        } else if measurementType == .kelvin {
            return inputValue * 9 / 5 - 459.67
        } else {
            return 0.0
        }
    }
    
    var celsius: Double {
        if measurementType == .fahrenheit {
            return (inputValue - 32) * 5 / 9
        } else if measurementType == .celsius {
            return inputValue
        } else if measurementType == .kelvin {
            return inputValue - 273.15
        } else {
            return 0.0
        }
    }
    
    var kelvin: Double {
        if measurementType == .fahrenheit {
            return (inputValue - 32) * 5 / 9 + 273.15
        } else if measurementType == .celsius {
            return inputValue + 273.15
        } else if measurementType == .kelvin {
            return inputValue
        } else {
            return 0.0
        }
    }
    
    var body: some View {
        NavigationStack {
            Form {
                Section("Input Temperature") {
                    TextField("Input Temperature", value: $inputValue, format: .number)
                    
                    Picker("Measurement Type", selection: $measurementType) {
                        Text("Fahrenheit").tag(MeasurementType.fahrenheit)
                        Text("Celsius").tag(MeasurementType.celsius)
                        Text("Kelvin").tag(MeasurementType.kelvin)
                    }
                    .pickerStyle(SegmentedPickerStyle())
                }
                
                Section("Fahrenheit") {
                    Text(fahrenheit, format: .number)
                }
                
                Section("Celsius") {
                    Text(celsius, format: .number)
                }
                
                Section("Kelvin") {
                    Text(kelvin, format: .number)
                }
            }
            .navigationBarTitle("Temperature Conversion")
            .navigationBarTitleDisplayMode(.inline)
        }
    }
}

#Preview {
    ContentView()
}
```

# 🧱 SwiftUI Basics 
<br/>

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundStyle(.tint)
            Text("Hello, world!")
        }
        .padding()
    }
}

#Preview {
    ContentView()
}
```
<img width="279" alt="Screenshot 2025-07-01 at 2 52 36 PM" src="https://github.com/user-attachments/assets/50c98b19-1fa8-43af-9194-cbadaf64edc3" />


### 1. `import SwiftUI`  
Loads the **SwiftUI framework**, which gives you tools to build user interfaces.  
Swift only loads what you ask for, so you must import what you need.

<br/>

### 2. `struct ContentView: View`  
Defines a screen layout named `ContentView`.  
It follows the **`View` protocol**, which means it can display content like text, images, or buttons.

<br/>

### 3. `var body: some View`  
This is a required property for anything using `View`.  
It returns the content you want to show.  
- `some View` means it returns *something* that conforms to `View`.

<br/>

### 4. `VStack`, `Image`, `Text`  
- `VStack`: stacks views vertically  
- `Image(systemName: "globe")`: uses an icon from Apple’s **SF Symbols**  
- `Text("Hello, world!")`: displays simple text on the screen

<br/>

### 5. `.imageScale()`, `.foregroundStyle()`, `.padding()`  
Methods that change how views look or behave are called *modifiers*.

Example:
```swift
Image(systemName: "globe")
    .imageScale(.large)
    .foregroundStyle(.blue)

Text("Hello, world!")
    .padding()
```


## Creating a Form
> Forms are scrolling lists of static controls like text and images, but can also include user interactive controls like text fields, toggle switches, buttons, and more.

```swift
struct ContentView: View {
    var body: some View {
        Form {
            Section {
                Text("This is a \"Text\" view")
            }
            
            Section {
                Text("with two Sections.")
            }
        }
    }
}
```

<img width="275" alt="Screenshot 2025-07-01 at 2 58 01 PM" src="https://github.com/user-attachments/assets/76b777ed-6c41-418d-bb8b-f268bc0555ae" />

## Adding a Navigation Bar

`NavigationStack`
> "A view that displays a root view and enables you to present additional views over the root view." It's comparable to the spine of a book. It is structural, but doesn't contain any visible information.

```swift
struct ContentView: View {
    var body: some View {
        NavigationStack {
            Form {
                Section {
                    Text("This is a \"Text\" view")
                }
                
                Section {
                    Text("with two Sections.")
                }
            }
            .navigationTitle(".navigationTitle")
            .navigationBarTitleDisplayMode(.inline)
        }
    }
}
```

- The navigation bar is attached to the first visible `View` inside the `NavigationStack`. In this instance, it's a `Form`.
- The `.navigationBarTitleDisplayMode()` contains 3 options.

<img width="269" alt="Screenshot 2025-07-01 at 3 28 08 PM" src="https://github.com/user-attachments/assets/a5a7fa8c-04d0-4589-b510-6c2cb0ae537a" />

##
