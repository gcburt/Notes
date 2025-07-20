### CGFloat and .scaleEffect

```swift
struct ContentView: View {
    @State private var animationAmount = 1.0
    
    var body: some View {
        Button("BIG RED SHINY BUTTON") {
            animationAmount += 1
        }
            .padding(100)
            .background(.red)
            .foregroundStyle(.white)
            .clipShape(.circle)
            .scaleEffect(animationAmount)
            .animation(.default, value: animationAmount)
    }
}
```
1. `.scaleEffect(animationAmount)` causes the button to grow larger
2. `.animation(.default, value: animationAmount)` smooths out the transition

> Some older systems use floating point numbers for displays, logic, etc. Swift uses far more precise Doubles. To bridge the two data types, Apple created `CGFloat`, a structure that normally operates as a double, but can silently turn into a floating point number when necessary. Sometimes, you'll see CGSize. That is just another struct that contains multiple CGFloat's
> In this example, .scaleEffect contains a GCFloat of animationAmount. You can use Double and CGFloat interchangably.
> CG stands for Core Graphics
