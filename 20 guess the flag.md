```swift
struct ContentView: View {
    @State private var countries = ["Estonia", "France", "Germany", "Ireland", "Italy", "Nigeria", "Poland", "Spain", "UK", "Ukraine", "US"].shuffled()
    @State private var correctAnswer = Int.random(in: 0...2)
    @State private var score = 0
    @State private var gotWrongAnswer: Bool = false
    @State private var wrongAnswerChoice: String = ""
    @State private var questionNumber: Int = 0
    @State private var gameOver: Bool = false
    @State private var finalScore: Int = 0
    
    func answerQuestion(_ c: Int) {
        if c == correctAnswer {
            score += 1
            questionNumber += 1
            reshuffle()
            newGame()
        } else {
            wrongAnswerChoice = "\(countries[c])"
            gotWrongAnswer = true
        }
    }
    
    func reshuffle() {
        countries.shuffle()
        correctAnswer = Int.random(in: 0...2)
    }
    
    func newGame() {
        if questionNumber == 8 {
            finalScore = score
            gameOver = true
            score = 0
            countries.shuffle()
            correctAnswer = Int.random(in: 0...2)
            questionNumber = 0
        }
    }
    
    var body: some View {
        ZStack {
            LinearGradient(stops: [Gradient.Stop(color: .blue, location: 0.4), Gradient.Stop(color: .clear, location: 1.0)], startPoint: .top, endPoint: .bottom)
                .ignoresSafeArea()
            VStack(spacing: 20) {
                VStack {
                    VStack {
                    Text("Choose the flag for")
                        .foregroundStyle(.white)
                        .font(.subheadline.weight(.heavy))
                    Text(countries[correctAnswer])
                        .foregroundStyle(.white)
                        .font(.largeTitle.weight(.semibold))
                    Text("\(score)")
                        .foregroundStyle(.white)
                        .font(.largeTitle.weight(.medium))
                }
                    VStack {
                        ForEach(0...2, id: \.self) { c in
                            Button {
                                answerQuestion(c)
                            } label: {
                                Image(countries[c])
                                    .clipShape(.buttonBorder)
                                    .shadow(radius: 0.5)
                            }
                        }
                    }
                }
                .frame(maxWidth: .infinity)
                .padding(.vertical, 20)
                .background(.ultraThinMaterial)
                .clipShape(.rect(cornerRadius: 20))
            }
            .padding()
            .alert("Wrong", isPresented: $gotWrongAnswer) {
//                Button("I suck", role: .destructive) {}
                Button("I suck", role: .cancel) {
                    questionNumber += 1
                    reshuffle()
                    newGame()
                }
            } message: {
                Text("Thats the flag of \(wrongAnswerChoice)")
            }
            .alert("Game Over", isPresented: $gameOver) {
                Button("OK") {}
            } message: {
                Text("\(Double(finalScore) / 8.0)")
            }
        }
    }
}
```
<img width="250" alt="Screenshot 2025-07-05 at 10 00 09 PM" src="https://github.com/user-attachments/assets/e8edaabb-0efe-4d9b-b61d-0abf49f929f3" />



## VStack, HStack and ZStack
> These stacks arrange views vertically, horizontally and depthwise. Declaring views explicittly allows 3 things.
1. Spacing is now controlled
2. Allignment (.leading, etc.)
3. Prevents swiftUI from moving around freely

```swift
struct ContentView: View {
    var body: some View {
        VStack(alignment: .leading, spacing: 20) {
            Text("first text")
            Text("Second text is really long")
        }
    }
}
```
<img width="150" alt="Screenshot 2025-07-03 at 2 32 26 PM" src="https://github.com/user-attachments/assets/6d0cfd4a-dc5d-44c3-af84-b9ac552fa93f" />

## Spacer()
> Like a spring
```swift
struct ContentView: View {
    var body: some View {
        Spacer()
        
        VStack() {
            Text("first text")
            Text("Second text is really long")
        }
    }
}
```
<img width="150" alt="Screenshot 2025-07-03 at 2 52 48 PM" src="https://github.com/user-attachments/assets/8db187c0-6163-4eb3-aec2-91a8942e15f8" />

# Colors and Frames

## .background

```swift
struct ContentView: View {
    var body: some View {
        ZStack {
            Text("Your content")
        }
        .background(.red)
    }
}
```
> the .background(.red) modifier is coloring the entire ZStack View red.
<img width="150" alt="Screenshot 2025-07-03 at 3 01 02 PM" src="https://github.com/user-attachments/assets/b13ceb13-59fa-433d-877e-3961ac29c86b" />

```swift
struct ContentView: View {
    var body: some View {
        ZStack {
            Color.red
                .frame(width: 20, height: .infinity)
            Text("Your content")
        }
        .background(.red)
    }
}
```
- There's some weird shit happening here. The ZStack width is roughly 100. When i add the .background(.red) modifier to the Color.red View, it expands to fill the ZStack and ignored the safe area.
<img width="150" alt="Screenshot 2025-07-03 at 3 14 38 PM" src="https://github.com/user-attachments/assets/f8a8e6cc-c543-43f3-bb54-faf52140501b" />
<img width="150" alt="Screenshot 2025-07-03 at 3 18 22 PM" src="https://github.com/user-attachments/assets/1b28dcb0-65c5-4681-8fee-eb97dcdbf747" />
<img width="150" alt="Screenshot 2025-07-03 at 3 26 30 PM" src="https://github.com/user-attachments/assets/712f9ce3-bc93-4e56-b98b-a225422d697b" />

## Modifiers

