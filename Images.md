## Images

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
    }
}
```

> I have my raccoon photo. If it's a static image in my catalog, I can use dot notation.

<img width="150" alt="Screenshot 2025-08-22 at 1 43 41 PM" src="https://github.com/user-attachments/assets/d033c42c-35f2-4f76-beb0-aa4c4f152208" />

## Frames

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

## Clipped modifier

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

## Resizable modifier

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
            .resizable()
            .frame(width: 300, height: 300)
            
    }
}
```

> `.resizable()` allows the image to change size. Without any other modifiers, the pixels are squished into the frame.

<img width="150" alt="Screenshot 2025-08-22 at 1 49 45 PM" src="https://github.com/user-attachments/assets/25dfdf12-18d5-4cf8-ad47-32011783aa43" />

## Scale to Fit

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
            .resizable()
            .scaledToFit()
            .frame(width: 300, height: 300)
            
    }
}
```

> Scale to fit means scale the image to fit inside the frame.
- Note the frame is only showing because of the selectable key.

<img width="150" alt="Screenshot 2025-08-22 at 2 01 23 PM" src="https://github.com/user-attachments/assets/0bb46d4f-7a75-4e86-8a85-bf0af3311f6d" />

## Scale to fill

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
            .resizable()
            .scaledToFill()
            .frame(width: 300, height: 300)
            
    }
}
```

> Scale to fill means scale the image to fill the frame, even if there's overrun.

<img width="150" alt="Screenshot 2025-08-22 at 2 08 40 PM" src="https://github.com/user-attachments/assets/4cfe3f5e-493d-4834-822c-f44051965a35" />

## Container relative frame

```swift
struct ContentView: View {
    var body: some View {
        Image(.raccoon)
            .resizable()
            .scaledToFit()
            .containerRelativeFrame(.horizontal) { size, axis in
                size * 0.8
            }
            
    }
}
```

> - `.containerRelativeFrame` references the container. In this case, the container is the whole screen. Then make a frame relative to the container.
> - `.horizontal` states the axis that the relative container will be compared to.
> - The closure is a little complicated. It requires two parameters, a CGFloat and an axis. Because it's a closure, you pick the names.

<img width="150" alt="Screenshot 2025-08-22 at 2 38 52 PM" src="https://github.com/user-attachments/assets/26ab1ee4-5b26-46a5-b36b-dd1dcf442a14" />

## ScrollView (vertical)

```swift
struct ContentView: View {
    var body: some View {
        ScrollView {
            VStack(spacing: 10) {
                ForEach(0..<100) {
                    Text("\($0)")
                }
            }
            .frame(maxWidth: .infinity)
        }
    }
}
```

> Makes a scrolling view. When views are added, they're rendered immediately, regardless of whether or not the user can see them. If you upload 1000 profiles, that could be an issue.
> `.frame(maxWidth: .infinity` is not `.frame(width: .infinity`. Width requires a specific CGFloat to work.
> 
<img width="150" alt="Screenshot 2025-08-22 at 3 33 45 PM" src="https://github.com/user-attachments/assets/6e26a6ef-9cfe-4135-b4ce-607304f39e1b" />

## ScrollView (horizontal)

```swift
struct ContentView: View {
    var body: some View {
        ScrollView(.horizontal) {
            HStack(spacing: 10) {
                ForEach(0..<100) {
                    Text("\($0)")
                }
            }
        }
    }
}
```

> Horizontal scrollviews require the `.horizontal` parameter.

<img width="150" alt="Screenshot 2025-08-22 at 3 32 08 PM" src="https://github.com/user-attachments/assets/3c4a45dd-b932-4de7-b18c-4f0e232491a8" />


## LazyVStack

```swift
struct ContentView: View {
    var body: some View {
        ScrollView {
            LazyVStack(spacing: 10) {
                ForEach(0..<100) {
                    Text("\($0)")
                }
            }
//            .frame(maxWidth: .infinity)
        }
    }
}
```

> - LazyVStacks only render what is shown. Far better for optimization in certain cases.
> - Note that the .frame isn't used. Lazy VStack(s) take up all available space. It makes sense. What if the new views get progressively larger? It would look weird.

<img width="150" alt="Screenshot 2025-08-22 at 3 34 36 PM" src="https://github.com/user-attachments/assets/08127923-1b02-490a-a91c-d87780a8efa5" />
