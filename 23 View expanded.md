## Creating a new body property
```swift
struct ContentView: View {
    let singleLine = Text("Single line...")
    
    @ViewBuilder var doubleLine1: some View {
        Text("Option 1")
        Text("has same attributes as body:")
    }
    
    var doubleLine2: some View {
        VStack{
            Text("Option 2")
            Text("is just a VStack.")
        }
    }
    
    var doubleLine3: some View {
        Group {
            Text("Option 3")
            Text("is a group.")
        }
    }
    var body: some View {
        VStack(spacing: 30) {
            singleLine
            doubleLine1
            doubleLine2
            doubleLine3
        }
    }
}
```
> **Views** can be created outside of the *body:* property. You can just create a *new property* to add to the existing and required *body: property*. This example has 4 custom properties alongside the main *body:* property.
1. `singleLine` is simply a single line.
2. `doubleLine1` contains two Text boxes. `@ViewBuilder` applies all the same `body:` properties and methods to the custom property.
3. `doubleLine2` is just a `VStack` For all intents and purposes, its basically the same as `singleLine`
4. `doubleLine3` uses a Group. I don't really know what that does yet. The format gets moved around differently.
<img width="150" alt="Screenshot 2025-07-07 at 1 36 08 PM" src="https://github.com/user-attachments/assets/f9492e70-5271-42fc-b969-6009ffa6913f" />

## Creating a new View

```swift
struct ContentView: View {
    
    struct CustomText: View {
        var text: String
        
        var body: some View {
            Text(text)
                .frame(width: 200, height: 100)
                .background(.red)
                .foregroundStyle(.white)
                .font(.title)
        }
    }
    
    var body: some View {
        VStack {
            Text("Text")
                .frame(width: 200, height: 100)
                .background(.red)
                .foregroundStyle(.white)
                .font(.title)
            
            CustomText(text: "Also Text")
        }
    }
}
```

<img width="150" alt="Screenshot 2025-07-07 at 2 05 21 PM" src="https://github.com/user-attachments/assets/618c766f-cea8-4439-a50a-96a53cf35e6e" />