```swift
struct ContentView: View {
    var body: some View {
        ZStack {
            VStack(spacing: 0) {
                Color.red
                Color.black
            }
            
            Text("Go Dawgs")
                .foregroundStyle(.secondary)
                .padding(50)
                .background(.ultraThinMaterial)
        }
        .ignoresSafeArea()
    }
}
```
- `Color.red` Shades in color **inside** the VStack.
- `.foregroundStyle(.secondary)` Changes the text color.
- `.background(.ultraThinMaterial)` adds the frosted glass look.
<img width="235" alt="Screenshot 2025-07-03 at 10 50 23 PM" src="https://github.com/user-attachments/assets/caa247c5-3095-4447-9072-a4bd8c52e34c" />

## Gradients
> 4 types of gradients. They consist of a type, color and direction.
#### LinearGradient

```swift
struct ContentView: View {
    var body: some View {
        LinearGradient(colors: [.red, .black], startPoint: .top, endPoint: .bottom)
    }
}
```
<img width="232" alt="Screenshot 2025-07-03 at 10 58 19 PM" src="https://github.com/user-attachments/assets/fcf114fb-f33d-494f-bb28-214ab53cf555" />

```swift
struct ContentView: View {
    var body: some View {
        LinearGradient(stops: [
            Gradient.Stop(color: .red, location: 0.45),
            Gradient.Stop(color: .black, location: 0.55)]
            , startPoint: .top, endPoint: .bottom)
    }
}
```
<img width="230" alt="Screenshot 2025-07-03 at 11 11 59 PM" src="https://github.com/user-attachments/assets/4916b11c-5b79-4b5c-b0e5-b423c749ac46" />

#### RadialGradient

```swift
struct ContentView: View {
    var body: some View {
        RadialGradient(colors: [.red, .black], center: .center, startRadius: 20, endRadius: 200)
    }
}
```
<img width="197" alt="Screenshot 2025-07-04 at 1 16 47 AM" src="https://github.com/user-attachments/assets/d2fb92e2-fe7e-431f-a6f6-375dc45381bb" />

#### AngularGradient

```swift
struct ContentView: View {
    var body: some View {
        AngularGradient(colors: [.red, .orange, .yellow, .green, .indigo, .blue, .purple], center: .center)
    }
}
```
<img width="191" alt="Screenshot 2025-07-04 at 1 28 55 AM" src="https://github.com/user-attachments/assets/7b3816c5-cfa7-42b1-8532-2033eab601b8" />

#### .gradient
> Add to a color in a foreground or background

```swift
struct ContentView: View {
    var body: some View {
        Text("Text box")
            .frame(maxWidth: .infinity, maxHeight: .infinity)
            .foregroundStyle(.white)
            .background(.indigo.gradient)
    }
}
```
<img width="207" alt="Screenshot 2025-07-04 at 1 44 17 AM" src="https://github.com/user-attachments/assets/88bf0050-9b24-47b2-ae4e-72354f4dbcca" />

## Buttons and images

```swift
struct ContentView: View {
    var body: some View {
        Button("Press") {
            print("Button pressed")
        }
    }
}
```
or
```swift
struct ContentView: View {
    var body: some View {
        Button("Press", action: buttonPress)
    }
    
    func buttonPress() {
        print("Button pressed")
    }
}
```
<img width="150" alt="Screenshot 2025-07-04 at 1 45 10 PM" src="https://github.com/user-attachments/assets/a248e609-4e8f-4706-8ffd-25f0bf15ec78" />

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Button("Button 1") {}
                .buttonStyle(.bordered)
            Button("Button 2") {}
                .buttonStyle(.borderedProminent)
            Button("Button 3", role: .destructive) {}
                .buttonStyle(.bordered)
            Button("Button 4", role: .destructive) {}
                .buttonStyle(.borderedProminent)
            Button("Button 5") {}
                .buttonStyle(.borderedProminent)
                .tint(.green)
            Button {
                print("Something")
            } label: {
                Text("Button 6")
                    .padding()
                    .foregroundStyle(.white)
                    .background(.indigo)
            }
        }
    }
}
```
<img width="211" alt="Screenshot 2025-07-04 at 2 29 03 PM" src="https://github.com/user-attachments/assets/4e3e0ba2-8fc9-4978-9a83-9b68c3f9fea8" />

#### Images

```swift
struct ContentView: View {
    var body: some View {
        VStack {
          Image(decorative: "some image name in catalog")
        }
    }
}
struct ContentView: View {
    var body: some View {
        VStack {
          Image(systemName: "pencil.circle")
        }
    }
}
```
- adding the `decorative: ""` parameter will prevent voiceover from reading the image.
- `systemName:` pulls from the apple catalog

#### Images and buttons together

```swift
struct ContentView: View {
    var body: some View {
        Button("Edit", systemImage: "pencil") {
            print("Button tapped")
        }
        
        Button {
            print("Button tapped")
        } label: {
            Label("Edit", systemImage: "pencil")
        }
    }
}
```
> Use the second option. SwiftUI will automatically decide the formatting style.
<img width="209" alt="Screenshot 2025-07-04 at 2 38 36 PM" src="https://github.com/user-attachments/assets/cde40cdc-23c1-47f5-b84a-c8cf3786bdb2" />

## Alerts

```swift
struct ContentView: View {
    @State private var showAlert: Bool = false
    @State private var word: String = ""
    
    var body: some View {
        Button("Button") {
            showAlert = true
        }
        .alert("Whoa man", isPresented: $showAlert) {
            Button("okiedokie") {}
            Button("Custom destructive", role: .destructive) {}
            Button("Custom cancel", role: .cancel) {}
        } message: {
            Text("This works with TextField too??")
        }
    }
}
```
<img width="150" alt="Screenshot 2025-07-05 at 10 04 21 AM" src="https://github.com/user-attachments/assets/73711528-3ad3-4048-baa7-b0234d4d8312" />

## Stacking up buttons


