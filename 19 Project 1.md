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
