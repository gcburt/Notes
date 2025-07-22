## Using the ternary operator/ aka conditional modifiers

```swift
struct ContentView: View {
    let familyMembers = ["Grant", "Hunter", "Amanda", "Mike", "Scott", "Julie"]
    @State private var yourName: String = ""
    
    var body: some View {
        Form {
            Section("What is your name?") {
                Picker("Name", selection: $yourName) {
                    ForEach(familyMembers, id: \.self) { a in
                        Text("\(a)")
                    }
                }
            }
            Text(yourName)
                .bold(yourName == "Grant" ? true : false)
        }
    }
}
```
> `.bold(yourName == "Grant" ? true : false)` WTF
<img width="150" alt="Screenshot 2025-07-08 at 1 45 24 PM" src="https://github.com/user-attachments/assets/eb8bef13-67e2-4c13-9606-e004cc24077a" />

## Environmental modifiers

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Form {
                Text("One")
                Text("Two")
                    .font(.largeTitle)
                Text("Three")
                Text("Four")
                Text("Five")
            }
        }
        .font(.footnote)
    }
}
```
> Some modifiers can be applied on containers, ex. VStack. They can sometimes be overridden by applying a different modifier to the child View. Doesn't always work. Not all modifiers are environmental and there's no convenient way to know ahead of time.

<img width="233" alt="Screenshot 2025-07-08 at 1 53 40 PM" src="https://github.com/user-attachments/assets/e6a2db86-1217-406f-ae5c-e5965eb94c3b" />

## Creating views as properties
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
> **Views** can be created outside of the main *body:* property. Create a new property, assign some functionality, and add it to the main *body:*. `@ViewBuilder` is how i'm going to do it.

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

## Creating custom Views

```swift
struct ContentView: View {
    var body: some View {
        VStack(spacing: 10) {
            CapsuleView(textBox: "First")
            CapsuleView(textBox: "Second")
                .foregroundStyle(.black) // Doesn't work
            CapsuleView(textBox: "Third")
                .opacity(0.5) // 
        }
    }
}

struct CapsuleView: View {
    var textBox: String
    
    var body: some View {
        Text(textBox)
            .font(.largeTitle)
            .padding()
            .foregroundStyle(.white)
            .background(.blue)
            .clipShape(.capsule)
    }
}
```
> I have created a whole new struct that conforms to view. I'm passing it in the body property.
1. `.foregroundStyle(.black)` doesn't work because it has already been assigned in the CapsuleView.
2. `opacity(0.5)` has not been previously assigned.
<img width="150" alt="Screenshot 2025-07-08 at 2 09 12 PM" src="https://github.com/user-attachments/assets/e5481bce-3886-46b4-8ed5-5dd1fa32f480" />

## Creating custom modifiers
```swift
struct ContentView: View {
    var body: some View {
        VStack(spacing: 10) {
            Text("Sup")
                .modifier(Title())
        }
    }
}

struct Title: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .padding()
            .foregroundStyle(.white)
            .background(.blue)
            .clipShape(.rect(cornerRadius: 10))
    }
}
```
> `struct Title: ViewModifier { func body(content: Content) -> some View {` is just the new flavor of `struct ContentView: View { var body: some View {`

<img width="233" alt="Screenshot 2025-07-08 at 2 54 24 PM" src="https://github.com/user-attachments/assets/593e55b1-3cb5-4fcd-a828-d4492bbd4fb6" />

#### Level up with an extension

```swift
struct ContentView: View {
    var body: some View {
        VStack(spacing: 10) {
            Text("Sup")
                .titleStyle()
        }
    }
}

struct Title: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .padding()
            .foregroundStyle(.white)
            .background(.blue)
            .clipShape(.rect(cornerRadius: 10))
    }
}

extension View {
    func titleStyle() -> some View {
        modifier(Title())
    }
}
```

> Same result, but now i type `.titleStyle()` instead of `.modifier(Title())` This is the "Correct" way.

#### Level up again with custom parameters

```swift
struct ContentView: View {
    var body: some View {
        Text("sup")
            .modifier(TitleView())
            .watermarked(text: "BURTON")
    }
}

struct TitleView: ViewModifier {
    func body(content: Content) -> some View {
        content
            .padding(40)
            .font(.title)
            .background(.blue)
    }
}

struct WatermarkView: ViewModifier {
    let text: String
    
    func body(content: Content) -> some View {
        
        
        ZStack(alignment: .bottomTrailing) {
            content
            
            Text(text)
                .background(.black)
                .foregroundStyle(.white)
        }
    }
}

extension View {
    func watermarked(text: String) -> some View {
        modifier(WatermarkView(text: text))
    }
}
```
> This is getting harder. I'm passing a parameter into another parameter.
<img width="239" alt="Screenshot 2025-07-08 at 5 40 53 PM" src="https://github.com/user-attachments/assets/4f84d994-6bb7-4e5f-830e-3c7b216ba309" />
