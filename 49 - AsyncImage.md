### AsyncImage

```swift
struct ContentView: View {
    var body: some View {
        AsyncImage(url: URL(string: "https://hws.dev/img/logo.png"))
    }
}
```
> This image is 1200 pixels high. Swift doesn't know that until it's downloaded. 
<img width="150" alt="Screenshot 2025-09-09 at 10 41 34 AM" src="https://github.com/user-attachments/assets/7772136a-2a5e-4c38-96ee-243e220f0400" />

### scale

```swift
struct ContentView: View {
    var body: some View {
        AsyncImage(url: URL(string: "https://hws.dev/img/logo.png"), scale: 3)
    }
}
```
> By adding a scale parameter, it now knows to apply this to the 3x parameter and can shrink accordingly.
> However, it's extremely limited in the scaling.
<img width="150" alt="Screenshot 2025-09-09 at 10 43 16 AM" src="https://github.com/user-attachments/assets/30f20ec0-96e3-4cf1-88b3-065e2a418f52" />

### Making it behave like a normal image

```swift
struct ContentView: View {
    var body: some View {
        AsyncImage(url: URL(string: "https://hws.dev/img/logo.png")) { image in
            image
                .resizable()
                .scaledToFit()
        } placeholder: {
            ProgressView()
        }
        .frame(width: 200, height: 200)
    }
}
```
> The placeholder is necessary, because something always has to be there.
<img width="150" alt="Screenshot 2025-09-09 at 10 55 48 AM" src="https://github.com/user-attachments/assets/6bab35bf-ff38-42e8-b3b3-e5b6fd44aa50" />
> Image or loading image
### Complete control

```swift
struct ContentView: View {
    var body: some View {
        AsyncImage(url: URL(string: "https://hws.dev/img/logo.png")) { phase in
            if let image = phase.image {
                image
                    .resizable()
                    .scaledToFit()
            } else if phase.error != nil {
                Text("Issue loading image")
            } else {
                ProgressView()
            }
        }
        .frame(width: 200, height: 200)
    }
}
```
> This is best for when you want to show a default view when the image fails to load. This just added a textbox for if the view fails.
> Image, loading image or Error(possible image)
<img width="150" alt="Screenshot 2025-09-09 at 11 00 27 AM" src="https://github.com/user-attachments/assets/0e4b32b2-8645-43da-ac4a-40f2c83cf1a6" />

