## Images

#### .image

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
    }
}
```

> I have my raccoon photo. If it's a static image in my catalog, I can use dot notation.

<img width="150" alt="Screenshot 2025-08-22 at 1 43 41 PM" src="https://github.com/user-attachments/assets/d033c42c-35f2-4f76-beb0-aa4c4f152208" />

#### Frames

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
            .frame(width: 300, height: 300)
    }
}
```
> I've added a frame, but the image doesn't change. If i click the *selectable* button at the bottom of the preview, you can see the frame.

<img width="150" alt="Screenshot 2025-08-22 at 1 44 32 PM" src="https://github.com/user-attachments/assets/cc93fcbe-be01-476e-9abd-7c05804fa54f" />

#### Clipped modifier

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
            .frame(width: 300, height: 300)
            .clipped()
    }
}
```

> By adding the `clipped()` modifier, I have clipped all pixels outside the frame.

<img width="150" alt="Screenshot 2025-08-22 at 1 47 57 PM" src="https://github.com/user-attachments/assets/0a33d3e2-1ba0-4b9e-b725-b5ebf46662d4" />

#### Resizable modifier

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
            .resizable()
            .frame(width: 300, height: 300)
            
    }
}
```

> `.resizable()` squished the pixels into the frame.

<img width="150" alt="Screenshot 2025-08-22 at 1 49 45 PM" src="https://github.com/user-attachments/assets/25dfdf12-18d5-4cf8-ad47-32011783aa43" />
